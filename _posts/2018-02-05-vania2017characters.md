---
title: "From Characters to Words to in Between: Do We Capture Morphology?"
layout: post
excerpt_separator: <!--more-->
---

([Vania and Lopez, 2017](https://www.aclweb.org/anthology/P17-1184)) at ACL

We know that words exist, and we know that we can break them up into smaller parts—"rereading" can be broken into the morphemes `["re-", "read", "-ing"]`, or into the characters `["r", "e", "r", "e", "a", "d", "i", "n", "g"]`. Today's paper explores which of these levels is the best representation for language modeling. It also shows the benefit of morphological analysis—without it, even tons more data won't carry the day.

<!--more-->

The authors pose four questions:

>
1. How do representations based on morphemes compare with those based on characters?
2. What is the best way to compose subword representations?
3. Do character-level models capture morphology in terms of predictive utility?
4. How do different representations interact with languages of different morphological typologies?

To answer these, we should first sort out some preliminary terminology:

- **morpheme:** smallest unit of meaning. They can be bound ("-ing") or free, and they can express core meaning ("to run") or features (past-tense).
- **morph:** the surface realization of a morpheme. In "tries", the morphemes are "try+s", while the morphs are "tri+es". 
- **morphological analysis:** breaking a word into its lemma (dictionary form) and features. try+VB+3rd+SG+Pres.

- **Fusional language**: concatenates single morphemes realizing multiple features. An example is English.
- **Agglutinative language**: One feature per morpheme, like Turkish. 
- **Root and Pattern morphology** (I've heard this as 'templatic'): insert sounds around and between a stem of consonants. Arabic is the biggest example.
- **Reduplication**: repeating part or all of the word, giving new meaning. Indonesian uses this to pluralize.

---

The task they approach is language modeling, which is super important in language and speech processing. Its objective is to fnd the probability of a given sequence of text, and it does this by decomposing it according to the chain rule, such that each next word (or character, or what have you) depends on the part before it. They employ ten different models, combining different encodings and composition methods. Each has a finite output vocabulary, so they compare outputs using perplexity.

One of the authors is supported by an Indonesian endowment, which may explain the interest in reduplicating languages. In any case, the results strongly suggest that in the absence of annotated data, character trigrams are the way to go. But annotated data brings you so much farther, consistently achieving lower-perplexity models. (That is, models that were less surprised by the next thing they saw.) BPE actually turned out ggarbage words in many cases. And the bi-LSTM composition method, which brings information from each direction into each representation, outperformed simple addition. (Again, no big surprises here. Complex learned functions doing well?)

The often-extreme benefit of morphological annotations, the authors note, begs for bootstrapping. A structured autoencoder would be a good way to model the morphological analyses as a latent variable, generating more labeled data. Maybe I should do that...

**The bottom line:** Your best bet for language modeling is annotated data. Lacking that, use the output of bi-LSTMs with character trigrams as input.
