# Segment tree

## When to use

Similar to Binary indexed tree, segment tree can be used for efficient update and query for an array of data - both O(log(n)).

* If we save data normally, updation would take O(1) , but query would take O(n)

* If we save aggreated data, query would take O(1), but update would take O(n)

Compare to binary indexed tree, segment tree's aggreated function no need to be a grouped operation , but take more memory.

## Structure

Given the array of data $A[0 \ldots N-1]$ .
Segment tree is a form of binary tree: The root of tree would save aggregated data from $0$ to $N - 1$, the 2 childs save aggregated data from $0$ to $(N - 1)/2$ and $(N+1)/2$ to $N-1$ (split the range in half) and so on. Each node , except the leaf, would have 2 childs. We would have less than $4N$ tree nodes.

- Building: building from leaves to top by aggregated function - which can be call from the root using a recursive function.

- Query: Query from the root, we could have 3 case: the query range out of the node's range ( not include the node) , the query range include the node's range ( include the node) and the query range partly overlap the range ( check the child nodes).

- Update: Update the matching nodes, whose range the index is between.


