---
path: '/2022/4/sequences-in-discrete-math-20220406195115'
title: 'sequences in discrete math'
date: '20220406195115'
category: 'discrete math'
tags: ['math', 'sequences']
---

# sequences in discrete math

## Sequences
* Sequence - A discrete structure used to represent an ordered list. There are no number
of initial terms in a sequence to determine for certain which sequence "we're dealing with",
there are ways to specify a sequence.
    * This is a function whose domain is a subset of integers.

Sequences are denoted by:
`am, am+1, am+2, ..., an`

or

`am, am+1, am+2, ...`

* Each individual element `ak` ("a sub k") is called a **term**
    * These exist at an **index** (position)

### Formulas to define sequences
* Explicit formula - A general formula for a sequence is a rule that shows how the values of `ak`
depend on `k`

### Sequences - Finite or infinite
* The **length** of a sequence is defined as the number of terms in the squence
* A sequence can be finite or infinite
    * Finite sequences have a fixed number of terms
        * Example: Sequence of 2-digit perfect square numbers
    * Infinite sequence will continue on infinitely. Every term is followed by
    a new term.
        * Example: Sequence of positive integers
        * Odd numbers, prime numbers, perfect square numbers, etc.

### Deriving terms of sequences
* Given an explicit formula for a sequence one can use a given value for the subscript
and obtain the value for the term at that point in the sequence
    * Example: Given the following, what are the first six terms.
    `ak = (5-k)/(5+k), for every integer k >= 1`
    Answer: `4/6, 3/7, 2/8, 1/9, 0, -1/11`

### Explicit formula for a sequence
Given initial terms, finding the formula can be difficult.
1. There is no single method
1. we have to observe the initial terms to derive a pattern
1. then we write the pattern given the terms of the index variable.

Example: Consider the sequence
`1/2, 2/3, 3/4, 4/5, ...`

The explicit formula for the sequence:
`ak = k/(k+1), for every integer k >= 1`

### Geometric progressions in sequences
The ratio between successive terms is constant. Typically looking like:
`a*r^0, a*r^1, ...`
`ak = a * r^k`

**Note:** If `r > 1` then increasing sequence, else decreasing sequence.

Example:
Start with $10 in bank at year 0 and double money each year.

`ak` is money at year `k`

`ak = 10 * 2^k, for every integer k >= 0`

### Arithmetic progressions in sequences
We increase at a given rate every interval, based on some arithmetic interval.

`a + d * 0, a + d * 1, ...`
`ak = a + d * k`

Example:
Start with $10 in bank at year 0 and add $20 each year.

`ak` is money at year `k`

`ak = 10 + 20 * k, for every integer k >= 0`

