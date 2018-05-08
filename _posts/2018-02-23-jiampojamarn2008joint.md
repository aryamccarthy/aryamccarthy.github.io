---
layout: paper
title: "Joint Processing and Discriminative Training for Letter-to-Phoneme Conversion"
authors: "Jiampojamarn et al."
year: 2008
venue: ACL
link: "https://www.aclweb.org/anthology/P/P08/P08-1.pdf#page=949"
---

Ah, joint learning. It's cool, isn't it? It lets information flow both ways: the intermediate representations have to be good for later tasks. This paper jointly learns input segmentation, phoneme prediction, and sequence modeling.

<!--more-->

Letter-to-phoneme (L2P; moving from the alphabet of written letters to the alphabet of sounds) is a tricky task—think of the English words "comb", "come", "home". The authors point to Kominek and Black, who show that the number of rules can grow with the lexicon size.

If you have an alignment between the letters and phonemes of some text, you can treat L2P "as a sequence of classification problems, or as a sequence modeling problem." If it's classification, you use multi-class classifiers to predict the right phoneme given a letter and its context. This turns each phoneme into an independent prediction. A sequential model would acknowledge the conditional dependencies between neighboring phonemes, treating it as a tagging problem. This doesn't let you incorporate context as well. We need instead something that meets three goals:

> 1. The phoneme predicted for a letter should be informed by the letter’s context in the input word.
> 2. In addition to single letters, letter substrings should also be able to generate phonemes.
> 3. Phoneme sequence information should be included in the model.

The hope (and motivation for a joint model) is to not have errors propagate forward, and to find the optimal parameters for each subtask *given the later tasks*. Their solution: Collins's **perceptron HMM**. It out-of-the-box handles goals 1 and 3 out of the box, and it lets you use overlapping n-gram features. Finally, they tick off #2 by using a "monotone phrasal decoder" to perform segmentation.

So now what do we have? Something that can be discriminatively trained. We keep finding the best output given the weights, then updating the weights to favor correct answers. (It's like what we do with back-propagation in neural networks.)

They claim to use only binary features, considering each piece of context. This means that their feature vocabulary must be huge—they're modeling the presence of n-grams. It also means that their approach would fall apart in, say, Chinese.

They pull a trick out of machine translation to avoid Viterbi decoding, instead using the "monotone search algorithm" of [Zens and Ney](https://www.aclweb.org/anthology/N04-1033). (Monotone: It doesn't allow reordering.) The advantage of this search is that it allows translation of entire phrases (n-grams), rather than just words (letters). 

On top of the perceptron algorithm, they use a trainer called MIRA: Margin Infused Relaxed Algorithm. Perceptrons don't update weights if they're already predicting correctly. MIRA, on the other hand, tries to increase the margin when it gets things right, trying to update in favor of the best sentence, down-weighting other sentences from the n-best list. (This is the same thing as we saw in [the DopeLearning paper]({{ "/malmi2016dopelearning" | absolute_url }}) for training given a list of candidates. They just didn't call it MIRA.)

