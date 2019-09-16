# Chapter 6: Heapsort
## 6.1 | Heaps

**Heaps** are data structures that can be visualized as both either a tree or an array. The tree is completely full except for the lowest
level, which is filled in left to right.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-9.png)

**Max-Heaps** are where the value of the root node is less than or equal to either of the child nodes. <br/>
**Min-Heaps** are where the value of the root node is greater than or equal to either of the child nodes.

## 6.2 | Maintaining the Heap Property

In order to maintain the max-heap property, there is the **Max-Heapify** algorithm:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-10.png)

Essentially, this algorithm works by "floating down" the node with a smaller value than its children so that the max-heap property is
maintained.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-11.png)

The runtime of the Max-Heapify algorithm is T(n) = T(2n/3) + Θ(1).

This can be simplified to T(n) = O(lg n) by case 2 of the Master Theorem.

This can be even more simplified to O(h), where h is the height of the max-heap tree.

## 6.3 | Building a Heap
