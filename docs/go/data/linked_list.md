---
sidebar_position: 1
---

# Linked Lists

Is a data structure that represents a list of elements on which the elements can point to another
element. The first element of the list is called **Head** and can only point to the next element.

## Properties

| Property |                    Description                    |
| :------: | :-----------------------------------------------: |
|   node   |                element of the list                |
|   next   |             pointer to the next node              |
| previous | pointer to the previous node (double linked list) |

---
![linked-list](linked_list.png)

---
```go
type LikedList struct {
    head *Node
    tail *Node
}

type Node struct {
    val int
    next *Node
    prev *Node
}

func (n Node) Next() *Node {
    return n.next
}

func (n Node) Val() int {
    return n.val
}

func (list *LinkedList) Push(v int) {
    node &Node{val: v}
    
    if list.head == nil {
        list.head = node
    }

    list.tail.next = node
    list.tail = node
}

func (list *LinkedList) Find(v int) *Node {
    return findInList(list.First(), v)
}

func findInList(node *Node, target int) *Node {
    if node == nil {
        return nil
    }

    if node.Val() == target {
        return node
    }

    findInList(node.Next(), target)
}
```