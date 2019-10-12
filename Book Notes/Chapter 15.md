# Chapter 15: Dynamic Programming

In chapters 2 and 4 we saw the divide-and-conquer method of solving problems. The algorithms involve partitioning the problem into disjoint
subproblems, solving the subproblems recursively, and combining their solutions to solve the original problem. In contrast, dynamic programming applies when the subproblems overlap—that is, when subproblems share subsubproblems. In this context,
a divide-and-conquer algorithm does more work than necessary, repeatedly solving the common subsubproblems.

A **dynamic-programming** algorithm solves each subsubproblem just ojnce and then saves its answer in a table, thereby avoiding the work of recomputing
the answer every time it solves each subsubproblem.
