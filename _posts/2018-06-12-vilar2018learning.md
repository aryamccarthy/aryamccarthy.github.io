---
layout: paper
title: "Learning Hidden Unit Contribution for Adapting Neural Machine Translation Models"
author: Vilar
year: 2018
venue: NAACL
link: "http://www.aclweb.org/anthology/N18-2080"
---

This NAACL paper seeks to perform domain adaptation while learning only a few model parameters. It does this by learning to amplify or diminish the values coming from hidden nodes (their **contributions**), thus the paper title: "Learning Hidden Unit Contribution". This is useful when you have a lot of out-of-domain text to train with, but very little in-domain text.

<!--more-->

Training is done in two phases.

1. Train a normal NMT model on your big out-of-domain corpus.
2. Freeze the parameters of the network. Introduce a scaling unit after each hidden unit. Only learn the scaling factors \\(\rho\\)—one parameter for each hidden unit. The \\(\rho\\) parameters are sigmoided to squash them to the range (0, 1), then doubled. (In Vilar's notation, the function \\(\alpha\\) does this squashing and doubling.)

These are only applied to the activation function outputs of the hidden layers. It doesn't make sense to apply it to, say, the embeddings, because they're not squashed.

What's the advantage of this, though? Why bother with this over normal continued training? Because it converges slightly faster. And it gets you maybe one BLEU point over normal continued training.
