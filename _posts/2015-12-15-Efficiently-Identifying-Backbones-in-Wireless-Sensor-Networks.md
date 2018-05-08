---
layout: post
title: Quickly Finding Reliable Communication Backbones
---

SMU's algorithm engineering class has been facetiously called a "course in computational creativity." This creativity was stretched into graph theory for the class's final project: fast algorithms for graph coloring and finding communication backbones in wireless sensor networks. 

My implementation of the smallest-last ordering for greedy coloring was [my first contribution](https://github.com/networkx/networkx/commit/17b8d21f7edd4ec4388ba9bd52acb3a91d6ef9e2) to Python's [networkx](https://networkx.readthedocs.io/en/stable/) graph library.

With the increasing prevalence of IoT devices and Bluetooth beacons, finding reliable communication pathways is becoming a critical problem. Interference, contention, and routing each become complicated problems when wireless sensors are randomly distributed. This motivates the investigation of communication backbones which can serve as trunk lines for the communication.

![trunk line](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Map_of_Proposed_American_Radio_Relay_League_Trunk_Lines_from_Page_21_of_the_February_1916_Issue_of_QST.png/1024px-Map_of_Proposed_American_Radio_Relay_League_Trunk_Lines_from_Page_21_of_the_February_1916_Issue_of_QST.png)
*Large-scale trunk lines for communicating in the USA*

A model of the wireless sensor network is the [random geometric graph](https://en.wikipedia.org/wiki/Random_geometric_graph) (RGG). Nodes in the graph are connected if they are within a given radius *r*, which meshes with our intuitive understanding of wireless signal range. A really approachable primer on wireless sensor networks and RGGs is [here](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3292077/).

A minimal (cheap) backbone communicates with as many nodes as possible, while including as few nodes as possible. A trick for finding the backbone is using the [graph coloring](https://en.wikipedia.org/wiki/Graph_coloring)—putting the nodes into as few buckets as possible, with no adjacent nodes in the same bucket. The buckets are [independent sets](https://en.wikipedia.org/wiki/Independent_set_(graph_theory)). A single independent set in an RGG tries to cover as much of the space as possible, without letting the nodes communicate. Merging two independent sets lets them serve as relays for one another. 

![]({{ site.baseurl }}/images/simplegraph50.png)
*Nodes marked in red form the backbone with the greatest coverage, and black edges connect the backbone. The red edges connect a single node to all of its neighbors.*

While graph coloring is an NP-complete problem, numerous heuristics have been proposed. My thesis advisor, [David W. Matula](https://www.smu.edu/Lyle/Departments/CSE/People/Faculty/MatulaDavid), presented the [smallest-last ordering](http://dl.acm.org/citation.cfm?id=322385). It repeatedly removes a node of least degree until the graph is empty. Along the way, you wind up with a terminal clique: every node left has the same degree, because they're all connected to one another. The graph will need at least as many colors as the terminal clique size.

![]({{ site.baseurl }}/images/ordering50.png)
*The terminal clique is discernible at the far left of the graph, where the slope is consistent.*

Along the way, I learned some pretty cool tricks for speeding up the implementation:

- [Fast random point generation on a sphere](http://mathworld.wolfram.com/SpherePointPicking.html)—avoids rejection sampling (which is not guaranteed to terminate) and transcendental functions. It produces a 25% speedup over the next best method.
- [*k*-d trees](https://docs.scipy.org/doc/scipy-0.14.0/reference/generated/scipy.spatial.KDTree.html) for quickly determining the edges present in a random geometric graph. It beats the *O*(*n*^2) brute-force algorithm.
- Speeding up the smallest-last ordering by using a [bucket queue](https://en.wikipedia.org/wiki/Bucket_queue) data structure optimized by tracking the lower bound on degree. The naive algorithm is *O*(*n*^2); this is *O*(*n*+*m*). I added my to `networkx`, so I anticipate seeing it show up in future students' projects without attribution. *Shrug.*
- Computing faces on the sphere using the [Euler characteristic](https://en.wikipedia.org/wiki/Euler_characteristic), instead of by counting.

My full writeup for the project is [here](https://raw.github.com/aryamccarthy/WirelessSensorNetwork/blob/master/docs/Linear%20Algorithms%20for%20Wireless%20Sensor%20Networks.pdf), and the code is [here](https://github.com/aryamccarthy/WirelessSensorNetwork).
