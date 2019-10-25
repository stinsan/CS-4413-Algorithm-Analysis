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

Huffman codes provide an effective way to compress data. Huffman’s greedy algorithm uses a table giving
how often each character occurs (i.e., its frequency) to build up an optimal way of
representing each character as a binary string.

Suppose we have a 100,000-character data file that we wish to store compactly.
We observe that the characters in the file occur with the frequencies given by Figure 16.3. 

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-55.png)

Here, we consider the problem of designing a **binary character code** in which each character is represented by a unique binary string, which we call a **codeword**. If we use a **fixed-length code**, we need 3 bits to represent 6 characters:
_a_ = 000, _b_ = 001, ..., _f_ = 101. This method requires 300,000 bits to code the entire file. However, a **variable-length code** can do considerably better than a fixed-length code, by giving frequent characters short codewords and infrequent characters long codewords.
For our example, this code requires 224,000 bits, a 25% improvement.

### Prefix Codes
For this to work, it must be that no codeword is also a prefix of some other codeword. Such codes are called **prefix codes**. To encode a string, we just concatenate the codewords representing each character of the file. 

For example, with the variable-length prefix code of Figure 16.3, we code the 3-character file _abc_ as 0·101·100 =
0101100, where “·” denotes concatenation.

Prefix codes are desirable because they simplify decoding. Since no codeword is a prefix of any other, the codewords in an encoded file are unambigous.

We represent the decoding process with the use of a binary tree whose leaves are the given characters. The binary codeword for a character is a simple path from the root to the character where 0 means to "go to the left child" and 1 means "go to the right child."
Figure 16.4 shows the trees for the two codes of our example.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-56.png)

An optimal code for a file is always represented by a full binary tree, in which
every nonleaf node has two children. The tree for the fixed-length code in Figure 16.4a is not optimal since it is not a full binary tree.

### Constructing a Huffman Code
In the pseudocode that follows, we assume that _C_ is a set of _n_ characters and
that each character _c ∈ C_ is an object with an attribute _c.freq_ giving its frequency. The algorithm builds the tree T corresponding to the optimal code in a bottom-up manner.  The algorithm uses a min-priority
queue _Q_, keyed on the _freq_ attribute, to identify the two least-frequent objects to
merge together. When we merge two objects, the result is a new object whose
frequency is the sum of the frequencies of the two objects that were merged.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-57.png)

For our example, Huffman’s algorithm proceeds as shown in Figure 16.5.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-58.png)

The total running time of Huffman Code algorithm on a set of _n_ characters is O(n lg n).

