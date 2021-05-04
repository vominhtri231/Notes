# Definition
Heap is a complete tree, where the node value is always either greater (max heap) or smaller (min heap) the child values.

# Array as heap
An array can be used to store heap: Elmenent at index i will have parent at `(i-1)/2`, left child at `i*2 + 1`, right child at `i*2 + 2`. The root is at index 1.

Example:

```
      6
    /   \
   4     5
  / \   / \
 3   2 0   1


```
|0|1|2|3|4|5|6|
|-|-|-|-|-|-|-|
|6|4|5|3|2|0|1|

# Operations

### Delete root
1. Remove the root
2. Swap the last element with the root
3. Heapify down from  
  (Swapping with left or right nodes)

### Insert to heap
1. Insert element to the end of the heap
2. Heapify up from the inserted index     
  (Swapping with parent node)