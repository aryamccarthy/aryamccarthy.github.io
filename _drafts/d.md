---
layout: paper
title: "Asymptotic analysis of the stochastic block model for modular networks and its algorithmic applications"
authors: "Decelle et al."
year: 2011
venue: Physical Review E
link: https://arxiv.org/pdf/1109.3041.pdf
mathjax: true
---

*Aside: Journals, don't hide your entries behind [a login](https://journals.aps.org/pre/abstract/10.1103/PhysRevE.84.066106) or [a paywall](https://motherboard.vice.com/en_us/article/a3yxwb/ai-researchers-are-boycotting-natures-new-machine-intelligence-journal).*

Today's paper points out connections between the stochastic block model in network science and various Bayesian reasoning techniques. It's particularly interesting to me because, despite being published in 2011, it uses an adjusted-for-chance measure to gauge performance.

<!--more-->

First off, what's a stochastic block model? And how does it work?

You can get a good idea from how it's parameterized:

- The number of groups, \\(q\\)
- The expected fraction of nodes in each group, \\(\{n_a\}_{a=1}^q\\)
- A \\(q\times{}q\\) affinity matrix \\(P\\), where each entry \\(p_{ab}\\) represents the probability of an edge between nodes in communities \\(a\\) and \\(b\\).
