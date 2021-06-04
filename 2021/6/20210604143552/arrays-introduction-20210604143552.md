|  Title | Category  | Tags  | Date |
| ------------ | ------------ | ------------ | ----|
| arrays-introduction | dsa  | arrays, arraylists  | 20210604143552 |

# arrays introduction
Arrays are statically allocated, contiguous blocks of memory that provide O(1)
access to a data of a single type. This data is stored at a specified index.

## Arrays
Arrays are not primitive data structures (i.e., ints, floats, chars, boolean). These are used
to store a sequence of related objects/values.

Properties:
* Each array is a sequence of cells with an associated index to the cell.
* Allocations of **contiguous** blocks of memory
* Cells store one element each
* These are flexible and can store a wide variety of data types
* Access is constant time if you know the index of a cell

Arrays do not have to be immediately constructed, they can be initialized with
values, or initialize empty and then fill in later.

## Accessing and searching

### Access
* location (index) is known and is O(1)
* data at index 5 is exactly 5 memory locations away from index 0
* data can be accessed by just adding to the memory address of index 0

```java

// some array of ints
int[] someArray = {0, 1, 2, 3, 4, 5, 6, 7, 8}

```

### Search
* if the location is unknown then the time complexity is O(n)
* searches are linear if we do not know the index (rephrase of above comment)

## Memory
Memory is statically allocated, meaning that the bounds of the array is
the set capacity based on the index count determined at creation.

This is an explanation of why index bound errors exist.

```

// memory would be:
...{0, 1, 2, 3, 4}...
// where this is the bounds

```




