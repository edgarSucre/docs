---
sidebar_position: 3
---

# Heap
A heap is a tree based data structure that satisfies the `heap invariant`: If A is a parent node of B then A is ordered with respect to B. This separates the heap in two types `min heap` where all child node are bigger than the parent node and `max heap` with the opposite.

## Binary heap
A `binary heap` is a binary tree that supports the heap invariant. In a binary tree every node has exactly two children.

### Implementation 
The representation of a binary heap is a tree structure however it's implementation is based on an array. This give us a practical way for locating parent and child nodes

```go
type Node[T any] struct {
    value T
}

type MinHeap[T any] struct {
    list []Node[T]
}

// i is a child index
func parent(i int) int {
    return (i-1)/2
}

// i is the parent index
func left(i int) int {
    return 2*i + 1
}

// i is the parent index
func right(i int) int {
    return 2*i + 2
}

func (h *MinHeap[T]) swap(i,j int) {
    h.list[i], h.list[j] = h.list[j], h.list[i]
}

func (h *MinHeap[T]) Insert(v T) {
    node := Node{value: v}
    h.list = append(h.list, node)

    h.heapIfyUp(len(h.list)-1)
}

func (h *MinHeap[T]) heapIfyUp(index int) {
    for h.list[parent(index)] > h.list[index] {
        h.swap(parent(index), index)
        index = parent(index)
    }
}

func (h *MinHeap[T]) Pop() (Node[T], bool) {
    if len(h.list) == 0 {
        return nil, false
    }

    removed := h.list[0]

    lastPosition := len(h.list) - 1

    h.list[0] = h.list[lastPosition]

    h.list = h.list[:lastPositing]

    h.heapIfyDown(0)

    return removed, true
}

// index represents a parent node
func (h *MinHeap[T]) heapIfyDown(index int) {
    lastIndex := len(h.list) - 1
    leftChildIndex, rightChildIndex := left(index), right(index)

    childToCompare := 0

    for leftChildIndex <= lastIndex {
        if leftChildIndex == lastIndex {
            childToCompare = leftChildIndex
        } else if h.list[leftChildIndex].value < h.list[rightChildIndex].value {
            childToCompare = leftChildIndex
        } else {
            childToCompare = rightChildIndex
        }

        if h.list[index] > h.list[childToCompare] {
            h.swap(index, childToCompare)
        } else {
            return
        }
    }
}

```

### Heap package
The heap package provides a heap interface that can be implemented

```go
import (
	"container/heap"
	"fmt"
)

// An IntHeap is a min-heap of ints.
type IntHeap []int

func (h IntHeap) Len() int           { return len(h) }
func (h IntHeap) Less(i, j int) bool { return h[i] < h[j] }
func (h IntHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *IntHeap) Push(x any) {
	// Push and Pop use pointer receivers because they modify the slice's length,
	// not just its contents.
	*h = append(*h, x.(int))
}

func (h *IntHeap) Pop() any {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[0 : n-1]
	return x
}

// This example inserts several ints into an IntHeap, checks the minimum,
// and removes them in order of priority.
func main() {
	h := &IntHeap{2, 1, 5}
	heap.Init(h)
	heap.Push(h, 3)
	fmt.Printf("minimum: %d\n", (*h)[0])
	for h.Len() > 0 {
		fmt.Printf("%d ", heap.Pop(h))
	}
}

```