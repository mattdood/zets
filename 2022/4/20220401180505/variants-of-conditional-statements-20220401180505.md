---
path: '/2022/4/variants-of-conditional-statements-20220401180505'
title: 'variants of conditional statements'
date: '20220401180505'
category: 'discrete math'
tags: ['math', 'conditional statements']
---

# variants of conditional statements
Statements can have conditional relationships that are true in both directions. This
is the case when a hypothesis causes the conclusion, but may be true that if the
conclusion occurred first then the hypothesis could result.

This can be said for the opposite of a hypothesis and conclusion happening.

If a combination of both the converse and inverse happens, it is contrapositive.

* Converse - The concept of a hypothesis/conclusion causing one another's result in
a given direction
* Inverse - The opposite of a hypothesis and conclusion
* Contrapositive - Combination of the converse and inverse results

## Contrapositive
The contrapositive of a conditional statement `if p then q` is obtained by both
**negating** and **exchanging the hypothesis and conclusion**.

In statement form:
`p -> q` is `~q -> ~p`

**Note:** A conditional statement is logically equivalent to its contrapositive.
This is often easier to utilize and prove.

Example:
Write a contrapositive.

"If a number is divisible by 9, then the number is divisible by 3"

`p` = "the number is divisible by 9"
`q` = "the number is divisible by 3"

Statement form:
`p -> q`

Contrapositive form:
`~q -> ~p`

"If the number is not divisible by 3, then it is not divisible by 9"

### Compound statements in contrapositives
A compound statement can utilize De Morgan's laws to break it down into components
for determining negations.

Example:
Find the contrapositive.

"If n is prime, then n is odd or n is 2"

`p` = "n is prime"
`q` = "n is odd"
`r` = "n is 2"

Statement form:
`p -> (q V r)`

Equivalent contrapositive:
`~(q V r) -> ~p`

With De Morgan's law:
`(~q ^ ~r) -> ~p`

"If n is not odd and n is not 2, then n is not prime"

## Converse of a conditional statement
The converse of a conditional statement `if p then q` is obtained by **exchanging
the hypothesis and conclusion**.

Symbollically:
`p -> q` is `q -> p`

**Note:** A conditional statment and its converse are ***not*** logically equivalent.

Example:
The converse of the following.

"If it walks like a duck and it talks like a duck, then it is a duck"

`p` = "it walks like a duck"
`q` = "it talks like a duck"
`r` = "it is a duck"

`(p ^ q) -> R`

Converse:
`r -> (p ^ q)`

"If it is a duck, then it walks like a duck and it talks like a duck"

## Inverse of a conditional statement
The inverse of a conditional statement of the form `if p then q` is obtained
by **negating the hypothesis and conclusion**.

Symbolically:
`p -> q` is `~p -> ~q`

**Note:** A conditional statement and ***its inverse*** are **not** logically equivalent.
**Note:** The converse and the inverse of a conditional statement **are** logically equivalent.

Example:
Write the inverse for the following.

"If n is prime, then n is odd or n is 2"

`p` = "n is prime"
`q` = "n is odd"
`r` = "n is 2"

`p -> (q V r)`

Inverse:
`~p -> ~(q V r)`
`~p -> (~q ^ ~r)` by De Morgan's law

"if n is not prime, then n is not odd and n is not 2"

## Only if form
If `p` and `q` are statement variables, "`p` only if `q`" means "if not `q` then not `p`",
or equivalently "if `p` then `q`".

If `p` occurs, then `q` must also occur.

Example:
Write the equivalent if-then statement.

"Today is Thanksgiving only if tomorrow is Friday"

`p` = "Today is Thanksgiving"
`q` = "Tomorrow is Friday"

Equivalent versions:
* "If today is Thanksgiving, then tomorrow is Friday"
* "If tomorrow is not Friday, then today is not Thanksgiving"

## Biconditional statement
This is a combination of a conditional statement and its converse.

Given statement variables `p` and `q`, the biconditional of `p` and `q` is
`p if, and only if, q` or `p iff q` and is denoted by `p <-> q`.

* It is true if both `p` and `q` have the same truth values and is false if
`p` and `q` have opposite truth values

Truth table:
| p | q | p <-> q |
|---|---|---------|
| T | T |    T    |
| T | F |    F    |
| F | T |    F    |
| F | F |    T    |

Knowing this, then `p <-> q` has the same truth values as `(p -> q) ^ (q -> p)`.
This is the converse of the conditional statement.

**Note:** This equivalence is very important for converting complex forms with biconditionals
to convert them into simpler forms.

Example:
Write the equivalent statement as a conjunction of two if-then statements.

"This integer is even if, and only if, it equals twice some integer"

`p` = "This integer is even"
`q` = "This integer equals twice some integer"

"If this integer is even, then it equals twice some integer and if this integer
equals twice some integer, then it is even"

* In order of operations `<->` is co-equal with `->`
    * As with `^ V` the only way to indicat eprecedence is with parentheses

