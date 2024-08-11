---
sidebar_position: 3
---

# Queue
Data structure that follows the `FIFO` strategy to manage it's elements. It uses `Enqueue` to
insert elements at `Back` of the list, and `Dequeue` to remove elements from the `Front`.

## Use cases
- Message based services.
- Used for *Breadth First Search* traversal in graphs.
- Any type of process that requires FIFO.


![queue](img/queue.png)

```go
// implementing a queue with an array
type Queue[T any] struct {
    items []T
}

func (q *Queue[T]) Enqueue(item T) {
    q.items = append(q.items, item)
}

func (q *Queue[T]) Dequeue() T {
    var empty T

    if len(q.items) == 0 {
        return empty
    }
    
    item, items := q.item[0], q.items[1:]
    q.items = items

    return item
}


// implementing a queue with linkedList
type Queue[T any] struct {
    list LinkedList[T]
}

func (q *Queue[T]) Enqueue(item T) {
    q.list.Append(item)
}

func (q *Queue[T]) Dequeue() T {
    return q.list.Pop().Val()
}
```