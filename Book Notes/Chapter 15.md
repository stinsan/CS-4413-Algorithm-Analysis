# Chapter 15: Dynamic Programming

In chapters 2 and 4 we saw the divide-and-conquer method of solving problems. The algorithms involve partitioning the problem into disjoint
subproblems, solving the subproblems recursively, and combining their solutions to solve the original problem. In contrast, dynamic programming applies when the subproblems overlap—that is, when subproblems share subsubproblems. In this context,
a divide-and-conquer algorithm does more work than necessary, repeatedly solving the common subsubproblems.

A **dynamic-programming** algorithm solves each subsubproblem just ojnce and then saves its answer in a table, thereby avoiding the work of recomputing
the answer every time it solves each subsubproblem.

Dynamic programming is typically applied to optimization problems. Such problems have many possible solutions, each having a value. We want the solution with the optimal (minimum or maximum) value.

A dynamic-programming algorithm has four steps:
1. Characterize the structure of an optimal solution.
2. Recursively define the value of an optimal solution.
3. Compute the value of an optimal solution, typically in a bottom-up fashion.
4. Construct an optimal solution from computed information.

# 15.1 | Rod Cutting
Serling Enterprises buys long steel rods and cuts them into shorter rods, which it then sells. Each cut is free. We assume that we know,
for _i = 1, 2, ..._ the price _p<sub>i</sub>_ that Serling charges for a rod of length _i_ inches. Rod lengths are always integer values. Figure 15.1 below shows an example table.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-39.png)

Given a rod length of _n_ inches and a table of prices _p<sub>i</sub>_ for _i = 1, 2, ..., n_, detemine the maximum revenue _r<sub>n</sub>_ obtainable by cutting up the rod and selling the pieces. Note that if the price _p<sub>n</sub>_ for a rod of length _n_ is large enough, an optimal solution may require no cutting at all.

Consider the case when _n = 4_. Figure 15.2 below shows all the ways to cut a 4 inch rod. We see that cutting the rod into two 2-inch pieces produces a revenue of _p<sub>2</sub> + p<sub>2</sub> = 5 + 5 = 10_, which is optimal.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-40.png)

Observe that there are _2<sup>n-1</sup>_ to cut up a rod of length _n_. We denote a decomposition into pieces using ordinary additive notation, so that 7 = 2 + 2 + 3 indicates that a 7-inch rod has been cut into two 2-inch pieces and one 3-ince piece.

If an optimal solution cuts the rod into _k_ pieces, then an optimal decomposition

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_n = i<sub>1</sub> + i<sub>2</sub> + ... +  i<sub>k</sub>_

of the rod into pieces of lengths  i<sub>1</sub>, i<sub>2</sub>, ..., i<sub>k</sub> provides a maximum corresponding revenue

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_r<sub>n</sub> = p<sub>i<sub>1</sub></sub> + p<sub>i<sub>2</sub></sub> + ... +  p<sub>i<sub>k</sub></sub>_

The _r<sub>i</sub>_ for _i_ = 1, 2, ..., 10 is:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-41.png)
