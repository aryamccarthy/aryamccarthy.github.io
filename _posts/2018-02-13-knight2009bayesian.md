---
title: "Bayesian Inference with Tears"
layout: post
excerpt_separator: <!--more-->
---

([Knight 2009](https://www.isi.edu/natural-language/people/bayes-with-tears.pdf))

Kevin Knight describes a very real phenomenon for a first-year grad student: everyone is throwing out expressions like "Integrate over the possible values" or "Don't you see how this is a generative model?" and you want to quit school to move to the woods of North Carolina and bagpipe on the side of a hill. When the Bayesian craze struck, Knight had to work and avoid being left behind, so he wrote a workbook to teach others. 

<!--more-->

First off: Why do we want Bayesian things? Because they promise compact models and small steps.

The first motivating example is probabilistic tree substitution grammars. These can be used to generate strings starting from a root token S, just like with [probabilistic context-free grammars](https://en.wikipedia.org/wiki/Probabilistic_context-free_grammar) (PCFGs), except that we expand each nonteriminal with a weighted choice among trees, rather than just sequences of tokens. The best string is **argmax\_(derivations which yield the string _s_) P(_deriv_) = PROD\_{_r_ for _r_ in _deriv_} P(_rule_ \| root(_r_))**. That is to say, we compute the product of the weighted choices that generated our surface form **_s_**. One tree can come from multiple derivations, so how about instead **argmax\_(trees which yield the string _s_)  SUM\_{ _deriv_ in _tree_ } P(_deriv_) = PROD\_{ _r_ for _r_ in _deriv_ } P(_rule_ \| root(_r_))**. We can now pick the most probable grammar given the treebank that we intend to produce. This is when EM can shine—except it can't. EM creates a huge matrix of rules and derivations, so you'll run out of memory. Even if it didn't, what's to stop EM from saying, "You get one rule to generate each entire sentence from the root! Hooray!"? The answer: nothing. It will do exactly that. This beats out learning either CFG rules or appropriately expressive TSG rules.

We want three things in our model: re-use of rules, compact model sze, and good likelihood. EM fails at re-use. It's not EM's fault. It's ours. We made a bad generative model, and EM just optimized it.

So what do we do? We change our generative story. Instead of P(rule \| rule->root), we use P(rule \| rule->root, context). Our context will be the counts of the rules used so far. The history of used rules becomes a cache. We compute P(rule \| rule->root, context) as count(rule in cache) / sum\_(other rules with same root) count(other rule in cache). Think of this as a weighted selection from your `collections.Counter`. This is a rich-get-richer, accumulative advantage scenario.

So how do we make this Bayesian? We incorporate a base probability, the one we had before this caching and counting nonsense. We also incorporate a hyperparameter beta. With probability beta, we'll use the base distribution. With probability (1-beta), we'll use the cache.

So what's the base distribution? We need a TSG already to decide it. So we generate new rules by sampling. 

```
def generate_TSG_rule(symbol):
    with probability d, quit
    with probability (1-d):
    	pick a number of children from a Poisson distribution, mean lambda
    	pick the identities of the children from a uniform distribution over symbols
    	for child in children:
    		generate_TSG_rule(symbol)
    return updated tree
```

And how do we pick d and lambda? "They can be anything you want! Ha, ha." Christ, I thought we were scientists, not wizards.

We can also bias our distribution toward using the cache over time. Instead of beta, use (alpha / (alpha + H)). H is the number of times the nonterminal rule->root has been expanded. Now we can just simplify our rule into a weighted sum over a denominator. Doing a little more algebra (an exercise to Knight's readers, which is eighth-grade math) shows that this amounts to a Chinese Restaurant Process. We have different restaurants for each nonterminal we wish to expand.

And at this point, quite uncomfortably, we're done. There's nothing to fit. We can't make P0 better, and optimizing the other parameters on a huge treebank is...wasteful?

Anyway, we can now answer the following questions using our newly Bayesian p(rule \| rule->root, cache):

1. Which derivations produce the observed Treebank? What are their derivation probabilities according to the cache model? (Given a derivation, we can get its probability by mechanically applying our boxed formula to it.)
2. What is the sum of probabilities of all derivations? (What is p(Treebank)?)
3. Which derivation has highest probability? (The Viterbi derivation.)
4. Given all derivations, what are the expected counts of all TSG rules?


---

Now let's look at add-one smoothing. Here, we use the "boxed formula" again, deciding that our base distribution will be uniform over all tags and we just keep using that cache model. Turns out (and again, you can work through the workbook with eighth-grade math) add-lambda smoothing is the same CRP, with different alphas.

---

Eventually we get to Gibbs sampling. (Yeah, I'm getting briefer with this. It's already a very casual document.) The idea is that we stumble drunkenly, making weighted choices about changing each part. "Note that the small change is user-defined and problem-specific. This is annoying. Plain EM doesn’t require so much of your personal involvement."

Fortunately, the analogies presented make it easy to see how you could incrementally update your computed probabilities when you move around the space through Gibbs sampling.

We also get a nice summary of annealing, which Knight refers to as one of many black magics: "Another black magic sampling idea is annealing. When choosing the next sample by weighted coin flip, we can cube-root all the P(derivation) values. That will make for a flatter distribution. For example, instead of 0.008 versus 0.027 (a roughly 25/75 coin flip), we’d have 0.2 versus 0.3 (a 40/60 coin flip). The sampler will effectively wander around even more drunkenly and maybe hit regions it would accidentally overlook otherwise. As iterations proceed, we 'sober up' and start square-rooting instead of cube-rooting, and finally we stop rooting altogether."

> The question of how to set α’s and β’s always comes up in this sort of work. It seems reasonable and practical to set them in order to optimize some end-to-end task accuracy. Bayesian people look at you sadly when you suggest this. They will tell you to embrace your uncertainty about what values α and β should take on, and reason under that uncertainty. For example, the distribution of α’s values can be captured by a Gaussian distribution. Instead of choosing a specific value for α, we need only specify a mean (μ) and standard deviation (σ) for its distribution, and sample from that. Haven’t we just replaced α with μ and σ? Yes, it’s turtles all the way down.
>
> Step 7 says “if desired”. That brings up the whole question of what we are learning. Of course, you and I want to learn things like P(NN \| VB) = 0.32, so that we can tag new sentences with the Viterbi algorithm. But be careful saying that out loud. Bayesian people will get sad, or possibly go berserk. They will say, we want to learn a distribution over possible values that P(NN \| VB) might take. Yeah! Then when we tag new sentences, we do it keeping that whole distribution in mind. Yeah!

TL;DR it's a very different mindset, and it's turtles all the way down. You mask your uncertainty about some variables by expressing them as depending on others, "turtles all the way down". And you'll always ask about how to set other parameters that get generated. Don't. Quit asking. Lastly, understand how Chinese Restaurant Processes (the "boxed equation") are everything.
