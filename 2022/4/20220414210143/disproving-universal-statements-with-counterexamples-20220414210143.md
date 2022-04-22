---
path: '/2022/4/disproving-universal-statements-with-counterexamples-20220414210143'
title: 'disproving universal statements with counterexamples'
date: '20220414210143'
category: 'discrete math'
tags: ['math', 'universal statements', 'counterexample']
---

# disproving universal statements with counterexamples
Disproof is the opposite of a proof, it shows that something is false rather than true.

Any statement that makes inferences about a set of numbers can be disproved by finding
a counterexample wherein the hypothesis is false. Also, there are erros that can
happen when writing proofs - which can be illustrated with counterexamples.

## Disproving a universal statement
A universal statement (below) is disproven when we show that the **negation**
of it is true.
`∀ x in D, if p(x) then q(x)`


If the negation (below) is true, then the universal statement is no longer proven.
`∃ x such that p(x) ^ ~q(x)`


Example:

`∀ real numbers a and b, if a^2 = b^2 then a = b`

Solution:
* To disprove this statement we need to find real numbers `a` and `b` such that
the hypothesis `a^2 = b^2` is true and the conclusion `a = b` is false
* The fact that both positive and negative integers have positive squares should
be used here
* Let `a = 1, b = -1`, then `a^2 = b^2 = 1` and `a^2 = b^2` but `a <> b`

The original statement is false.

## Common errors with counterexamples
* **Arguing from examples**
    * Examples are not sufficient to prove a general case
* **Using the same letter to mean 2 different things**
    * The same letter for 2 things is confusing, for example:
        * `m` is even, `m = 2k`
        * `n` is odd, `n = 2k + 1`
        * This now implies `m` and `n` are consecutive, shrinking the scope. Unless
        they are truly consecutive, we're assuming it is now `m + 1` which is no
        longer "general".
* **Making algebraic mistakes**
* Jumping to a conclusion
* Doing circular reasoning
* Making confusion between what is "known" and "what is still to be shown"
* Using the phrase "any" rather than "some"
* Misusing the word "if"

