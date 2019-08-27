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
