# Heap

## Definition

Heap is a complete tree, where the node value is always either greater (max heap) or smaller (min heap) the child values.

## Java implementation

Java support HEAP implementation via `PriorityQueue`
```java
// priority queue is min by default
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a,b)->Integer.compare(b,a);
```

## Array implementation

An array can be used to store heap: Element at index i will have parent at `(i-1)/2`, left child at `i*2 + 1`, right child at `i*2 + 2`. The root is at index 1.

### Example:

```txt
      6
    /   \
   4     5
  / \   / \
 3   2 0   1
```

| 0   | 1   | 2   | 3   | 4   | 5   | 6   |
| --- | --- | --- | --- | --- | --- | --- |
| 6   | 4   | 5   | 3   | 2   | 0   | 1   |

### Operations

* Delete root  - $O(log(n))$

1. Remove the root
2. Swap the last element with the root
3. Heapify down from  
    (Swapping with left or right nodes)

* Insert to heap - $O(log(n))$

1. Insert element to the end of the heap
2. Heapify up from the inserted index (Swapping with parent node)

### Pseudo-code

```java
class Heap {
	int[] heap;
	int len;
	Heap(int n) {
		heap = new int[n];
		len = 0;
	}

	void add(int value) {
		heap[len] = value;

		int curIndex = len;
		while(curIndex > 0) {
			int nextIndex = (curIndex - 1) / 2;
			if(heap[nextIndex] < heap[curIndex]) {
				swap(nextIndex, curIndex);
			} else {
				break;
			}
			curIndex = nextIndex;
		}

		len++;
	}

	int remove() {
		int top = heap[0];
		heap[0] = heap[len - 1];
		heap[len - 1] = 0;
		len--;

		int curIndex = 0;
		while(curIndex < len) {
			int right = curIndex * 2 + 1;
			int left = curIndex * 2 + 2;

			boolean rightGreater = (right < len) && (heap[right] > heap[curIndex]) ;
			boolean leftGreater = (left < len) && (heap[left] > heap[curIndex]) ;
			

			if(!rightGreater && !leftGreater) {
				break;
			}

			if(rightGreater && !leftGreater) {
				swap(right, curIndex);
				curIndex = right;
				continue;
			} 

			if(!rightGreater && leftGreater) {
				swap(left, curIndex);
				curIndex = left;
				continue;
			} 

			if(heap[right] > heap[left]) {
				swap(right, curIndex);
				curIndex = right;
			} else {
				swap(left, curIndex);
				curIndex = left;
			}
		}
		
		return top;
	}

	private void swap(int nextIndex, int curIndex) {
		int temp = heap[nextIndex];
		heap[nextIndex] = heap[curIndex];
		heap[curIndex] = temp;
	}
}
```