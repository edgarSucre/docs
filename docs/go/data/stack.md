---
sidebar_position: 2
---

# Stack

Data structure akin to an array with a simplified interface that exposes methods for inserting 
`Push` and deleting `Pop` data. Stacks follows the `LIFO` strategy to manage it's elements.

## Use cases
- Text editor use it for undo mechanisms.
- Browsers to support the back and forward navigation buttons.
- Syntax toolings for matching brackets and braces.
- Used to support recursion by keeping track of previous function calls.
- Used for *Deep First Search* on a graph.
- To solve the tower of hanoi

![stack](img/stack.png)

```go
// implementation using an array
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

// implementation using an linked list
type LinkedList[T any] interface {
    Prepend(T)
    Pop() (T, bool)
    Size() int
}

type LinkedStack[T any] struct {
    list LinkedList[T]
}

func (stack *LinkedStack[T]) Push(item T) {
    stack.list.Prepend(item)
}

// the returned boolean indicate the item was removed successfully.
func (stack *LinkedStack[T]) Pop() (T, bool) {
    return stack.list.Pop()
}

func (stack LinkedStack[T]) IsEmpty() bool {
    return stack.list.Size() == 0
}
```
