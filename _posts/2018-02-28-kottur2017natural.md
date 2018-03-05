---
layout: paper
title: "Natural Language Does Not Emerge 'Naturally' in Multi-Agent Dialog"
authors: "Kottur et al."
venue: EMNLP
year: 2017
link: "https://aclweb.org/anthology/D17-1321"
---

Did you like yesterday's paper? Too bad. Today's calls it out. (Not because its methods were bad, but because it's a stretch to call what it did "natural language". Yoav Goldberg has presented [a similar critique](https://medium.com/@yoav.goldberg/an-adversarial-review-of-adversarial-generation-of-natural-language-409ac3378bd7) of other work.) This paper calls out some shortcomings in approaches before yesterday's: that passive, corpus-based conversation agents never learn grounding: the mapping between physical concepts and words. It also points out something that yesterday's Lewis game agents couldn't do: compositionality. Since the Lewis sender is restricted to one symbol, how could it ever compose ideas?

<!--more-->

We start off with an introduction to the same Lewis game framework as yesterday. The paper introduces the language of "Q-bot" and "A-bot", but it's easier for me to think of these in the same vocabulary as yesterday: "receiver" and "sender". A counter to compositionality is that a "sender" with a large enough vocabulary will take the one-big-lookup-table approach: match every entity to one symbol, regardless of the composition of its attributes, like Jorge Luis Borges's [Funes the Memorious](https://en.wikipedia.org/wiki/Funes_the_Memorious). This obviously makes it hard for the receiver to understand unseen examples.

But in this game, the receiver can also query the asker about properties of the entity. (This is what differentiates their model from the one last week.) It doesn't always ask the same questions, so A's symbol usage is entirely contextual. If we restrict A's vocabulary farther, plus eliminating its state vector (its memory), we get something that takes a bit more thinking.

The cool parts of this paper were playing with varying the vocabulary sizes. We already looked at the huge vocabulary. At the other end of the spectrum, you can constrain the vocabulary to force generality: if there are four options for a given question and four symbols in the vocabulary, you learn to overload the symbols as responses to questions.
