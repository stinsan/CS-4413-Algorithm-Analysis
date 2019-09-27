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

The worst-case for quicksort occurs when the array is partitioned into one subarray with _n - 1_ elements and another with 0 elements.
Let us assume that this unbalanced partitioning occurs in every recursive call. The partitioning algorithm takes Θ(_n_) time. Since the recursive call of an array of size 0 just returns, T(0) = Θ(1). Thus, the recurrence of the running time is <br/>
<br/>
_T(n) = T(n - 1) + T(0) + Θ(n)_<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_= T(n - 1) + Θ(n)_<br/>.
<br/>
This has the solution _T(n) = Θ(n<sup>2</sup>)_, by the substitution method.

The Θ(n<sup>2</sup>) run time for quicksort occurs when the input array is already pre-sorted; this is a common situation in which insertion sort will perform better than quicksort. Insertion sort on a pre-sorted array runs in _O(n)_.

**Best-case Partitioning**:

The best-case for quicksort occurs when the array is partitioned as evenly as possible. One array will have size of _floor(n/2)_ and the other will have size of _ceil(n/2) - 1_. The recurrence for this case would be <br/>
<br/>
_T(n) = 2T(n/2) + Θ(n)_,<br/>
<br/>
where sloppiness from _floor()_, _ceil()_, and subtracting by 1 is tolerated. By the master's theorem, this recurrence has the solution _T(n) = Θ(n lg n)_.

**Balanced Partitioning**:

Suppose the partitioning algorithm produces a 9-to-1 proportional split. We then obtain the recurrence<br/>
<br/>
_T(n) = T(9n/10) + T(n/10) + cn_<br/>
<br/>
for the running time of quicksort, where the constant _c_ is explicitly shown for the _Θ(n)_ term.

Figure 7.4 below shows the recursion tree for this recurrence:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-24.png)

Notice that every level of the tree has cost _cn_ until the recursion reaches a boundary condition at _log<sub>10</sub> n = Θ(lg n)_, and then the level have a cost of less than or equal to _cn_. The recursion fully terminates at depth _log<sub>10/9</sub> n = Θ(lg n)_.
Thus, the total cost of quicksort is _O(n lg n)_.

Even though it is partitioned in a 9-1 split, quicksort still runs at _O(n lg n)_; a 99-1 split would still also yield _O(n lg n)_.
In fact, any split of constant proportionality yields a recursion tree of depth _Θ(lg n)_, where each level is _O(n)_. Thus, quicksort has a running time of _O(n lg n)_ for a split with constant proportionality.

**Intuition for the Average Case**:

Quicksort is random; some partitions will be good and others will be bad. In the average case, however, there's a mix of good and bad splits. For the sake of intuition, suppose that the good and bad splits alternate levels in the tree and that the good splits are best-case and the bad splits are worst-case. This is shown in Figure 7.5a below:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-25.png)

The bad split has a partitioning cost of _Θ(n) + Θ(n + 1) = Θ(n)_. The good split in Figure 7.5b also hase a partitioning cost of _Θ(n)_. Even though the good split is significantly more evenly partitioned than the bad split, they are still both _Θ(n)_.

Thus, the running time of quicksort taking account good and bad partitions is still _O(n lg n)_, with the only difference being that the bad splits have a slightly larger hidden constant.

## 7.3 | A Randomized Version of Quicksort

In exploring the average-case complexity of quicksort, we assumed that good and bad splits were equally likely. In reality, this is not likely, but we can add randomization to an algorithm in order to obtain good expected performance over all inputs.

Instead of always using _A[r]_ as the pivot, we will select an element from the subarray A[p...r] at random. We do so by first exchanging _A[r]_ with a random element from _A[p...r]_. By randomly sampling the range _p,...,r,_ we ensure that the pivot element _x = A[r]_ is equally likely to be any of the _r - p + 1_ elements in the subarray.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-26.png)
