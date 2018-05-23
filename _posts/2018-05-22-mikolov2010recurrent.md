---
layout: paper
title: "Recurrent neural network based language model"
authors: Mikolov et al.
venue: INTERSPEECH
year: 2010
link: "http://www.fit.vutbr.cz/research/groups/speech/publi/2010/mikolov_interspeech2010_IS100722.pdf"
---

Neural networks, the broken record of modern NLP. This paper presents a 50% reduction in the perplexity of a language model when RNNs are used, instead of n-gram backoff. This paper was cool because it's a rare example of both better results and faster training.

<!--more-->

The goal of language modeling is to incorporate fluency into sequential outputs. This is typically done by predicting the next word given its context. The authors claim that there's a disconnect between the simple models used in downstream tasks like [machine translation](https://en.wikipedia.org/wiki/Machine_translation) and the complex models emerging from research.

The first person to construct a neural network for a language model was [Bengio](http://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf). Unfortunately, this was a standard feed-forward network, unable to leverage arbitrarily large contexts. Recurrent neural networks sidestep this problem. Arbitrarily long data can be fed in, token by token. The math shakes out as follows, where \\(\mathbf{w}_1, \ldots, \mathbf{w}_T\\) is a sequence of vectors representing each word and \\(\mathbf{h}_t\\) is the hidden states at time step \\(t\\). Their paper proposes [one-hot encoding](https://en.wikipedia.org/wiki/One-hot) of each word, though we don't do that much anymore—[thanks to the first author](https://arxiv.org/abs/1301.3781).

$$ \mathbf{x}_t = [\mathbf{w}_t, \mathbf{h}_{t - 1}] $$

$$ \mathbf{h}_t = \sigma\left(W \cdot \mathbf{x} \right) $$

$$ \mathbf{y}_t = \mathrm{softmax}\left( V \cdot \mathbf{h}_t \right) $$

(We've previously discussed the sigmoid activation function as a way to squash an arbitrary value to the range \\((0, 1)\\) and softmax as a differentiable way of squeezing a vector of real-numbered scores into a probability distribution.)

To train the network, their loss function is simply the difference between the softmax output and the desired vector—a one-hot vector where the current word is 1 and all others are zero. They also replace words rarer than some threshold with a rare-word token. The stunning part is that they claim 6 hours to train, compared to Bengio's 26 hours (or 113 *days* without importance sampling). It's not often that you find a win for both speed and accuracy, but this is one. [Durrett and Klein (2013) is another.]


