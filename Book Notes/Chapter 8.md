# Chapter 8: Sorting in Linear Time

## 8.1 | Lower Bounds for Sorting
All the sorts covered previously were comparison sorts. That is, given two elements _a_ and _b_, we perform one of the tests <br/>
_a < b_, _a ≤ b_, _a = b_, _a ≥ b_, or _a > b_ to determine their relative order.

In this section, we assume that all input elements are unique. Given this assumption, comparisons of the for _a = b_ are useless, so we can assume that no comparisons of this form are made. Also note that the comparisons _a ≤ b_, _a < b_, _a ≥ b_, and _a > b_ are all equivalent in that they yield the same information about the ordering of _a_ and _b_. Thus, we can assume that all comparisons have the form _a ≤ b_.

### **The Decision-Tree Model**:

**Decision Tree**: A full binary tree that represents the comparisons between elements that are performed by a particular sorting algorithm operating on an input of a given size.

Figure 8.1 below is a decision tree showing insertion sort.

![](https://github.com/stinsan/CS-4413-Algorithm-Analysis/blob/master/Screenshots/algo-27.png)
