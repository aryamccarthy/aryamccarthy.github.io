---
layout: paper
title: "A Distributional and Orthographic Aggregation Model for English Derivational Morphology"
authors: "Deutsch, Hewitt, and Roth"
year: 2018
venue: NAACL
link: "https://www.aclweb.org/anthology/P18-1180"
---

Derivational morphology is that awkward, messy uncle that nobody really talks about, compared to its golden-boy sibling inflectional morphology. The authors present an improved system for generating derivational forms from their base words. 

<!--more-->

## Their innovative model: nearest neighbor search of word embeddings

Rather than look at the relationship in embedding space between all word pairs using a particular suffix, they look at all pairs using a particular transformation of meaning, like turning a verb into a noun which performs that verb's action.

They also do a bit of filtering: nearest neighbor search in the embedding space suffers from a hubness problem—some words are everybody's neighbor. Their heuristic is to take only words that start with the same 4 letters as the base word. 

## Their seq2seq model

There isn't a perfect match between meaning and derivational suffixes. "-er" in "baker" marks an agent, but "-er" in "burner" marks a patient (the semantic object of the action). The authors collect word forms from a corpus, constraining their sequence-to-sequence word generator such that it only considers forms that they've observed. 

The authors do rescoring by including both the seq2seq model's score and the word's frequency in the corpus as features into a simple neural network (a single-layer perceptron).

## Other notes

- They found that shortest-path search was not much more expensive than beam search, so why not try it? Does about as well.
    - They say shortest path explores far fewer states than beam search. How can this be, when beam search restricts the search space and shortest path is exhaustive?
- Nominal transformations were the biggest improvement over the baseline—there are lots of possible affixes, so the dictionary constraint helps restrict them to reasonable ones.


**Future work.**

- Label bias. It's a thing that'll come up when searching through that trie—it's called the 'beam problem' in MT. A recent proposal ameliorates this by performing a weak form of global scoring.
