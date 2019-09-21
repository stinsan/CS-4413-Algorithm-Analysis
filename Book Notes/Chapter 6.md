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

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-12.png)

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-13.png)

*Build-Max-Heap* takes O(n) time complexity.

## 6.4 | The Heapsort Algorithm

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-14.png)

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-15.png)

Heapsort takes _O(n lg n)_ because Build-Max-Heap() takes _O(n)_ and each of the n - 1 calls to Max-Heapify() takes _O(lg n)_.

## 6.5 | Priority Queue

A **priority queue** is a data structure for maintaining a set _S_ of elements each with an associated value called a **key**.

A **max-priority queue** supports the following operations:
- *Insert(S, x)*: inserts the element *x* into the set *S*, which is equivalent to the operation *S = S ⋃ {x}*.
- *Maximum(S)*: returns the element of *S* with the largest key.
- *Extract-Max(S)*: removes and returns the element of *S* with the largest key.
- *Increase-Key(S, x, k)*: increases the value of element *x*'s key to the new value *k*, which is assumed to be at least as large as *x*'s current key value.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-16.png)

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-17.png)

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-18.png)

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-20.png)

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-19.png)

