---
title: 'CircularlyLinked Lists'
date: '20210613164729'
category: 'dsa'
tags: ['circularlylinked', 'linkedlist']
---

# circularly linked lists
These are linkedlists where the **head** and **tail** nodes connect to each other
rather than to **null** references.

## What is a circularlylinked list
* Type of a linkedlist where the front and back are connected
* Usually this doesn't include a tail pointer
    * This doesn't change our add/remove efficiency
* Termination condition for logic changes due to no "end" to the list
* We can no longer iterate until we're null because this is linked
    * To mitigate this we can utilize a size variable
    * Additionally, we can use the `current.next` to point to the head as a termination condition
* These can be singly or doubly linked lists

Example circularlylinked list
![Circularly linked list diagram](./20210613165314-img-1.png)

## Adding to a circularlylinked list
* **Adding to the front** we access the back of the list, which we don't have without a tail pointer
* **Adding to the back** requires that we work through a similar workflow as adding to the front

Example of adding to the front:
![Adding to the front](./20210613170244-img-2.png)

* We change the head reference to the new node, then have to iterate the list in O(n) to reach our last node
    * Once at the last node we change the tail reference to point to the new node

### Efficient adding to the front
1. Create a new empty node
1. Add the new node at index 1
1. Move the data from the head to the new node
1. Add the new data into the head node

* This ensures that the next reference to the new node is maintained without having to change the pointers

Create a node:
![Adding to the front efficiently, new node](./20210613170524-img-3.png)

Add the node to the list at index 1 to be copied:
![Adding to the front efficiently, inserting the node](./20210613170537-img-22.png)

### Adding to the back
1. Create a new empty node
1. Add the new node at index 1
1. Copy data from the head node to the new node
1. Insert new data at the tail node
1. Change the reference for the head to the "new node"

Create a node and insert at index 1:
![Adding to the back efficiently, new node](./20210613171032-img-4.png)

Shift the data to the new node and change the head reference:
![Shift the data to the new node](./20210613171105-img-5.png)

## Removing from the front
* Removing from the front is trickier than just moving the head
* This is an O(1)
* Edge case: If the list is size 1 we have to avoid continually referencing ourself

1. Move the data from `head.next` into the head
1. Remove the second node from the list
    1. Redirect the head's reference to the 3rd in the list, skipping node 2

Removing from the front:
![Removing from the front](./20210613171302-img-6.png)

Skip the 2nd node and allow it to be garbage collected:
![](./20210613171348-img-7.png)

## Removing from the back
* No special O(1) technique, this is O(n)
* Must use a loop to stop one sort of the last node
* We have to have access to the node itself to remove it, the only way to reach the node is through traversal

Accessing the last node:
![Traversing the list](./20210613171613-img-8.png)

## Removing from the middle
* Removing from the middle is the same as a singlylinked list
* We have to traverse in O(n)
* Work through the list and then change the pointer reference once we find the node we want to delete

## Example linkedlists
* Singlylinked list:
    * Web browser sesarch history (back button)
* Doublylinked list:
    * Most recently used cache, music app that keeps song history
* Circularlylinked list:
    * Music playlist that starts over once it completes

