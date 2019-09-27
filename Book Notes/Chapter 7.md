# Chapter 7: Quicksort

## 7.1 | Description of Quicksort
Quicksort, like merge sort, applies the divide-and-conquer paradigm. Here is the three-step divide-and-conquer process for sorting a
typical subarray _A[p...r]:

1. **Divide**: Partition the array _A[p...r]_ into two (possibly empty) subarrays _A[p...q - 1]_ and _A[q + 1...r]_ such that each element of _A[p...q - 1]_ is less than or equal to _A[q]_, which is, in turn, less than or equal to each element of _A[q + 1...r]_. Compute the index _q_ as part of this partitioning procedure.

2. **Conquer**: Sort the two subarrays _A[p...q - 1]_ and _A[q + 1...r]_ by recursive calls to quicksort.

3. **Combine**: Because the subarrays are already sorted, no work is needed to combine them: the entire array _A[p...r]_ is now sorted.

The following procedure implements quicksort:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-21.png)

**Partitioning the Array**:

The running time of the partition procedure on the subarray _A[p...r]_ is Ѳ(_n_), where _n = r - p + 1_.
![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-22.png)

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-23.png)

## 7.2 | Performance of Quicksort

The running time of quicksort depends on whether the partitioning is balanced or unbalanced. If the partitioning is balanced, the algorithm runs asymptotically as fast as merge sort; if the partitioning is unbalanced, the algorithm runs asymptotically as slowly as insertion sort.

**Worst-case Partitioning**:

