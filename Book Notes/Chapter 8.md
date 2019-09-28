# Chapter 8: Sorting in Linear Time

## 8.1 | Lower Bounds for Sorting
All the sorts covered previously were comparison sorts. That is, given two elements _a_ and _b_, we perform one of the tests <br/>
_a < b_, _a ≤ b_, _a = b_, _a ≥ b_, or _a > b_ to determine their relative order.

In this section, we assume that all input elements are unique. Given this assumption, comparisons of the for _a = b_ are useless, so we can assume that no comparisons of this form are made. Also note that the comparisons _a ≤ b_, _a < b_, _a ≥ b_, and _a > b_ are all equivalent in that they yield the same information about the ordering of _a_ and _b_. Thus, we can assume that all comparisons have the form _a ≤ b_.

### The Decision-Tree Model:

**Decision Tree**: A full binary tree that represents the comparisons between elements that are performed by a particular sorting algorithm operating on an input of a given size.

Figure 8.1 below is a decision tree showing insertion sort.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-27.png)

In a decision tree, each internal node is annotated by _i : j_ such that _1 ≤ i_ and _j ≤ n_, where _n_ is the number of elements in the input.

Each leaf is a permutation of the input sequence annotated by 〈1, 2, ..., n〉.

Each internal node represents a comparison _a<sub>i</sub> ≤ a<sub>j</sub>_, with the left subtree representing that _a<sub>i</sub> ≤ a<sub>j</sub>_ is true, and with the right subtree representing that _a<sub>i</sub> > a<sub>j</sub>_ is true.

When a leaf is reached, the sorting algorithm has establish the ordering _a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>_.

Since any correct sorting algorithm must produce each permutation of its input sequence, there must be _n!_ leaves representing _n!_ permutations.

### A Lower Bound for the Worst Case:

The length of the longest simple path from the root of a decision tree to any of
its reachable leaves represents the worst-case number of comparisons that the corresponding sorting algorithm performs.

A lower bound on the heights of all decision trees in which each permutation
appears as a reachable leaf is therefore a lower bound on the running time of any
comparison sort algorithm. The following theorem establishes such a lower bound:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-28.png)

## 8.2 | Counting Sort

**Counting sort** assumes that each of the _n_ input elements is an integer in the range 0 to _k_, for some integer _k_. When _k = O(n)_, the sort runs in _Θ(n)_.

Counting sort counts, for some element _x_, the number of elements less than _x_. It then uses this information to put _x_ in the correct position. For example, if there are 17 elements less than _x_, then _x_ belongs in the 18th index.

We must use 3 arrays for counting sort: 
1. _A[1...n]_ is the input array.
2. _B[1...n]_ is the output array.
3. _C[1...k]_ is a temporary, storage array used for work.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-29.png)
