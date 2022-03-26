---
layout: paper
title: "Interpolating between types and tokens by estimating power-law generators"
author: "Goldwater, Griffiths, and Johnson"
year: 2006
venue: NIPS
link: "http://papers.nips.cc/paper/2941-interpolating-between-types-and-tokens-by-estimating-power-law-generators.pdf"
---

Your statistical model is trained under the assumption that its training distribution matches the testing distribution. If you want to learn from type-level data like a dictionary or gazetteer, it's not as simple as appending those to your training data; it skews the distribution. In natural language, words occur with a power-law (Zipfian) distribution. We should have generators that match this. The authors make this by augmenting their generator with a frequency **adaptor**.

<!--more-->

---

We resort to a two-stage language model:

1. A generator, which produces words (perhaps a uniform multinomial distribution)
2. An adaptor, which governs their frequency.

Our adaptor of choice is the Pitman–Yor process (PYP), which generalizes the Chinese restaurant process. It's a way of seating people at tables (or adding new ones) where there's a preference toward tables which are already crowded. The tables are infinitely expandable; they represent some label or class. The probability of being seated at a given table (put in a given class \\(k\\)) is gnarly:

$$
\Pr(z_i=k \mid \mathbf{z}_{<i}) = 
\begin{cases} 
      0 & x\leq 0 \\
      \frac{100-x}{100} & 0\leq x\leq 100 \\
      0 & 100\leq x 
   \end{cases}
$$

And what's worse: it feeds into a bigger equation for the probability of the \\(i\\)th word, since the labels of the tables are not fixed.

$$
\begin{align}
\Pr(w_i = w \mid \mathbf{w}_{<i}, \mathbf{z}_{<I}, \theta)
 &= \sum_k \sum_{\ell_k} \Pr(w_i = w \mid z_i - k, \ell_k) \Pr(\ell_k \mid \mathbf{w}_{<i}, \mathbf{z}_{<I}, \theta) \Pr(z_i=k \mid \mathbf{z}_{<i})\\
  &= \sum_k \sum_{\ell_k} [w_i =  \ell_k] \Pr(\ell_k \mid \mathbf{w}_{<i}, \mathbf{z}_{<I}, \theta) \Pr(z_i=k \mid \mathbf{z}_{<i})\\
&= \sum_{k=1}^{K(\mathbf{z}_{<i})} \frac{n_k^{\mathbf{z}_{<i}}-a}{i - 1 + b} [w = \ell_k] + \frac{K(\mathbf{z}_{<i})a + b}{i - 1 + b}\theta_w
\end{align}
$$
Here, \\(\theta\\) is the parameter for our multinomial distribution. \\(K\\) is the number of tables so far. \\(n_k^{\mathbf{z}_{<I}}\\) is the number of people at table \\(k\\) so far. \\(a\\) and \\(b\\) control the power law's intensity and the preference toward new tables, respectively.

From this, you can get the probability of a *sequence* of words by summing over all category values \\(\mathbf{z}\\) and table labelings \\(\boldsymbol{\ell}\\).

---

When \\(a\\) approaches 1, the probability of a new table for a token drops to zero—every token gets its own table. Approaching 0 instead gives a type-based system. "The sum is dominated by the seating arrangement that minimizes the total number of tables...in which every word type receives a single table."

To test their model, the authors use essentially a toy task: English verb segmentation into stem and affix. While they don't compare to a baseline, they show that whether evaluating on types or tokens, low values of \\(a\\) helped—a preference toward types.
