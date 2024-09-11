---
sidebar_position: 1
---

# Linked Lists

Is a data structure that represents a list of elements on which the elements can point to another
element. The first element of the list is called **Head** and the  last is called **Tail**.

## Properties

| Property |                    Description                    |
| :------: | :-----------------------------------------------: |
|   node   |                element of the list                |
|   next   |             pointer to the next node              |
| previous | pointer to the previous node (double linked list) |

---
![linked-list](img/linked_list.png)

---
```go
type LikedList[T any] struct {
    head *Node[T]
    tail *Node[T]
}

type Node[T any] struct {
    val T
    next *Node
    prev *Node
    size int
}

func (n Node[T]) Next() *Node[T] {
    return n.next
}

func (n Node[T]) Prev() *Node[T] {
    return n.prev
}

func (n Node[T]) Val() T {
    if n == nil {
        return nil
    }

    return n.val
}

// add elements at the end of the list
func (list *LinkedList[T]) Append(v T) {
    node := &Node{val: v}
    
    if list.head == nil {
        list.head, list.tail = node, node
    } else {
        list.tail.next = node
        list.tail = node
    }

    list.size++
}

// insert elements at the start of the list
func (list *LinkedList[T]) Prepend(v T) {
    node := &Node{val: v}

    if list.head == nil {
        list.head, list.tail = node, node
    } else {
        list.head.prev = node
        list.head = node
    }

    list.size++
}

// remove element from the start of the list, and return said element
// the returned boolean indicate the item was removed successfully.
func (list *LinkedList[T]) (Pop() Node[T], bool) {
    if list.head == nil {
        return nil, false
    }

    n := list.head
    list.head = list.head.next
    n.next = nil

    return n, true
}

func (list *LinkedList[T]) Find(v T) *Node[T] {
    return findInList(list.First(), v)
}

func findInList[T any](node *Node[T], target T) *Node[T] {
    if node == nil {
        return nil
    }

    if node.Val() == target {
        return node
    }

    findInList(node.Next(), target)
}
```