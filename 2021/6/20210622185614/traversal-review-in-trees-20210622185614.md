---
path: '/2021/6/traversal-review-in-trees-20210622185614'
title: 'traversal review in trees'
date: '20210622185614'
category: 'dsa'
tags: ['traversal', 'recursion', 'binary search tree', 'binary tree', 'trees']
---

# traversal review in trees
Different traversals offer pros and cons when working with BSTs, depending on the use case.

## Preorder
* Uniquely identifies a BST
* Hybrid depth approach that biases toward giving data closer to the root faster than data in leaf nodes

## Inorder
* Most notable property is that if implemented on a BST the data is returned sorted
* The inorder traversal is the only one that does not uniquely define a BST
* If implemented on a regular binary tree the data is just given left-to-right

## Postorder
* This is similar to preorder and uniquely identifies a BST
* When removing data it will only remove from the leaf nodes
* This is a hybrid depth approach that biases data in leaf nodes faster than giving data closer to root

## Levelorder
* This is easiest to understand
* Gives the data in an ordering sorted based on the depth of each level
* Uniquely identifies a BST and gives data in a sorted manner on a per-level basis


