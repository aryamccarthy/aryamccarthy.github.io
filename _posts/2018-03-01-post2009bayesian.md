---
layout: paper
title: "Bayesian Learning of a Tree Substitution Grammar"
authors: "Post and Gildea"
year: 2009
venue: "ACL-IJCNLP"
link: "http://www.aclweb.org/anthology/P09-2012"
---

We're getting super Bayesian today. If you're not ready, check out [Kevin Knight's tutorial]({{ "/knight2009bayesian" | absolute_url }}) on Bayesian statistics for NLP. In fact, his paper specifically talks about how to learn tree substitution grammars. (What does it mean to *learn* a grammar? We assume that we already have the derivation rules, and we want to learn their relative chances of being used given the context.) This paper tackles it from a more concrete angle, mixing **Gibbs sampling** to deal with the complexity of the space and **nonparametric priors** to address overfitting.

TSGs are an improvement on context-free grammars. Instead of extending a node with other nodes, you can extend it with a whole subtree, giving structure. This makes parsing in TSGs NP-hard.

The authors extracted grammar rules following the methodology of another paper. They also applied a Dirichlet prior—the non-cache part of the Knight paper.

They get around the NP-hardness by sampling with a collapsed Gibbs sampler. Their results are...alright. "They substantially outperform heuristically extracted grammars from previous work as well as our novel spinal grammar, and can do so with many fewer rules." I still think the bigger contribution here was making the task Bayesian. Unfortunately, it's easy to get caught up in the Bayesian wave. NLP seems to go through fads. Bayesian was the last one, and fortunately it's easily integrated into the current one (neural networks, and more specifically variational methods). 
