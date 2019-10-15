# Chapter 15: Dynamic Programming

In chapters 2 and 4 we saw the divide-and-conquer method of solving problems. The algorithms involve partitioning the problem into disjoint
subproblems, solving the subproblems recursively, and combining their solutions to solve the original problem. In contrast, dynamic programming applies when the subproblems overlap—that is, when subproblems share subsubproblems. In this context,
a divide-and-conquer algorithm does more work than necessary, repeatedly solving the common subsubproblems.

A **dynamic-programming** algorithm solves each subsubproblem just ojnce and then saves its answer in a table, thereby avoiding the work of recomputing
the answer every time it solves each subsubproblem.

Dynamic programming is typically applied to optimization problems. Such problems have many possible solutions, each having a value. We want the solution with the optimal (minimum or maximum) value.

A dynamic-programming algorithm has four steps:
1. Characterize the structure of an optimal solution.
2. Recursively define the value of an optimal solution.
3. Compute the value of an optimal solution, typically in a bottom-up fashion.
4. Construct an optimal solution from computed information.

# 15.1 | Rod Cutting
Serling Enterprises buys long steel rods and cuts them into shorter rods, which it then sells. Each cut is free. We assume that we know,
for _i = 1, 2, ..._ the price _p<sub>i</sub>_ that Serling charges for a rod of length _i_ inches. Rod lengths are always integer values. Figure 15.1 below shows an example table.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-39.png)

Given a rod length of _n_ inches and a table of prices _p<sub>i</sub>_ for _i = 1, 2, ..., n_, detemine the maximum revenue _r<sub>n</sub>_ obtainable by cutting up the rod and selling the pieces. Note that if the price _p<sub>n</sub>_ for a rod of length _n_ is large enough, an optimal solution may require no cutting at all.

Consider the case when _n = 4_. Figure 15.2 below shows all the ways to cut a 4 inch rod. We see that cutting the rod into two 2-inch pieces produces a revenue of _p<sub>2</sub> + p<sub>2</sub> = 5 + 5 = 10_, which is optimal.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-40.png)

Observe that there are _2<sup>n-1</sup>_ to cut up a rod of length _n_. We denote a decomposition into pieces using ordinary additive notation, so that 7 = 2 + 2 + 3 indicates that a 7-inch rod has been cut into two 2-inch pieces and one 3-ince piece.

If an optimal solution cuts the rod into _k_ pieces, then an optimal decomposition

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_n = i<sub>1</sub> + i<sub>2</sub> + ... +  i<sub>k</sub>_

of the rod into pieces of lengths  i<sub>1</sub>, i<sub>2</sub>, ..., i<sub>k</sub> provides a maximum corresponding revenue

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_r<sub>n</sub> = p<sub>i<sub>1</sub></sub> + p<sub>i<sub>2</sub></sub> + ... +  p<sub>i<sub>k</sub></sub>_

The _r<sub>i</sub>_ for _i_ = 1, 2, ..., 10 is:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-41.png)

More generally, we can frame the values _r<sub>n</sub>_ for _n_ >= 1 in terms of optimal revenues from shorter rods:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; _r<sub>n</sub> = max( p<sub>n</sub> , r<sub>1</sub> + r<sub>n-1</sub> , r<sub>2</sub> + r<sub>n-2</sub> , ... , r<sub>n-1</sub> + r<sub>1</sub> ) = max<sub>1<=i<=n</sub> ( p<sub>i</sub> + r<sub>n-i</sub> )_

### Recursive Top-Down Implementation
This a a top-down, recursive implementation of the above equation:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-42.png)

This algorithm is inefficient because it solves some subproblems over and over again; it takes O(2<sup>n</sup>), which is where dynamic programming comes into play.

### Using Dynamic Programming for Optimal Rod Cutting

Dynamic programming saves the solution of previous subproblems, thus using additional memory to save computation time; it is an example of **time-memory trade-off**.

There are two ways to impelement dynamic programming:
1. Top-down with memoization
2. Bottom-up

In **top-down with memoization**, we modified the procedure to save the result of
each subproblem (usually in an array or hash table). The procedure now first checks
to see whether it has previously solved this subproblem. If so, it returns the saved
value, saving further computation at this level. 
We say that the recursive procedure has been **memoized**;
it “remembers” what results it has computed previously.

Here is the Cut-Rod procedure with memoization:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-43.png)

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-44.png)

The **bottom-up** version is even simpler:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-45.png)

For the bottom-up dynamic-programming approach, the Bottom-Up-Cut-Rod procedure
uses the natural ordering of the subproblems: a subproblem of size _i_ is “smaller”
than a subproblem of size _j_ if _i < j_ . Thus, the procedure solves subproblems of
sizes _j_ = 0, 1, ..., _n_, in that order.

Both the top-down with memoization and the bottom-up method take time complexity Θ(n<sup>2</sup>).

### Reconstructing a Solution
Our dynamic-programming solutions to the rod-cutting problem return the value of
an optimal solution, but they do not return an actual solution: a list of piece sizes.

Here is an extended version of the Bottom-Up-Cut-Rod procedure that computes, for each
rod size _j_, not only the maximum revenue _r<sub>j</sub>_ , but also _s<sub>j</sub>_, the optimal size of the
first piece to cut off:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-46.png)

The following procedure takes a price table _p_ and a rod size _n_, and it calls the
Extended-Bottom-Up-Cut-Rod procedure to compute the array s[1...n] of optimal
first-piece sizes and then prints out the complete list of piece sizes in an optimal
decomposition of a rod of length _n_:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-47.png)

A call to Extended-Bottom-Up-Cut-Rod(_p_, 10) would return arrays

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-48.png)

A call to Print-Cut-Rod-Solution (_p_, 10) would just print 10, while a call to Print-Cut-Rod-Solution (_p_, 7) would print cuts 6 and 1.

### 15.2 | Matrix Chain Multiplication
We are given a chain \<_A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>_\> of _n_ matrices to be multiplies, and we wish to
compute the product _A<sub>1</sub> A<sub>2</sub> ... A<sub>n</sub>_.
 
Take, for example, _n_ = 4; this product can be parenthesized in five different ways:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-49.png)

This is a naive implementation of this matrix multiplication:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-50.png)

If _A_ is a _p x q_ matrix and _B_ is a _q x r_ matrix, the resulting matrix _C_ is _p x r_. The time to compute C is dominated by the number of scalar multiplications in line 8, which is _pqr_.

To illustrate the different costs incurred by different parenthesizations, take the chain \<_A<sub>1</sub>, A<sub>2</sub>, A<sub>3</sub>_\>. Suppose the dimensions are 10 x 100, 100 x 5, and 5 x 50, respectively. 

If we multiply according to ((A<sub>1</sub> A<sub>2</sub>) A<sub>3</sub>), we get 10 x 100 x 5 = 5000 scalar multiplications to compute 
A<sub>1</sub> A<sub>2</sub>, plus 10 x 5 x 50 = 2500 scalar multiplications to multiply that with A<sub>3</sub>. This nets us 7500 scalar multiplications total.

Take another parenthesization, (A<sub>1</sub> (A<sub>2</sub> A<sub>3</sub>)), we perform 100 x 5 x 50 = 25000 scalar multiplications to compute A<sub>2</sub> A<sub>3</sub>, plus 10 x 100 x 50 = 50000 scalar multiplications to multiply that with  A<sub>1</sub>. This nets us 75000 scalar multiplications in total, 10 times more than the previous example.

The **matrix-chain multiplication problem** is stated as follows: Given a chain \<_A<sub>1</sub>, A<sub>2</sub>, ..., A<sub>n</sub>_\> of _n_ matrices, where _i_ = 1, 2, ..., _n_, matrix _A<sub>i</sub>_ has dimension _p<sub>i-1</sub> x p<sub>i</sub>_, fully parthesize the product _A<sub>1</sub> A<sub>2</sub> ... A<sub>n</sub>_ in a way that minimizes the number of scalar multiplications.

### Applying Dynamic Programming

#### Step 1: The structure of an optimal parenthesization
For convenience, let us adopt the notation _A<sub>i...j</sub>_, for the matrix that results from evaluating the product _A<sub>i</sub> A<sub>i+1</sub> ...A<sub>j</sub>_ . If the problem is nontrivial, then to parenthesize _A<sub>i</sub> A<sub>i+1</sub> ...A<sub>j</sub>_ , we must, for some value _k_ such that _i <= k < j_, compute the matrices _A<sub>i...k</sub>_ and _A<sub>k+1...j</sub>_ and then multiply them together to produce the product _A<sub>i...j</sub>_ . Both the "prefix" subchain the and "suffix" subchain have to be optimized themselves.

#### Step 2: A recursive solution
Next, we will define the cost of an optimal solution recursively in terms of the optimal solutions to the subproblems.
We pick as our subproblems the problems of determining the minimum cost of parenthesizing _A<sub>i</sub> A<sub>i+1</sub> ... A<sub>j</sub>_ for _1 <= i <= j <= n_. Let _m[i, j]_ be the minimum number of scalar multiplications needed to compute the matrix _A<sub>i...j</sub>_; for the full problem, the lowest-cost way to compute _A<sub>1...n</sub>_ would be _m[1, n]_.

The definition of _m[i, j]_ is as follows. If i = j, the problem is trivial, meaning no scalar multiplications are needed; thus, _m[i, i] = 0_. When it is nontrivial, we apply the split described in step 1, meaning we split the product _A<sub>i</sub> A<sub>i+1</sub> ...A<sub>j</sub>_ into  _A<sub>i...k</sub>_ and _A<sub>k+1...j</sub>_ for some _k_. Then, _m[i, j]_ equals the minimum cost for computing the subproducts _A<sub>i...k</sub>_ and _A<sub>k+1...j</sub>_, plus the cost of multiplying them together:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; _m[i, j] = m[i, k] + m[k + 1, j] + p<sub>i-1</sub> p<sub>k</sub> p<sub>j</sub>_

Since we don't know the value of _k_, we must check all possible values, namely _k = i, i + 1, ..., j - 1_. Additionally, we only require the minimum cost of parenthesization. Thus, our recursive definition for parenthesizing _A<sub>i...j</sub>_ is:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-51.png)

#### Step 3: Computing the optimal costs
We implement that tabular, bottom up approach in the following procedure:

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-52.png)
