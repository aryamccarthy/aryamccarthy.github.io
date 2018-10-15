---
layout: paper
title: An Exploration of Neural Sequence-to-Sequence Architectures for Automatic Post-Editing
authors: Junczys-Dowmunt and Grundkiewicz
year: 2017
venue: IJCNLP
link: http://aclweb.org/anthology/I17-1013
---

Automatic post-editing (APE) exists because our translation models are fallible. (Hopefully, they're also fallible in reliable ways.) Once your translation system has spit out a predicted translation of a sentence, you can feed both the prediction and the original, foreign sentence into your APE system to clean it up, making it feel more human. This paper presents a neural architecture for APE—it's similar to the [traditional neural MT architecture](https://aryamccarthy.github.io/bahdanau2015neural/), but with dual attention—one over the source, and one over the translation output.

---

<!--$$\begin{eqnarray}
mt &=& \textrm{MT-SYSTEM}(src) \\
pe &=& \textrm{APE}(mt, src)
\end{eqnarray}$$-->

Before the age of neural MT, post-editing generally was a phrase-based MT process. An automatically produced alignment would help create a new, "source-context aware", source text. It would have the tokens of the MT output and the tokens of the original source paired together.

This paper, leaping into the neural age, builds on the standard model (plus a few additions made in the Nematus toolkit—the decoder is wonky, using GRUs out the wazoo). They introduce four model variants. To understand them, we should understand the difference between hard and soft attention. Soft attention means that multiple encoder states can make fractional contributions to picking the output token of the decoder. Hard attention makes you rely on only one state per output token. It's like the relationship between k-means and a Gaussian mixture model.

1. **Hard, monotonic attention.** This borrows from [Aharoni and Goldberg](http://aclweb.org/anthology/P17-1183)'s system for morphological inflection—another string transduction task. The system can predict not only a word, but also a special symbol \<STEP\> which forces the attention mechanism to advance to the next encoder state. To precompute the \<STEP\> tokens interleaved into the input, the authors use the Longest Common Subsequence between the MT output and the correct translation.
1. **Hard and soft attention.** Hard attention meant swapping out the decoder for something without the standard attention mechanism. What if we brought it back? Append the hard attention's encoder state to the standard (soft) attention's state.
1. **Soft dual-attention.** This is the idea of [Zoph and Knight](http://www.aclweb.org/anthology/N16-1004), but expressed more clearly. Let's compute standard attention over both the source (which was previously unused) and the MT output—each from separate encoders—then concatenate those.
1. **Hard attention with soft dual-attention.** Strap two of those hard-and-soft mechanisms together. 

The authors followed the conventions of the 2016 WMT shared task on automatic post-editing, including evaluation by [Translation Edit Rate (TER)](https://www.cs.umd.edu/~snover/pub/amta06/ter_amta.pdf), with the widespread BLEU as only a secondary metric.

They also performed model averaging—taking the best 8 checkpoints from the training process. This regularization, they found, improved performance.

--- 

Enough about their experimental framework. Let's dig into error analysis.

They found that their models chose to edit 75–80% of the sentences, no matter what. The majority were improved, while about a quarter of the edited sentences were deteriorated.

The authors present visualizations of their attention matrices. 

> For CGRU-HARD [hard and soft dual-attention], it is interesting to see how the monotonic attention now allows the soft attention mechanism to look around the input sentence more freely or to remain inactive instead of following the monotonic path.

**TLDR:** Use both sequences for APE. Dual attention over both the original source and the MT output that needs editing does better than just editing the output while ignoring the source.
