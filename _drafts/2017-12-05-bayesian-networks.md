---
layout: post
title: Scale-Free Networks and Chinese Restaurants
---

[TOC]

- Chinese Restaurant Process (or urn scheme) as a metaphor for Dirichlet process
- Those are preferential attachment models (rich get richer)—positive feedback.
  - Those are also common in citation networks: people cite popular papers, giving them more visibility, making them more popular.
  - And related to fault tolernce: random failures generally strike small nodes, and a few big nodes gone maintain connectedness.

Attachment probability in CRP:
	$\frac{size(i)}{\sum_j size(j) + \alpha}$
Attachment probability to *each* node:
	$\frac{\deg(i)}{\sum_j \deg(j)}$
  
Incidentally, it's really common evidently to normalize things by their maximum. 

Let's define the scaling:
$$s(G) = \sum_{(u,v) \in E} \deg(u) \cdot \deg(v)$$
Now we normalize it by the max over all graphs with the same distribution.
$$S(G)=\frac{s(G)}{s_{\text{max}}}$$
where $s_{\text{max}}$ is the max of $s(H)$ for $H$ in all graphs with identical degree distribution to $G$. 

^^ Does this need to be adjusted for chance? How do you compute *this* expectation $\mathrm{E}_H[s(H)]$?


Barabasi-Albert model is a parameterization of the Yule distribution, which describes urn schemes.

## Properties: why do we care? 
