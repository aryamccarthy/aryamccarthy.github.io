---
layout: paper
title: "Overcoming catastrophic forgetting in neural networks"
authors: "Kirkpatrick et al."
year: 2017
venue: PNAS
link: "https://www.pnas.org/content/114/13/3521"
---

When you train a neural network for one task, then train it for another, it usually forgets how to handle the first task. Unfortunately, training on data from a different domain can also cause the network to "catastrophically forget" the first domain. This paper provides a different defense against catastrophic forgetting than [Tuesday's]({{ "/vilar2018learning" | absolute_url }}). As with all good metaphors in neural networks, this one is inspired by the neocortex. They call it **elastic weight consolidation (EWC)**.

<!--more-->

They call it elastic because they attach little springs to each weight after training on the first task, resisting changes from the values learned for that task. Each weight has its own spring of a custom strength. 

Let's justify this by getting a little Bayesian. Bayes's rule is easily googleable, but let's look at it in log-form.

$$ \log p(\theta \mid \mathcal{D}) = \log p(\mathcal{D} \mid \theta) + \log p(\theta) - \log p(\mathcal{D}) $$ 

If we assume that the data \\(\mathcal{D}\\) are split independently into the part for task A and the part for task B, we can manipulate the equation. 

$$ \log p(\theta \mid \mathcal{D}) = \left[\log p\left(\mathcal{D}_A \mid \theta\right) + \log p\left(\mathcal{D}_B \mid \theta\right)\right] + \log p(\theta) - [\log p(\mathcal{D}_A) +  \log p(\mathcal{D}_B)] $$ 

Now apply Bayes's rule again to collect the \\(\mathcal{D}_A\\) terms.

$$ \log p(\theta \mid \mathcal{D}) = \log p(\mathcal{D}_B \mid \theta) + \log p(\theta \mid \mathcal{D}_A) - \log p(\mathcal{D}_B) $$ 

> Note that the left-hand side is still describing the posterior probability of the parameters given the entire dataset, whereas the right-hand side depends only on the loss function for task \\(B\\), \\(\log p(\mathcal{D}_B \mid \theta)\\). All of the information about task A must there- fore have been absorbed into the posterior distribution \\(p(\theta \mid \mathcal{D}_A)\\).

Since the true posterior in a neural network is messy and intractable—think of everything you have to sum over to get the denominator—they use an approximation. They imagine the posterior probability of the parameters as a multivariate Gaussian distribution. Each parameter is the mean of one dimension, and the precision (inverse of the standard deviation squared) is the diagonal of the [Fisher information](https://en.wikipedia.org/wiki/Fisher_information) matrix.

The new loss when training on task \\(B\\) is now penalized by how far the parameters deviate from the optimum on task \\(A\\)—their log-likelihoods according to the multivariate Gaussian we defined above. The \\(\lambda\\) coefficient lets us tweak the strength of the penalty.

$$ \mathcal{L}(\boldsymbol{\theta}) = \mathcal{L}(\boldsymbol{\theta}) + \lambda \sum_i \frac{F_i}{2} (\theta_i - \theta^*_{A, i}) ^2 $$

Plus, this method can easily generalize to a third task:

> 
When moving to a third task, task *C*, EWC will try to keep the network parameters close to the learned parameters of both tasks *A* and *B*. This can be enforced either with two separate penalties or as one by noting that the sum of two quadratic penal- ties is itself a quadratic penalty.

When tracking the signal-to-noise ratio 
