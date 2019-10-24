# Chapter 16: Greedy Algorithms
For many optimization problems, using dynamic programming to determine the best choices is overkill; simpler, more efficient algorithms will do. A **greedy algorithm** always makes the choice that looks best at the moment. That is, it makes a locally optimal choice in the hope that this choice will lead to a globally optimal solution.

## 16.1 | An Activity-Selection Problem
We did not cover this section in lecture.

## 16.2 | Elements of the Greedy Strategy

At each decision point, a greedy algorithm makes the choice that seems best at the moment.

We design greedy algorithms according to the following sequence
of steps:
1. Cast the optimization problem as one in which we make a choice and are left
with one subproblem to solve.
2. Prove that there is always an optimal solution to the original problem that makes
the greedy choice, so that the greedy choice is always safe.
3. Demonstrate optimal substructure by showing that, having made the greedy
choice, what remains is a subproblem with the property that if we combine an
optimal solution to the subproblem with the greedy choice we have made, we
arrive at an optimal solution to the original problem.

### Greedy-choice Property
In dynamic programming, we make a choice at each step, but the choice usually depends on the solutions to subproblems. As a result, we usually solve dynamic programming problems in a bottom-up manner, from smaller subproblems to larger ones.

In a greedy algorithm, we make whatever choice
seems best at the moment and then solve the subproblem that remains. The choice
made by a greedy algorithm may depend on choices so far, but it cannot depend on
any future choices or on the solutions to subproblems. A greedy strategy usually
progresses in a top-down fashion, making one greedy choice after another, reducing each given problem instance to a smaller one.

### Optimal Substructure
A problem exhibits **optimal substructure** if an optimal solution to the problem contains within it optimal solutions to subproblems.
This property is a key ingredient of assessing the applicability of dynamic programming as well as greedy
algorithms. 

### Greedy Versus Dynamic Programming
You might be tempted to generate a dynamic-programming solution to a
problem when a greedy solution suffices or, conversely, you might mistakenly think
that a greedy solution works when in fact a dynamic-programming solution is required. To illustrate the subtleties between the two techniques, let us investigate
two variants of a classical optimization problem

The **0-1 knapsack problem** is as follows. A thief robbing a store finds _n_ items. The _i_ th item is worth _v<sub>i</sub>_ dollars and weights _w<sub>i</sub>_ pounds, where _v<sub>i</sub>_ and _w<sub>i</sub>_ are integrers. The thief wants to take as valuable a load as possible, but he can carry at most _W_ pounds in his knapsack, for some integer _W_. The thief is not allowed to take a fractional amount of an item.

The **fractional knapsack problem** is the same, except the thief can now take fractions of an item.

Both knapsack problems exhibit the optimal-substructure property. If an item is removed from the thief's knapsack, that will still be an optimal solution just with different constraints.

Although the problems are similar, we can solve the fractional knapsack problem
by a greedy strategy, but we cannot solve the 0-1 problem. The fractional knapsack problem is solved by computing the value per pound _v<sub>i</sub> / w<sub>i</sub>_ for each item. Then, the thief steals as much as possible of the item with the greatest value per pound.
After exhausting that item, he moves on to the item with the second greatest value per pound, and so on, until he reaches his weight limit _W_.

To see that this greedy strategy does not work for the 0-1 knapsack problem,
consider the problem instance illustrated in Figure 16a. The value per pound of item 1 is
6 dollars per pound, which is greater than the value per pound of either item 2 (5
dollars per pound) or item 3 (4 dollars per pound). The greedy strategy, therefore,
would take item 1 first. As you can see from the case analysis in Figure 16.2(b),
however, the optimal solution takes items 2 and 3, leaving item 1 behind. The two
possible solutions that take item 1 are both suboptimal.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-54.png)

## 16.3 | Huffman Codes



