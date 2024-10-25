---
sidebar_position: 2
---

# Binary Tree
Hierarchical data structure composed of `Nodes` on which every Node can have up to 2 children Nodes
`Left` and `Right`. The top of the tree is called `Root`. 

## Binary Search Tree (BST)
A *BST* is a binary tree that satisfies the BST invariant: left subtree has smaller elements and 
right subtree has larger elements.

![binary_tree](../img/binary_search_tree.png)

## Balanced Binary Tree
A height balanced binary tree is a binary tree in which the height of the left subtree and right 
subtree of any node does not differ by more than 1 and both the left and right subtree are also 
height balanced.

![balanced binary tree](../img/binary-tree-balanced.png)

### Balanced vs Unbalanced 
A balanced binary tree has better performance compared to the unbalanced counterpart.

| Operation | Balanced | Unbalanced |
| --------- | -------- | ---------- |
| Insert    | O(log n) | O(n)       |
| Find      | O(log n) | O(n)       |
| Delete    | O(log n  | O(n)       |

### AVL Tree
An *AVL* tree defined as a self-balancing Binary Search Tree (BST) where the difference between 
heights of left and right subtrees for any node cannot be more than one. The difference between the 
heights of the left subtree and the right subtree for any node is known as the *balance factor* of the node.

### Red Black Tree
Red Black Trees are a type of balanced binary search tree that use a set of rules to maintain balance, 
ensuring logarithmic time complexity for operations like insertion, deletion, and searching, 
regardless of the initial shape of the tree. Red Black Trees are self-balancing, using a simple 
color-coding scheme to adjust the tree after each modification.

## Complete Binary Tree
A `complete binary tree` is a tree in which at every level, except possibly the last is completely 
filled and all nodes are as far left as possible.

![complete binary tree](../img/binary-tree-complete.png)

## Full Binary Tree
A `full binary tree` is a binary tree with either zero or two child nodes for each node. 

![full-binary-tree](../img/binary-tree-full.png)

## Binary tree use cases
- Red Black Trees
- AVL Trees
- Splay Trees
- Binary heaps
- Treap - a probabilistic data structure (uses a randomized BST)

## Examples

### BST base structure
```go
type Node[T any] struct {
    value T
    left *Node[T]
    right *Node[T]
}

type Tree[T] struct {
    node *Node[T]
}
```

### BST insert - no balancing
```go
func(t *Tree[T]) Insert(val T) *Tree {
    if node == nil {
        t.node = &Node{value: val}
    } else {
        t.node.insert(val)
    }

    return t
}

// note: ignoring duplicates, depends on the use case

// base insert without any balancing
func (n *Node[T]) Insert(val T) {
    if val < n.value {
        if n.left == nil {
            n.left = &Node{value: val}
        } else {
            n.left.insert(value)
        }
    } else if n > n.value {
        if n.right == nil {
            n.right = &Node{value: val}
        } else {
            n.right.insert(value)
        }
    }
}


```