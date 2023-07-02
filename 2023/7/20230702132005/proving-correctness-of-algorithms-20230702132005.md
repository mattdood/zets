---
path: '/2023/7/proving-correctness-of-algorithms-20230702132005'
title: 'proving correctness of algorithms'
date: '20230702132005'
category: 'algorithms'
tags: ['math', 'formal proofs']
---

# proving correctness of algorithms
Inspection of algorithms that produce the correct behavior over a broad range of inputs
is very important. We may run our algo for some sample input values to verify correctness,
but this only ensures this is true for the values that are tested (not all possible inputs).

## Verifying an algorithm
Empirical analysis cannot assure the correctness for all range of inputs, this would
be sampling for different types of input.

For example: To prove that a loop executes correctly, we want to show it works for
the first iteration, then for the second, etc. We also want to show the loop terminates
when it is supposed to (isn't infinite). This is similar to `mathematical induction`.
1. We will prove using induction that a "loop invariant", a property of the loop in the algo below, is always true
2. We will show that the algorithm terminates

### Loop invariant
The term `invariant` is "never changing or something that is always true".
For loops this would be something that's the same for every iteration of the loop.

The loop invariant here is `max`, which always holds the maximum number among the first `i` elements.
```
def findMax(list):
 max = list[0]
 for i from 0 to len(list)-1:
  if list[i] > max:
   max = list[i]
 return max
```

### Proof of correctness
Steps to determine the proof of correctness with loop invariants are described below.
These are only inclusive of loop invariants.

## Steps
1. Identify the loop invariant
1. Use induction to prove that the loop invariant holds true. For this, we need to prove
the following conditions:
    1. **Initialization (Base Case)** - The loop invariant is satisfied at the beginning of the for loop
    1. **Maintenance (Inductive Case)** - Assume that the loop invariant is true for the `ith` iteration,
    then show that the loop invariant will be true before the `(i + 1)th` iteration
    1. **Termination** - When the loop terminates, the invariant gives us a useful property that
    helps show that the algorithm is correct

#### Example proving a recursive algorithm
Proving recursive invariants is similar to loop invariants. We'll use strong induction
because it's easier for recursive structures at all levels.

This example computes `3^n` for a non-negative integer `n` using recursion:
```
ThreePower(n):
    if n = 0:
        return 1
    else if n mod 2 = 0: (i.e. n is even)
        x = ThreePower(n / 2)
        return x * x
    else: (if n is odd)
        x = ThreePower((n - 1) / 2)
        return 3 * x * x
```

##### Cases
* Base case - It is similar to what we have seen before:
    * We consider that the recursive invariant holds true for the base case of the recursive algorithm
* Inductive case - We assume that:
    * The recursive invariant is true for the `ith` execution
    * We also assume that is truef or all values less than `ith` (previous iterations),
    until the base case valuue (strong induction)
    * Then we want to show that the invariant is going to be true for the `(i + 1)th` execution
* Termination - When execution terminates, the invariant gives us a useful property

###### Proof
* Recursive invariant - At each recursive call, `ThreePower(k)` returns `3^k`
* Initialization (Base case) - When `k = 0`, `ThreePower(k)` returns `1 = 3^0` which is correct
* Maintenance (Inductive case):
    * We can divide this into 2 cases: `k` is even, `k` is odd
        * When `k` is even - Algorithm sets `x` to `ThreePower(k/2)`, which by recursion invariant returns `3^(k/2)`
            * The algorithm returns `x * x`, which is `3^(k/2) = 3^k`
        * When `k` is odd - Algorithm sets `x` to `ThreePower((k - 1)/2))`, which by recursion invariant returns `3^(k-1)/2`
            * The algorithm returns `3 * x * x` which is `3 * 3^(k-1)/2*3^(k-1)/2 = 3^k`
* Termination - At the top level of the recursive call, `ThreePower(n)` gives `3^n`, the solution to the problem
