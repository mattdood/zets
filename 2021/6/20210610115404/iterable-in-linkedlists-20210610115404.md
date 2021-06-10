|  Title | Category  | Tags  | Date |
| ------------ | ------------ | ------------ | ----|
| iterable-in-linkedlists | dsa  | linkedlist, singlylinked list  | 20210610115404 |

# iterable in linkedlists
Using `Iterable` gives a user the ability to iterate over the SinglyLinkedList
structure without giving access to `Node` objects and their respective states.

## Node scope
Limitations of LinkedLists:
* We cannot access an element at a specific index or position in a linked list.
    * This is because the nodes are processed one at a time
* `Node` scope is only to the next node

## Iterating through a linked list
`Iterators` loop through data based on a `current` cursor, rather than having a
`while loop` that would require termination statements.

The iteration using `Iterator` would instead use `hasNext()` and `next()` methods,
which do not require termination statements.

```java
import java.util.Iterator;
public class LinkedList<T> implements Iterable<T> {
    // Other methods omitted

    // Returns iterator of the iterable object.
    // This overrides `iterator()`
    public Iterator<T> iterator() {
        return new LLiterator<>(); // generic implementation of `Iterator`
    }

    // Within LinkedList class we implement a subclass
    private class LLIterator implements Iterator<T> {
        private Node<T> curr;
        LLIterator () { curr = head; }
        public boolean hasNext() { return curr != null; }
        public T next() {
            if (hasNext()) {
                T temp = curr.data;
                curr = curr.next;
                return temp;
            }
            return null;
        }
}
```

### Using an iterator
The `Iterator` that was created in the previous section is now instantiated.
This gives the user more control over what we can do, while also giving a more
reasonable interface to interact with the `LinkedList` object.

```java
// Create a `LinkedList` object
linkedList<String> courses = new LinkedList<>();

// List populated here


// using thte iterator this way give us more
// control over each step
Iterator<String> courseIt = courses.iterator();
while (courseIt.hasNext()) {
    String data = courseIt.next();
    // Do something with the data here
}
```


