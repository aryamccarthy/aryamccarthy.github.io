---
layout: paper
title: "Extreme Adaptation for Personalized Neural Machine Translation"
authors: "Michel and Neubig"
year: 2018
venue: ACL
link: "https://arxiv.org/abs/1805.01817"
---

While I was at [MTMA](http://www.statmt.org/mtma18/index.php), a quick one-night project I explored with [Brian Thompson](https://www.ll.mit.edu/mission/cybersec/publications/publications-by-author/thompson-b.html) was whether we could fiddle with biases in the final softmax layer of an <abbr title="Neural machine translation">NMT</abbr> model to perform domain adaptation, purely off word frequency. Short answer: no, or at least not how we did it.

Michel and Neubig thought of bias-meddling [and made it work (!)]. Instead of adapting to new domains, they adapted to individual speakers by learning how to update the biases correctly. This paves the way for speaker-specific MT, as well as inferring properties of speakers.

<!--more-->

|Source           | Speaker | Translation
|-----------------|------|---|
|I went home      |Man   |Je suis rentré à la maison
|                 |Woman |Je suis rentrée à la maison
|I do drug testing|Doctor|Je teste des médicaments
|                 |Police|Je dépiste des drogues


We all have our own [idiolect](https://en.wikipedia.org/wiki/Idiolect)—our personal style of speaking. Different facets of our identity like gender, social status, and geographical origin affect our word choice and preferred [phrasal constructs]({{ "/becker1975phrasal"  | absolute_url }}). At the moment, NMT doesn't factor this into its decision process.

The sequence-to-sequence model for NMT is an end-to-end process: feed words in, get words out, the end. The last two layers are a linear (well, affine) layer and a softmax layer: one that turns scores into a probability distribution over all words in the vocabulary of the target language. The probability of the next word&nbsp;\\(e_i\\) being output given its context&nbsp;\\(\mathbf{c}_i\\) is given below.

$$ \Pr(e_i | \mathbf{c}_i) = {\rm softmax}(W\mathbf{c}_i + \mathbf{b})_i$$

The context is the current state of the decoder, captured in the hidden state vector of the decoder's RNN. The softmax function exponentiates and normalizes its arguments—vector in, vector out. We then select the \\(I\\)th position, which contains the probability of word \\(e_i\\). Think of \\(W\\) as embeddings for each word. You maximize the matrix-vector product where your embedding is most similar to the context. The bias term reflects the overall preference for individual words. We then choose the word with the highest score. 

More broadly, in NMT, we have a probability distribution over target-language words conditioned on source-language words: \\(\Pr(y \mid x; \theta)\\). The authors argue for making our parameters \\(\theta\\) domain-specific. Their speaker adaptation task is the limit of low-resource domain adaptation: there are hundreds of speakers (domains) and very little text per speaker. With so many speakers, individual parameters per person would be utterly infeasible. Plus, training on such small data would lead to major overfitting. Hopefully, we can exploit commonalities between speakers—both as a regularizer and a way to reduce the footprint.

Michel and Neubig present three models:

1. `spk_token`: Identifying the speaker by appending a speaker-specific token to the start of the target sentence. (Target seems fishy—how would that work? I've emailed for clarity.)
2. `full_bias`: Learning a bias vector for each speaker. (Still loads smaller than all of the parameters.) The biases for all speakers over all vocabulary words is \\(B \in \mathbb{R}^{\mid\mathcal{S}\mid \times \mid \mathcal{V} \mid}\\).
3. `fact_bias`: 'fact' for factored, as in sharing information. The authors realize that the current format can't share information—each speaker is completely independent. How can we enforce that sharing? By splitting \\(B\\) into the product of two low-rank matrices: \\(B = S \tilde{B}\\), with \\(S \in \mathbb{R}^{\mid\mathcal{S}\mid \times k}\\) and \\(\mathbb{R}^{k \times \mid \mathcal{V} \mid}\\). This has drastically fewer parameters for reasonable values of \\(k\\).

In the last two cases, the bias vector is added to the others; now, the probability of the next word is this:

$$ \Pr(e_i | \mathbf{c}_i) = {\rm softmax}(W\mathbf{c}_i + \mathbf{b}_{all} + \mathbf{b}_{speaker})_i$$


*As a linear algebra aside, [you can factor \\(B\\) into its optimal pair of low-rank matrices with rank \\(k\\)](https://nlp.stanford.edu/IR-book/html/htmledition/low-rank-approximations-1.html) using singular value decomposition, the mathemagic behind PCA. The speaker biases become a linear combination ("mixture" is the [hip ML word](https://brenocon.com/blog/2008/12/statistics-vs-machine-learning-fight/) for it) of the "centroid" biases—the basis vectors.*

They tested with bootstrap resampling, which I've [taken issue with in the past]({{ "/passban2018improving" | absolute_url }}), but it doesn't really matter. Their factored bias model gets just shy of a full BLEU point better than the baseline.

As additional, non-BLEU validation, they also put together a classifier to suss out who the speaker of the sentence was. It performs better on the non-baseline models, so speaker-specific information seems to be incorporated. They also included a yes on the EuroParl corpus (proceedings of the European Parliament) to see whether it was topic information, not just speaker information, that helped the model.

**The bottom line:** With as low as 10 parameters per person, the authors are able to massively adapt their NMT system to different speakers or domains, with modest improvements in BLEU.
