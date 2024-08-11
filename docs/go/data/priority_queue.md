---
sidebar_position: 4
---

# Priority Queue
`PQ` Is an abstract data type that operates similar to a normal queue except that each element has a
certain priority. The priority of the elements determine the order in which elements are removed
from the queue. In `PQ` inserting is done with `Add` which inserts the element and `Poll` which 
removes the element with the highest priority. `PQ` use mainly heaps as data structure, but it can
implemented with other data structures.

## Heap
A heap is a tree based data structure that satisfies the `heap invariant`: If A is a parent node of
B then A is ordered with respect to B. This means the tree must be in certain order *min* or
*max* to be a valid heap.

### Binary heap
A `binary heap` is a binary tree that supports the heap invariant. In a binary tree every node has
exactly two children.

### Complete binary tree
A `complete binary tree` is a tree in which at every level, except possibly the last is completely
filled and all nodes are as far left as possible.

![linked-list](img/heap.png)

## Use cases
- Anytime you need the dynamically fetch the `next best`, or the `next worst`.
- `Best First Search` such as A* use `PQ` to grab the next most promising node.
- Used by `Minimum Spanning Tree` algorithms.