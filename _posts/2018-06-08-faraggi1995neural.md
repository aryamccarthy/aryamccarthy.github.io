---
layout: paper
title: "A Neural Network Model for Survival Data"
authors: Faraggi and Simon
year: 1995
venue: "Statistics in Medicine"
link: "https://onlinelibrary.wiley.com/doi/pdf/10.1002/sim.4780140108"
---



<!--more-->

Predicting survival is always fun, because the data is right-censored: once the study ends, you don't actually know when the survivors die. A common model for this is the Cox proportional hazards model, which is log-linear. 

The authors are using neural networks for regression—the network has a single output node. The one-layer perceptron they use has a simple architecture: input, hidden nodes plus a bias node, and output. They use a sigmoid nonlinearity between the input and hidden nodes, but not into the output nodes. (The target value is not confined to a fixed range, so a squashing function like sigmoid would make it impossible to match the target variable.)

That bias node in the hidden layer isn't needed after all in this model, because the Cox model has a 'baseline hazard' to keep everything normalized.

The network is applied to the Cox proportional hazards model, governed by a **hazard function**: the instantaneous probability of death, given that you've survived to this moment. 

$$ h(t, \mathbf{x}_i) = h_0(t) \exp\{\boldsymbol{\beta} \mathbf{x}_i\} $$

We can replace the linear scoring function \\(\boldsymbol{\beta} \mathbf{x}_i\\) with a neural network: \\(g(\mathbf{x}_i; \theta) \\). 

Finally, train the network by maximizing the conditional log-likelihood, with an L2 penalty on the network weights.

It's not abundantly clear in the paper how to perform inference (how to predict) with the model. The hazard function is doubly parameterized: the 'covariates' and time. I'm sure there's some kind of calculus here, looking for an inflection point in time. 

**Big takeaway:** when you see a linear combination in your model, why not make it a nonlinear combination? 
