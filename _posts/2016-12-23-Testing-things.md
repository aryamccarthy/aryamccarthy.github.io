---
layout: post
title: A subtle syntax distinction in Python
---

Sophomore year, I thought my professor was archaic for seriously discussing FORTRAN as a language, but Lawrence Livermore National Lab still uses it because the numerical routines written in it have been battle-tested for decades. Python makes things better by wrapping those routines in simple syntax, batteries included. But there are some kinks, too. I determined a subtle and damaging flaw in a major Python library and corrected it.

I'm a contributor to [networkx](https://networkx.readthedocs.io/en/stable/), the most successful graph library for Python. We use Travis for continuous integration (CI), making sure that each submitted change passes all tests before incorporating it into the body of code. And we'd had trouble lately: one function's result was based on random decisions, which meant it could return one of two possible values.

![Build status](https://travis-ci.org/networkx/networkx.svg?branch=master)

It took us a few days of wrongly failing builds to nail down the problem, coming from that one test. We resolved that there were two right answers—two possible partitions of the graph. One split the graph into two components, and the other simply gave one large component.

Originally, the test checked this:

```python
ground_truth = set([frozenset([0, 1, 2, 3, 4, 5, 6, 7]),
                    frozenset([8, 9, 10, 11, 12, 13, 14, 15])])
assert_equal(result, ground_truth)
```

But `ground_truth` wasn't necessarily correct, so we had do incorporate the other possibility. A fix was presented:

```python
assert(result in [ground_truth, set(frozenset(range(16)))])
```

By flipping all its coins the right way, the build passed. But passing wasn't enough. Ten points to whoever already sees the problem.

---

Sets got strapped into Python later in its life. Frozensets are their immutable cousin. Calling `set(frozenset(x))` is consequently the same as just calling `python set(x)`—it's a typecast. Instead, we need `set([frozenset(x)])`—expressing a one-element set—but our syntax is looking rough. The cleanest way is some syntactic sugar introduced in Python 2.7: a set literal. The set literal syntax `{foo}` makes us *less likely to make the mistake* shown above. The easiest way, then, to express what we're after is this:

```python
assert(result in [ground_truth, {frozenset(range(16))}])
```

When I submitted this pull request to the repository, I took out a nasty bug that had mis-marked a number of good PRs as failing. Knowing which builds properly do and don't pass means less time manually sorting that out—the entire point of continuous integration. This means networkx can move forward in a more streamlined, complete way.
