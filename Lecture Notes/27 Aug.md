# Chapter 2 (cont.)

**Loop invariance for insertion sort**:
1. **Initialization**: Initially the subarray A[1...j-1] only consists of one element, A[1]. Thus, it is already sorted.
2. **Maintenance**:  The body of the for loop works by moving A[j-1], A[j-2], A[j-3], and so on by one position to the right
until it finds the proper position for A[j] (lines 4–7), at which point it inserts the value of A[j] (line 8). 
The subarray A[1... j] then consists of the elements originally in A[1...j], but in sorted order. Incrementing j for the next iteration
of the for loop then preserves the loop invariance.
3. **Termination**: The condition causing the for loop to terminate is that j > A.length = n. Because
each loop iteration increases j by 1, we must have j = n + 1 at that time. Substituting n + 1 for j in the wording of loop invariant, 
we have that the subarray A[1...n] consists of the elements originally in A[1...n], but in sorted order. 
Observing that the subarray A[1...n] is the entire array, we conclude that the entire array is sorted. Hence, the algorithm is correct.

### Chapter 2.2: Analyzing Algorithms

**Random-Access Machine (RAM)**: A generic, one-processor computational model used by this book. In the RAM model, 
instructions are executed one after another, with no concurrent operations.

**Analysis of the running time of insertion sort**:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/1.png)

Note: For the above graphic, n = A.length and t<sub>j</sub> denotes the number of times the while-loop (line 5) is executed for that value of j.

- The best case is when t<sub>j</sub>= 1, which means the list is already sorted. This would have a time complexity of c<sub>1</sub>(n + c<sub>2</sub>), or Θ(n).

- The worst case is when t<sub>j</sub> is large, which means that the list is sorted in reverse order. This would have a time complexity of Θ(n<sup>2</sup>).

- The average case is n<sup>2</sup>/2, or just Θ(n<sup>2</sup>).

### Chapter 2.3.1: The Divide-and-Conquer Approach

**The Divide-and-Conquer Paradigm**:
1. **Divide** the problem into a number of subproblems that are smaller instances of the
same problem.
2. **Conquer** the subproblems by solving them recursively. If the subproblem sizes are
small enough, however, just solve the subproblems in a straightforward manner.
3. **Combine** the solutions to the subproblems into the solution for the original problem.

**Merge Sort**:
1. **Divide**: Divide the n-element sequence to be sorted into two subsequences of n=2
elements each.
2. **Conquer**: Sort the two subsequences recursively using merge sort.
3. **Combine**: Merge the two sorted subsequences to produce the sorted answer
