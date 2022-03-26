---
layout: post
title: Two thoughts on group theory
---

Each semester, I work through one or two textbooks. I've just picked up Dummit and Foote's _Abstract Algebra_ and begun chapter 1. (Weirdly, my math degree never introduced me to abstract algebra.) Two thoughts come to mind.

## Faces, vertices, edges

First, I had a different route for solving Section 1.2's problem 10 than the two suggested in the book. It's not a particularly involved, problem, but it's still interesting.

The question asks:

> (10.) Let $G$ be the group of rigid motions in $\mathbb{R}^3$ of a cube. Show that $|G| = 24$.

The advice given is:

> [F]ind the number of positions to which an adjacent pair of vertices can be sent. Alternatively, you can find the number of places to which a given face may be sent and, once a face is fixed, the number of positions to which a vertex on that face may be sent.

It's worthwhile to see that there are actually three natural perspectives here, not just two. I've included my third one at the end.

1. **The vertex perspective.** We can consider the vertices, as suggested. Consider adjacent vertices $i$ and $j$. Their motion will totally determine all other positions. The first vertex $i$ can be sent to 8 possible positions—the 8 vertices, including its initial position. The other vertex $j$ can then move to any of the 3 vertices adjacent to the repositioned $i$. No flips are possible, after all—rigid motions only. There are 8 repositionings of the vertex, with 3 corresponding rotations each. $|G| = 8 \times 3 = 24$.
2. **The face perspective.** Similarly, consider a given face $f$ and incident vertex $v$. Move $f$ to any of the possible faces, of which 6 exist (including its initial position). To remain incident, $v$ can be in any of 4 positions. Thus there are 6 possible repositionings and 4 rotations. $|G| = 6 \times 4 = 24$.
3. **The edge perspective.** This one was more natural to me. Consider any edge $\{u, v\}$ in the cube. It can be moved to any of the 12 edges' initial positions, including its starting point. There are two orientations of this edge, though: placing $u$ and $v$ in different positions. $|G| = 12 \times 2 = 24$.

Of course, these should—and do—all lead to the same answer.

## Finding a cycle decomposition

There's an intro algorithms connection to cycle decomposition which I thought worth sharing.

Cycle decompositions can be found with an algorithm provided in the book, which they (naturally) call the **Cycle Decomposition Algorithm**. Not stated in the book, these cycles are really strongly connected components of the graph. But because each must form a cycle, we don't need to use an algorithm for strongly connected components. The weakly connected components (WCC) are necessarily strongly connected. We can use a simpler, cheaper algorithm to find the strongly connected components of a graph with this structure—not everything is a nail that need's, e.g., a Kosaraju's algorithm hammer.
Here's a WCC algorithm, defined in the vocabulary of abstract algebra.

Excerpted below:

```python
S_13: Permutation = {
    1: 12, 2: 13, 3: 3,  4: 1, 5: 11, 6: 9,
    7: 5,  8: 10, 9: 6, 10: 4, 11: 7, 12: 8,
    13: 2,
}  # An example permutation of Ω defined in the book.

decomp = wcc_cycle_decomposition(S_13)
print(format_nicely(decomp))
# (1 12 8 10 4) (2 13) (5 11 7) (6 9)
```

Full code:

{% gist 2ce71471df74ab1262eb42fd21e6593b %}

[1]: https://en.wikipedia.org/wiki/Kosaraju's_algorithm