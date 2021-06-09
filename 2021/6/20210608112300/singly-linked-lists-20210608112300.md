|  Title | Category  | Tags  | Date |
| ------------ | ------------ | ------------ | ----|
| singly-linked-lists | dsa  | linkedlist, singly linked  | 20210608112300 |

# singly linked lists
Singly-linked lists (SLL) are the basic building blocks of the LinkedList
structural design.

ArrayLists were considered a dynamic data structure, though they require manual
resizing and upkeep in the methods.

LinkedLists do not require resizing operations and can expand indefinitley..

## Linkedlist
These are an alternative to arrays and overcome the some of the
drawbacks of using arrays.

Linkedlist points:
* Implements the list ADT, similar to Arraylist
* does not store data contiguously in memory, data is stored in nodes
* linked data structure is a collection of nodes
    * data is stored in the Node object
    * connections between nodes is done by having each node point to the next node in the list
    * data is not stored contiguously like in ArrayList

### Head pointers
Every node in a linkedlist has a head pointer that points to another node.

* If the **head** is null, then the singly linked list is empty

### Node class
For this example the node class is private, this is to avoid having other external
classes make node objects.

The example below uses a static sub-class from the `SinglyLinkedList` parent.

Attributes on nodes:
* Nodes should only be made by the `SinglyLinkedList`
* A node will have some `data` attribute and a header, `next`
    * in this case the header is an object reference
*

```java
// the parent class has access to the attributes
// of each Node
public class SinglyLinkedList {

    // private sub-class
    private static class Node {
        private int data;
        private Node next; // the reference header

        // constructor
        private Node(int data, Node next) {
            this.data = data;
            this.next = next;
        }

        // alternative constructor chained to the
        // full constructor, adding flexibility
        private Node(int data) { this(data, null); }

    }
}

```

### Adding nodes to the list (method)
After the constructor of the node is complete, helper methods can be added.

**Note**: When reassigning pointers we need to be careful, we can easily
lose track of the rest of the list if our pointer is assigned improperly.

Adding a node to the front:
1. Create the node itself
    1. Includes all data required
1. Set the new node's next reference points to the same node as the new node
1. Set the head to be the new node

Adding a node to the back:
1. Verify that the list itself is not null
    1. If the list is null, just make a `Node`
1. We have to iterate to the back of the list
1. Once we reach the back of the list (last known node):
    1. Set the `current.next` equal to a new `Node` object

```java

public class SinglyLinkedList {
    // full constructor omitted for brevity

    private Node head;
    public void addToFront(int data) {
        Node newNode = new Node(data);
        newNode.next = head;
        head = newNode;
    }

    public void addToBack(int data) {
        if (head == null) { // List is empty
            head = new Node(data);
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = new Node(data);
        }
    }

}

```

## toString() (method)
There are two implementations of `toString()` for this to
return the data from nodes. One is a public method for the node itself
and the other is a public method for the `SinglyLinkedList` object.


```java
public class SinglyLinkedList {

    // private sub-class
    private static class Node {
        private int data;
        private Node next; // the reference header
        // constructor
        private Node(int data, Node next) {
            this.data = data;
            this.next = next;
        }
        private Node(int data) { this(data, null); }

        // just use the toString() method of the data
        // in this case the data is an `int`
        public String toString() { return Integer.toString(); }

    }

    public String toString() {
        String answer = ""; // keeps track of all the string
        Node current = head; // reference to the current node

        // once we hit the last node, the next one will be null
        while (current != null) {
            answer += current = " ";
            current = current.next;
        }
        return answer;
    }
}

```
