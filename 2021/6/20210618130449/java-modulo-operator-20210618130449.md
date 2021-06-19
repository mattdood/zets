---
path: '/2021/06/java-modulo-operator-20210618130449'
title: 'Java Modulo Operator'
date: '20210618130449'
category: 'java'
tags: ['modulo', 'java']
---

# java modulo operator
The `%` in Java is modulo. The integers are partitioned by a modulo operation
into multiple "classes".

Java has slightly different behavior when working through modulo operations in
negatives. True and expected behaviors are listed below.

Example:
```java
// Integers by modulo 2

// Divides the integers into 2 `classes`
// these are "divisible evenly by 2" and "not divisibile evenly by 2"
// also known as even or odd

{..., 1, 3, 5, ...}, {..., 2, 4, 6, ...}
```

* Doing a modulo by 3 would give 3 classes, etc.

The integers modulo `n` gives us `n` different classes of numbers, based on the remainder.

## Expected behavior
Typically when working with remainders we want the smallest non-negative member of the class.
This gives a unique number to think of when thinking of modulo operations.

Example of modulo expected behavior:
```java
// taking 9 % 5
9 % 5 = 4

// using a negative, -9 % 5
-9 % 5 = 1
-10 = 5 * (-2) + 1 // this is the smallest non-negative remainder
```

## True behavior
When working with Java we get the **signed remainder closest to 0**

Java's `%` operator returns the closest remainder to 0.

Example above with true behavior:
```java
// taking 9 % 5
9 % 5 = 4

// using a negative, -9 % 5
-9 % 5 = -4 // -9 is negative, -4 is the closest to 0 of the negative remainders
```

* **When implementing a Deque we want a helper method to handle a negative number case**

