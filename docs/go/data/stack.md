---
sidebar_position: 2
---

# Stack

Data structure akin to an array with a simplified interface that exposes methods for inserting 
`Push` and deleting `Pop` data. Stacks follows the `LIFO` strategy to manage it's elements.

![stack](stack.png)

```go
type Stack[T any] interface {
    Push[T](item T) // put elements at the top of the stack
    Pop() T // remove element from the top of the stack and return it
}

type ConcreteStack[T any] struct {
    items []T
}

func (s *ConcreteStack[T]) Push(item T) {
    s.items = append(s.items, item)
}

func (s *ConcreteStack[T]) Pop() T {
    size := len(s.items)

    var empty T
    if size == 0 {
        return empty
    }

    item, s.items = s.items[size -1], s.items[:size-1]

    return item
}
```
