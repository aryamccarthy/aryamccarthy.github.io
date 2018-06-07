---
layout: paper
title: "Composing graphical models with neural networks for structured representations and fast inference"
authors: "Johnson et al."
year: 2016
venue: NIPS
link: "https://arxiv.org/pdf/1603.06277.pdf"
---

*NB: I link to an updated version of the paper on arXiv. Wish they could retroactively correct the NIPS version.*

My office the summer I worked at Harvard was right across from Ryan P. Adams's. Cool to see that he's making contributions at Twitter. The gist of this paper is that they've connected nonlinear likelihoods to latent-variable graphical models. 

<!--more-->

Neural networks are flexible but slow and opaque. Graphical models are interpretable and quick to perform inference with but rigid. What if we could combine them? 

We rely on **conjugacy**: priors and likelihoods from the same family will have a posterior (basically their product) in the same family. This gives closed-form solutions that can be efficiently assessed. By contrast, a VAE (the hot new neural network architecture) that uses a Gaussian prior and a nonlinear likelihood model won't have a nice, clean posterior. (If prior, likelihood, and posterior are confusing words, check out Bayes's rule.)

The magic comes in the form of a **conditional random field (CRF)**, a particular family of graphical models. Let a neural network output the CRF's potentials instead of parameters of the distribution.

By learning to compute the potentials then using the CRF to reason with them, they preserve the fast inference that they'd like to have. 

