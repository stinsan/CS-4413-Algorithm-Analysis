# Chapter 1

Input → **Algorithm** → Output

Algorithms must: <br/>
1. Terminatate <br/>
2. Be correct (although incorrect algorithms can be useful -- heuristic) <br/>
3. Be efficient (in terms of time, space, randomness)<br/>
  
Types of algorithms: <br/>
1. Deterministic and sequential <br/>
2. Parallel (algorithms that use multiple proccessing cores) <br/>
3. Randomized <br/>
4. Approximation (may not be optimal, used for hard problems) <br/>

NP-complete algorithms:
- Approximation algorithms are used for these
- Traveling-salesman problem
- P ≠ NP: "P" stands for polynomial, "N" stands for non-deterministic

-----------------------------------------------------------------------

# Chapter 2

**Insertion Sort**
- Efficient for sorting small data sets

![alt text](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/0.png)

Correctness of insertion sort using **loop invariants**:
 
To do this, we must show that at the start of every for-loop from lines 1 through 8, 
the subarray A[1... j-1] consists of the elements originally in A[1...j-1], but in 
sorted order.

To show that a loop invariant proves correctness, we must show:
1. **Initialization**: It is true prior to the first iteration of the for-loop
2. **Maintenance**: It is true before an interation, it's also true before the next iteration
3. **Termination**: When the loop terminates, the invariant gives us a useful property
that helps show that the algorithm is correct
