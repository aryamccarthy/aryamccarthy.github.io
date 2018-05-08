---
layout: paper
title: "A Unified Architecture for Natural Language Processing: Deep Neural Networks with Multitask Learning"
authors: "Collobert and Weston"
year: 2008
venue: ICML
link: https://ronan.collobert.com/pub/matos/2008_nlp_icml.pdf
---

You know what's cool? Doing multitask learning that's *actually* multitask learning, instead of arbitrarily calling something multi-task (like morphological re-inflection). This paper presents a deep model that attempts to do it all for NLP: tagging, chunking, NER, semantic roles, and on and on.

<!--more-->
---

Let's start by discussing what multi-task learning (MTL) is and why you'd want to do it. When you train for one task, you risk overfitting. Your model may treat noise in the training data as signal. Training for multiple tasks acts as a regularizer (basically a prior, [for you Bayesians]({{ "/knight2009bayesian" | absolute_url }})). Your encoder is shared across multiple tasks, then different output layers pertain to each task. The encoder's parameters are updated, whatever the task, by back-propagation. A great blog post about MTL is [here](http://ruder.io/multi-task/).

This paper was one of the deep learning papers from before deep learning became a buzz word, so they belabor the fact that before neural networks, you'd have to hand-engineer features—which required research and time investment. Neural nets instead can approximate general functions, and they're trained automatically. This paper is advocating what is now standard, before it was standard.

It also goes into details about pieces that are nowadays glossed over. What's a word embedding? Ask this and you'll get dumb looks. "It's a vector representation of a word." Sure, but where does that vector come from? This paper makes that point quite well. It's a lookup table. Assume (for simplicity) a finite vocabulary. The word types (as opposed to tokens) can be numbered 0, 1, 2, …, N. Get the ith vector. This is the representation of that word. The individual values here can be randomly initialized, then updated to be more useful during the back-propagation that occurs in training.

If a word has multiple features (capitalization, etc.), you can have separate lookups (embeddings) for each feature, then concatenate them all to get a long representation of the word.

---

They also note the issue that not all sentences are the same length, but normal NNs require fixed-length sequences. One way would be to take windows of the sentence, which is dangerous. Just think—is even a 50-gram language model enough for grammaticality judgments?

Instead, the authors dug up a paper from 1989 on "time-delayed neural networks" (TDNN) which are basically convolutional neural nets. You output a sequence of representations that take the whole sentence into consideration, then "pool" these together using an operation like `max`, which condenses the entire sequence into a fixed-size representation—which can now be fed into a normal NN. This lets it consider the entire sequence at once, as opposed to the simple sliding window. They choose `max` (as opposed to, say, `sum` or `average`) because they believe it will find the "most relevant features over the sentence".

I found their formula incredibly opaque, so I implemented a Python snippet to show how the convolutional filter moves over the sentence. 

```python
n = 5  # Sentence length
ksz = 3  # Kernel size
for t in range(1, n + 1):  # "Time"—position in the sentence
    print(f"t = {t}")
    # output[t] = sum(L_j * x[t+j] for j in (1 - t) to (n - t))
    for j in range(1 - t, n - t + 1):
        # Only show the filter L_j if it's within our window.
        print(f"  j = {(j if not abs(j) > (ksz - 1) / 2 else ''):4}\tt+j = {t+j:4}")
```

```
t = 1
  j =    0	t+j =    1
  j =    1	t+j =    2
  j =     	t+j =    3
  j =     	t+j =    4
  j =     	t+j =    5
t = 2
  j =   -1	t+j =    1
  j =    0	t+j =    2
  j =    1	t+j =    3
  j =     	t+j =    4
  j =     	t+j =    5
t = 3
  j =     	t+j =    1
  j =   -1	t+j =    2
  j =    0	t+j =    3
  j =    1	t+j =    4
  j =     	t+j =    5
t = 4
  j =     	t+j =    1
  j =     	t+j =    2
  j =   -1	t+j =    3
  j =    0	t+j =    4
  j =    1	t+j =    5
t = 5
  j =     	t+j =    1
  j =     	t+j =    2
  j =     	t+j =    3
  j =   -1	t+j =    4
  j =    0	t+j =    5
```

(You may notice the similarity to [Toeplitz matrices](https://en.m.wikipedia.org/wiki/Toeplitz_matrix), which create diagonal bands of values. Here, you can picture a row of the matrix as representing a given time step and the values representing the identities of the filters. These move one step to the right at each time step.)

---

After the convolutional and pooling layers, you can add other standard neural network layers. The last two layers, though, should be (1) an output layer with N nodes, one for each possible output, and (2) a *softmax* layer, which turns the outputs of that layer into a probability distribution, making them positive with a sum of 1. 

Because this is a multi-task problem, the models don't need to share anything after the pooling layer. Each can go off and do its own thing with the pooled output. When they train, they can update both their own parameters and the convolutional layer's. Alternatively, you can split off even earlier, only sharing the word embeddings. Each task can have its own convolutional layers.

Without belaboring their results, they got good results on all the tasks they considered. **TL;DR:** Multi-task learning helps NLP.
