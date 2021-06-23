---
path: '/2021/6/unique-binary-tree-using-traversal-combos-20210622193837'
title: 'unique binary tree using traversal combos'
date: '20210622193837'
category: 'dsa'
tags: ['binary tree', 'trees', 'recursion']
---

# unique binary tree using traversal combos
When working through creation of unique binary tree structures I was given this
question in a quiz:

```
Alice and Bob both know that if you have a preorder, postorder, or levelorder
traversal of a BST, you can uniquely reconstruct the original BST. However, Bob
is curious about what we need to guarantee the uniqueness of a plain old binary
tree with no order property. Alice suggests that the right choice of two
different traversals can guarantee uniqueness. Which of the following
combinations will guarantee a unique binary tree?
```

This can be tested using 2 node trees and a visualization tool. The concept
with this traversal strategy is that when constructing we will allow one
traversal to choose the order and another traversal to do the creation.

## Combinations
Each of these will work through an `order -> structure` or `structure -> order`
1. inorder and levelorder
1. preorder and inorder
1. inorder and postorder

