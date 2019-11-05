# Chapter 23: Minimum Spanning Trees

The **minimum spanning tree** problem: Given an undirected graph _G_ = (_V, E_), each edge (_u, v_) ∈ _E_ has a weight _w_(_u, v_) specifying the cost to connect _u_ and _v_. We then wish to find an acyclic subset _T_ ⊆ _E_ that connects all of the vertices and whose total weight is minimized.

There are two algorithms to make a minimum spanning tree: **Kruskal's** and **Prim's**. Both are greedy algorithms.

## 23.1 | Growing a Minimum Spanning Tree
Assume that we have an undirected graph _G_ = (_V, E_) and a weight _w_ for each edge ∈ _E_. We wish to find the minimum spanning tree for _G_. A generic way to grow a minimum spanning tree is to manage a set of edges _A_ by maintaining the following loop invariant: Prior to each iteration, _A_ is a subset of some minimum spanning tree.

At each step, we determine an edge (_u_, _v_) that we can add to _A_ without violating
this invariant.  We call such an edge a **safe edge** for _A_, since we can add it safely to _A_ while
maintaining the invariant.

### Definitions 
- A **cut** (_S_, _V - S_) of an undirected graph _G_ = (_V, E_) is a partition of _V_. . Figure 23.2 illustrates this notion.<br/>
- We say that an edge _E_ ∈ (_u, v_) **crosses** a cut (_S_, _V - S_) if one of its endpoints is in _S_ and the other is in _V_.<br/>
- We say that a cut **respects** a set _A_ of edges if no edge in _A_ crosses the cut.<br/>
- An edge is a **light edge** crossing a cut if its weight is the minimum of any edge
crossing the cut. Note that there can be more than one light edge crossing a cut in
the case of ties.

### Theorem 23.1
