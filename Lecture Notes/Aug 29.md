# Chapter 2: Getting Started (cont.)

## 2.3.1 | The Divide-and-Conquer Approach (cont.)

**Merge Algorithm**:

The key operation of the merge sort algorithm is the merging of two sorted
sequences in the “combine” step. We merge by calling an auxiliary procedure
*MERGE(A, p, q, r)*, where *A* is an array and *p*, *q*, and *r* are indices into the array
such that <br/> p ≤ q < r. The procedure assumes that the subarrays *A[p...q]* and
*A[q + 1...r]* are in sorted order. It merges them to form a single sorted subarray
that replaces the current subarray *A[p...r]*.

- The algorithm:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-2.png)

- A diagram showing the algorithm's funtion:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-5.png)
![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-6.png)

Note that the merge algorithm is _**not**_ the same as the merge-sort algorithm, although it is part of merge-sort.

The time complexity of the merge algorithm is Θ(n).

**Merge Sort**:

- The algorithm:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-3.png)

- A diagram showing the algorithm's function:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-4.png)

The time complexity of merge sort is T(n) = 2T(n/2) + cn = cnlog(n) + cn, which is Θ(nlogn).

So, the time complexity of merge sort is better than the time complexity of insertion sort. So why use insertion sort? Insertion sort has 
the benefit of using constant space complexity (O(1)), whereas merge sort uses linear space complexity (O(n)).

Side note: when it comes to time complexity, log(n) < n<sup>c</sup> for any c > 0.
