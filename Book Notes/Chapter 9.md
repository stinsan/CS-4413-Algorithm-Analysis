# Chapter 9: Medians and Order Statistics

The _i_ th **order statistic** of a set of _n_ elements is the _i_ th smallest element. Thus, the **minimum** of a set is the 1st order
statistic and the **maximum** of the set is the _n_ th order statistic.

The **median** of a set is the element at location _floor( (n + 1) / 2 )_.

## 9.1 | Minimum and Maximum

This is how to find the minimum value of an array with an upper bound of _n-1_ comparisons:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-35.png)

From this, you can also find the maximum with an upper bound of _n-1_ comparisons.

### Simultaneous Minimum and Maximum

What if you want to find the minimum and maximum of an array simultaneously? What's the best approach?

A naive way would be to find the minimum and maximum independently, which would result in _(n-1)+(n-1) = 2n-2_ comparisons.

However, we are big brain and have a way of finding both the minimum and the maximum using at most _3 * floor( n/2 )_ comparisons by processing elements in pairs:

1. Compare elements with each other.
2. Compare the smaller element in the pair with the current minimum, and replace the current minimum if needed.
3. Compare the bigger element in the pair with the current maximum, and replace the current maximum if needed.

Thus, there are 3 comparisons per pair of elements in the array.

## 9.2 | Selection in Expected Linear Time

The algorithm Randomized-Select is modeled after
the quicksort algorithm. As in quicksort, we partition the input array
recursively. But unlike quicksort, which recursively processes both sides of the
partition, Randomized-Select works on only one side of the partition. This
difference shows up in the analysis: whereas quicksort has an expected running
time of <br/>_Θ(n lg n)_, the expected running time of Randomized-Select is _Θ(n)_,
assuming that the elements are distinct. Randomized-Select also uses the Randomized-Partition procedure.

The following code for Randomized-Select returns the _i_ th smallest
element of the array _A[p ... r]_ :

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-36.png)

This worst-case for this algorithm is _Θ(n<sup>2</sup>)_, and occurs if partitioning always occurs around the largest remaining element.

However, since this is randomized, no particular input illicits this worst-case; it is just a matter of luck when partitioning. Thus, the expected running time is _Θ(n)_.

## 9.3 | Selection in Worst-Case Linear Time

We now examine a selection algorithm whose running time is _O(n)_ in the worst
case. Like Randomized-Select, the algorithm Select finds the desired element by recursively partitioning the input array. Here, however, we guarantee a good split upon partitioning the array.

The Select algorithm determines the _i_ th smallest of an input array of _n > 1_
distinct elements by executing the following steps:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-37.png)
![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-38.png)
