# Chapter 22: Elementary Graph Algorithms
## 22.1 | Representations of Graphs
Two standard ways to represent a graph _G = (V, E)_:
- adjacency lists
- adjacency matrices

**Sparse graphs**: |_E_| is much less than |_V_|<sup>2</sup>.
**Dense graphs**: |_E_| is close to |_V_|<sup>2</sup>.

**Adjacency list representation** of a graph _G = (V, E)_ consists of an array _Adj_ of |_V_| lists, one for each vertex in _V_. For each _u_ in _V_, _Adj[u]_ contains all of the vertices adjacent to _u_ in _G_.

If _G_ is a directed graph, the sum of all the lists in an adjacency list representation is |_E_|.
If _G_ is undirected, the sum is 2|_E_|.

For both directed and undirected, the memory that an adjacency list representation takes is Θ (_V + E_).

A disadvantage to adjacency lists is that there does not exist a faster way to determine whether an edge (_u, v_) exists than to search for _v_ in _Adj[u]_.

For the **adjacency matrix representation** of a graph _G_ = (_V, E_), we assume the vertices are numbered 1, 2, ..., |_V_|. Then the adjacency matrix is |_V_| x |_V_| matrix _A_ = (_a<sub>ij </sub>_) such that _a<sub>ij</sub>_ is 1 if (_i, j_) is in _E_. Otherwise, it is 0.

Adjacency matrices have a space complexity of Θ (_V<sup>2</sup>_). Although the adjacency-list representation is asymptotically at least as space efficient as the adjacency-matrix representation, adjacency matrices are simpler,
and so we may prefer them when graphs are reasonably small.

Both adjacency lists and adjacency matrices can be readily adapted to represent **weighted graphs**, graphs
for which each edge has an associated weight, typically given by a weight function.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-59.png)

### Representing Attributes
An attribute _d_ of vertex _v_ will be represented as _v.d_. 

An attribute _f_ of edge (_u, v_) is represented as (_u, v_)._f_.

## 22.2 | Breadth-first Search
Given a graph _G = (_V, E_) and a **source** vertex _s_, breadth-first search explores the edges of _G_ to discover every vertex that is reachable from _s_. It computes the distance (smallest number of edges) from _s_
to each reachable vertex. It also produces a breadth-first tree with root _s_ that
contains all reachable vertices. For any vertex _v_ reachable from _s_, the simple path
in the breadth-first tree from _s_ to _v_ corresponds to a shortest path from _s_ to _v_
in G, that is, a path containing the smallest number of edges.

It is called breadth-first because the algorithm discovers all vertices at distance _k_ from _s_ before discovering any
vertices at distance _k + 1_.

To keep track of progress, breadth-first search colors each vertex white, gray, or
black. A vertex is **discovered** the first time it is encountered during the search, at which time
it becomes nonwhite. All vertices adjacent to black vertices have been
discovered. Gray vertices may have some adjacent white vertices; they represent
the frontier between discovered and undiscovered vertices.

Breadth-first search constructs a breadth-first tree, initially containing only its
root, which is the source vertex _s_. Whenever the search discovers a white vertex _v_
in the course of scanning the adjacency list of an already discovered vertex _u_, the
vertex _v_ and the edge (_u, v_) are added to the tree; we say that _u_ is the **predecessor**
or **parent** of _v_.

The breadth-first-search procedure _BFS_ below assumes that the input graph
_G_ = (_V, E_) is represented using adjacency lists. We store the color of each vertex _u_ in the attribute _u.color_ and
the predecessor of _u_ in the attribute _u.π_. If _u_ has no predecessor, then _u.π_ = _NIL_. The attribute _u.d_ hold the distance from _s_ to _u_. The algorithm also uses a FIFO queue _Q_ to manage the set of gray vertices.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-60.png)

Figure 22.3 illustrates the progress of _BFS_ on a sample graph.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-61.png)

### Analysis
The overhead for initialization is O(_V_), and
thus the total running time of the BFS procedure is O(_V + E_). Thus, breadth-first
search runs in time linear in the size of the adjacency-list representation of _G_.

The following procedure prints out the vertices on a shortest path from _s_ to _v_,
assuming that _BFS_ has already computed a breadth-first tree:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-62.png)

This procedure runs in time linear in the number of vertices in the path printed,
since each recursive call is for a path one vertex shorter.

## 22.3 | Depth-first Search
The strategy followed by depth-first search is to search “deeper” in the graph whenever possible. Depth-first search explores edges out
of the most recently discovered vertex _v_ that still has unexplored edges leaving it.
Once all of _v_ ’s edges have been explored, the search “backtracks” to explore edges
leaving the vertex from which _v_ was discovered. This process continues until we
have discovered all the vertices that are reachable from the original source vertex.
If any undiscovered vertices remain, then depth-first search selects one of them as
a new source, and it repeats the search from that source. The algorithm repeats this
entire process until it has discovered every vertex.

Unlike breadth-first search,
whose predecessor subgraph forms a tree, the predecessor subgraph produced by
a depth-first search may be composed of several trees, because the search may
repeat from multiple sources. Therefore, we define the **predecessor subgraph** of
a depth-first search slightly differently from that of a breadth-first search: we let 
_G<sub>π</sub>_ = (_V, E<sub>π</sub>_ ), where E<sub>π</sub> = {(_v.π , v_) : _v_ ∈ _V_ and _v.π_ ≠ _NIL_}

Depth-first search colors vertices during the search to
indicate their state. Each vertex is initially white, is grayed when it is discovered
in the search, and is blackened when it is finished, that is, when its adjacency list
has been examined completely.

Depth-first search also **timestamps** each vertex. Each vertex _v_ has two timestamps: the first timestamp _v.d_ records when _v_
is first discovered (and grayed), and the second timestamp _v.f_ records when the
search finishes examining _v_ ’s adjacency list (and blackens _v_).

The following pseudocode is the basic depth-first-search algorithm. The variable _time_ is a global variable that
we use for timestamping.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-63.png)

Figure 22.4 illustrates the progress of _DFS_ on the graph shown in Figure 22.2.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-64.png)

The running time of _DFS_ is Θ (_V + E_).
