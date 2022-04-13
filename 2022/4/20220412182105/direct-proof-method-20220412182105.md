---
path: '/2022/4/direct-proof-method-20220412182105'
title: 'direct proof method'
date: '20220412182105'
category: 'discrete math'
tags: ['math', 'direct proof']
---

# direct proof method
A straightforward approach to establish theorems that doesn't require knowledge of any
special techniques. Most mathematical theorems are conditional or biconditional
statements; or even if the statement isn't in a conditional form it has an equivalent.

The first step toward proving a theorem is to identify the underlying hypothesis and
conclusion. To then go further and prove the theorem, you assume that the hypothesis
is true and then uses it with other proven theorems to argue (logically) that
the conclusion is necessarily true.

* Theorem - mathematical statement that is true
* Proof - a rigorous argument that a theorem is true
* Formal proof - manipulates logic expressions via mechanical rules of inference
    * Computers produce formal proofs
* Informal proof - argument stated in natural language
    * The argument must still be rigorous and sound
    * Mathematicians produce "informal" proofs

## Basic definitions
* Definition of even integers - An integer `n` is **even** for some integer `k` such that `n = 2k`
* Definition of odd integers - An integer `n` is **odd** for some integer `k` such that `n = 2k + 1`
    * **Note:** The `n` and `k` between the examples are separate and not related.

Examples:
`4a^2b` is even as `4a^2b = 2(2a^2b) = 2k` where `k = 2a^2b`, `k` is some integer

`4a^2 + 4a + 1` is odd as `4a^2 + 4a + 1 = 2(2a^2 + 2a) + 1 = 2m + 1`, where `m = (2a^2 + 2a)`, `m` is some integer

* The above is using definitions above to simplify the equations then determine the state of the integer.

* Definition of real numbers - A real number `r` is **rational** if and only if, it can be expressed as a quotient
of two integers `p` and `q` as `r = p/q` with a nonzero denominator `q <> 0`
* A real number that is not rational is **irrational**

Examples:
`5.5 = 11/2` is a rational number
`3 * sqrt(2)` is an irrational number

* Definition of divides - if `n` and `d` are integers and `d <> 0` then `n` is **divisible** by `d`
(denoted by `d|n`) if, and only if, `n = dk` for some integer `k`
    * Read as "d divides n"

Example:
`3|(3a + 9b)` where `a` and `b` are integers.

And, `3a + 9b = 3(a + 3b) = 3k`, here `k` is some integer and `k = (a + 3b)`
* We're saying that `k` is divisible by `3`

## Direct proof method
* Most mathematical theorems ar econditional or biconditional statements
* The vast majority to be proved are universal.

In discussing how to prove the statements, it is helpful to use the standard form:
`∀ x in D, if p(x) then q(x)`

## Conditional statements with the direct proof method
The most straightforward way to prove a statement is the direct proof method.

**A direct proof to show:** `∀ x in D, if p(x) then q(x)`
1. **Supposition:** assume that `p(x)` is true. [**Goal:** you must show that `q(x)` is true]
1. Using the assumption `p(x)` (and other true facts, definitions, theroems) we can argue that
`q(x)` must also be true
1. **Conclusion:** You can then conclude that the statement is true

Example:
Prove the following statement - "for all integers `n`, if `n` is odd, then `n^2` is odd"

* Assume that `n` is odd. [our goal is to show that `n^2` is odd]
* Since `n` is odd, then for some integer `k`, `n = 2k + 1` (by definition of odd integers)
* By substitution we get:

```
n^2 = (2k + 1)^2

(2k)^2 + 2 * 2k * 1 + (1)^2

4k^2 + 4k + 1

2(2k^2 + 2k) + 1 (by algebra)
```

Let `m = 2k^2 + 2k`
* Since integers are closed under addition and multiplication operations, then `m` is an integer
* So, `n^2 = 2m + 1` therefore, `n^2` is odd (by definition of odd integers)

* Thus, the statement "for all integers `n`, if `n` is odd, then `n^2` is odd" is true


Example:
Prove the statement - "The difference of two rational numbers is rational"

Restated - "For all real numbers `r` and `s`, if `r` and `s` are rational, then `r - s` is rational"

Proof with the direct method:
* Suppose that `r` and `s` are rational numbers. [We must show that `r-s` is rationa]
* Let `r = a/b` and `s = c/d`, where `a,b,c,d` are some integers, and `b<>0, d<>0` (by definition of rational numbers)
* By substitution we get:
```
r - s = a/b - c/d

= (ad - bc) / bd (by algebra)
```

* Let `p = ad - bc` and `q = bd` and `p` and `q` are integers because products and difference
of integers are integers. Also, `q <> 0` (by the zero-product property, since `b<>0, d<>0`)

Hence, `r - s = p/q`, where `p` and `q` are integers and `q <> 0`
* Therefore, `r - s` is rational, proving the statement

## Proving biconditional statements with the direct proof method
* Utilizing a direct proof to prove the biconditional statements
`∀ x in D, p(x) if and only if q(x)`

1. Write two separate proofs, one for each direction of the statement
    1. `∀ x in D, if p(x) then q(x)`
    1. `∀ x in D, if q(x) then p(x)`
1. Clearly state which direction you are proving
1. Conclude that having proved both directions, the statement holds

Example:
Prove the biconditional statement - "for all integers `n`, `n` is even if and only if `n^3 + 3` is odd"

* We first prove the "if" part: "if `n` is even, then `n^3 + 3` is odd"
* Assume that `n` is even. [Our goal is to show that `n^3 + 3` is odd]
* Since `n` is even, we can write `n = 2k` for some integer `k` (by definition of even)
* By substitution and algebra:

```
n^3 + 3 = (2k)^3 + 3 = 8k^3 + 2 + 1 = 2(4k^3 + 1) + 1
```

* Let `m = (4k^3 + 1)`. `m` is some integer since integers are closed under addition and multiplication operations.
* So, `n^3 + 3 = 2m + 1`. Therefore, `n^3 + 3` is odd (by definition of odd integers)

* We next prove the "only if" part: "for all integers `n`, if `n^3 + 3` is odd, then `n` is even"
* We prove this part by contraposition

## Direct proof method using cases
Sometimes it is very difficult to prove the whole theorem at once, in that situation the
original theorem statement is divided into a number of separate pieces (cases) to
be proven separately.
`∀ x in D, p1(x) V p2(x) ... V pn(x), then q(x)`

1. Assume that each `pi(x), 1 <= i <= n` is true. Your goal is to show `q(x)` is true
1. Using the assumption `pi(x)` (and other true facts, etc.) argue that `q(x)` must also be true
* Conclude that `∀ x in D, p1(x) V p2(x) ... V pn(x), then q(x)` is true
    * We must make sure **all** possible cases are covered, not just some

Example:
Prove the statement - "for all integers `n`, `4 | 3 + (-1)^n(2n + 1)`"

Restated:
"for all integers `n`, if `n` is even or `n` is odd, then `4 | 3 + (-1)^n(2n + 1)`"

**Using method by cases**
* Let `n` be an integer. There are 2 cases for `n` which are `n` is even or `n` is odd

**Case 1:**
* Assume `n` is even
* Since `n` is even, we can write `n = 2k` for some integer `k` (by definition of even integers)
* by substitution we get:

```
3 + (-1)^n(2n + 1)
= 3 + (-1)^2k(2(2k) + 1)
= 3 + (1)(4k + 1)
= 3 + 4k + 1
= 4 + 4k
= 4(1 + k)
```
* Also, since `k` is some integer, and `(-1)^2k = 1`

* Let `r = (k + 1)`. `r` is some integer since integers are closed under the addition operation
* So, `3 , (-1)^n(2n + 1) = 4r`, where `r` is some integer.
* Therefore, it is divisible by `4` (by definition of divides)

**Case 2:**
* Assume that `n` is odd
* Since `n` is odd, we can write `n = 2k + 1` for some intger `k` (by definition of odd)
* By substitution and algebra:

```
3 + (-1)^n(2n + 1)
= 3 + (-1)^(2k + 1)(2(2k + 1) + 1)
= 3 + (-1)(2(2k + 1) + 1)
= 3 + (-1)(4k + 2 + 1)
= 3 + (-1)(4k + 3)
= 3 - 4k - 3
= -4k
= 4(-k) (by algebra)
```
* Also, since `k` is some integer, and `(-1)^(2k+1) = -1`

* Let `r = -k`. `r` is some integer since the negative of an integer is also an integer

* So, `3 + (-1)^n(2n + 1) = 4r`, where `r` is some integer.
* Therefore, the statement is divisible by 4 (by definition of divides)

**Wrapping up** For all cases `3 + (-1)^n(2n + 1)` is divisible by 4, it is true

