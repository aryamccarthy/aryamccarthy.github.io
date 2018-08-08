---
layout: paper
title: "Deciphering Foreign Language"
authors: "Ravi and Knight"
year: 2011
venue: ACL
link: "https://www.aclweb.org/anthology/P11-1002"
---

Did you like those puzzle games as a kid? The ones where you had to unscramble or shift letters to find a secret message? That's the approach that Ravi and Knight take to translation in the **zero-resource setting**: when no parallel text is available in the target language.

<!--more-->

The paper was published a few years before neural machine translation became hot, so it starts off with an overview of the [IBM models](https://en.wikipedia.org/wiki/IBM_alignment_models), the starting point of statistical translation. The authors see this as a problem that's slightly different from MT, but they frame it in that context. The usual approach to learning in these models is to find parameters that maximize the likelihoods of each translation in the training data—the product of each sentence pair's likelihood:

$$ \arg\max_\theta \prod_{\langle \mathbf{e}, \mathbf{f}\rangle} \Pr_\theta(\mathbf{f} \mid \mathbf{e}) $$

(We stick to the notational convention that we want to translate a foreign sentence \\(\mathbf{f}\\) into an English sentence \\(\mathbf{e}\\).)

Implicit in the IBM models is an alignment between the words of the source and target sentences. We want to *marginalize out* the alignment—to sum over all possible manifestations, so that the alignment isn't explicit. (The alignment is a **latent variable**.) This is equivalent to the above expression, but it makes the dependence on the alignment explicit:

$$ \arg\max_\theta \prod_{\langle \mathbf{e}, \mathbf{f}\rangle} \sum_\mathbf{a} \Pr_\theta(\mathbf{f}, \mathbf{a} \mid \mathbf{e}) $$

In the setting that Ravi and Knight care about, we don't have aligned sentence pairs to train on. We just want to find parameters that maximize the likelihood of those foreign strings:

$$ \arg\max_\theta \prod_\mathbf{f} \Pr_\theta(\mathbf{f}) $$

We can then do that same trick as above to say that we're marginalizing out all possible English sentences. This relies on the definition of [conditional probability](https://en.wikipedia.org/wiki/Conditional_probability#Conditioning_on_an_event). 

$$ \arg\max_\theta \prod_{\mathbf{f}} \sum_\mathbf{e} \left[\Pr(\mathbf{e}) \cdot \Pr_\theta(\mathbf{f} \mid \mathbf{e})\right] $$ 

The first term is what's called a **language model**: a probability distribution over all possible sentences. Usually, this is an \\(n\\)-gram model trained on separate data. The second term is the same one we saw earlier, which we split the alignment out of. Let's apply that again here. (Remember that this expression and the two before it express the same quantity. Now both the alignment and the English sentence for a given foreign sentence are latent variables.)

$$ \arg\max_\theta \prod_{\mathbf{f}} \sum_\mathbf{e} \left[\Pr(\mathbf{e}) \cdot \sum_\mathbf{a} \Pr_\theta(\mathbf{f}, \mathbf{a} \mid \mathbf{e})\right] $$ 

The way to train this foreign-sentence-decipherment model is probabilistically. We need to maximize the probability of the foreign sentence, assuming that it was generated according to a **generative story** that we choose, typically one that's simple to compute by making some limiting assumptions.

Before we focus on the foreign language decipherment, let's look at a simpler decipherment problem: a simple word substitution. Every English word gets mapped, deterministically, to a made-up string of characters. The generative story looks like this:

1. Generate the English plaintext sequence \\(\mathbf{e} = e_1, \ldots, e_n\\) with probability \\(\Pr(\mathbf{e})\\).
2. Substitute each English word \\(e_i\\) with a cipher word \\(c_i\\). The probability of a substitution is \\(\Pr_\theta(c_i \mid e_i)\\). We wind up with a cipher text sequence \\(\mathbf{c}\\).

The usual algorithm to optimize the IBM models is Expectation–Maximization. It scales quadratically with vocabulary size, though, so the authors propose a variant. They replace rare words with one token, `UNKNOWN`, keeping the top \\(K\\). This significantly limits the vocabulary size, while still handling the vast majority of tokens observed. Here's the twist: On every iteration of EM, they expand the vocabulary, taking the next \\(K\\) words in addition to the ones already included. To keep this from exploding into a huge model, they take any mappings that are above a given probability threshold as "truth", freeze those parameters, and take them out of the parameters that ned to be optimized. Now, there are fewer than, say, \\(2K + 1\\) parameters to deal with.

They also develop some techniques that they call Bayesian to reduce the sampling cost at each each step of decoding the model—essentially, they lean hard on their language model and use Map-Reduce to parallelize the sampling.

The next innovation is an improvement on IBM Model 3, incorporating Bayesian learning to avoid memory issues.

Other tricks:

- They use "linguistic knowledge"—they know that "8" maps to "8" (Artexte et al. use this later to do MT without parallel text) and they split nouns into morphemes: "YEAR" --> "YEAR" + "S"
- They get out of the issue that n-gram models have (forgetting what they said awhile ago) by having a language model that only recognizes whole segments.

Short-story version of their results: in low-resource settings, their model gets between a quarter and a half of the BLEU of models which are trained with the correct target sentence (IBM Model 3 and the famous MOSES system). Unfortunately, some of these points might come from their seed vocabulary of numbers, etc. Hard to say exactly how impressive this is, but it's certainly an interesting model.
