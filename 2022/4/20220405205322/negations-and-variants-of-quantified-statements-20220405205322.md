---
path: '/2022/4/negations-and-variants-of-quantified-statements-20220405205322'
title: 'negations and variants of quantified statements'
date: '20220405205322'
category: 'discrete math'
tags: ['math', 'quantified statements']
---

# negations and variants of quantified statements

## Negation of a universal statement
A universal statement is formally defined as:
`∀ x ∈  D, p(x)`

Where `p(x)` is a predicate and the domain of `x` is `D`.

Negation example:
This can be read as "it is not the case that for all `x` in `D`, `p(x)` is true"
* There is at least 1 statement with the predicate negated

`∃ x ∈ D such that ~p(x)`
* Symbolically, this would be `~(∀ x ∈ D such that ~p(x)) == ∃ x ∈ D such that ~p(x)`

Example:
"All dogs are friendly"

* `p(x)` = "x is friendly"
* `D` = all dogs

Formally, `∀ x ∈  D, p(x)`

The formal negation is: `∃ x ∈ D such that ~p(x)`
* "There is a dog in `D` such that `~p(x)`"
* "There is a dog that is not friendly"
* "Some dogs are not friendly"

**Note:** Negating an universal statement changes the qualifier and takes the negation of the
predicate.

## Negation of an existential statement
An existential statement is formally defined as:
`∃ x ∈ D such that p(x)`

Where `p(x)` is a predicate and the domain of `x` is `D`.

Negation example:
This can be read as "for all x, `p(x)` is false" or "there is not an `x` that exists that is true"

`∀ x ∈  D, ~p(x)`
* Symbolically, this would be `~(∃ x ∈ D such that p(x)) == ∀ x ∈  D, ~p(x)`

**Note:** Negating an existential statement changes the qualifier and takes the negation of the
predicate.

Example:
"there exists a question that is easy"

* `s(x)` = "x is easy"
* `D` = "all questions"

Formally, `∃ x ∈ D such that s(x)`

The formal negation is: `∀ x ∈  D, ~s(x)`
* "No questions are easy" or "all questions are not easy"

## De Morgan's laws for negations of quantified statements

Universal statements:
* `~(∀ x ∈ D such that ~p(x)) == ∃ x ∈ D such that ~p(x)`

Existential statements:
* `~(∃ x ∈ D such that p(x)) == ∀ x ∈  D, ~p(x)`

We basically just swap the existential/universal quantifier and negate te predicate.

## Negating a universal conditional statement
A universal conditional statement is of the form:
`∀ x, if p(x) then q(x)`

The negation of a universal conditional statement is formally defined as:
`∃ x such that p(x) ^ ~q(x)`

* Remember that the only way a universal conditional statement is `False` is to have
a `True` hypothesis with a `False` conclusion

* Symbolically, the logical equivalence is:
`~(∀ x, if p(x) then q(x)) == ∃ x such that p(x) ^ ~q(x)`

Example:
"If a function is differentiable, then it is continuous"

* `p(x)` = "x is differentiable"
* `q(x)` = "x is continuous"
* `F` is the set of all functions

Formally, `∀ x, if p(x) then q(x)`

The formal negation is: `∃ x such that p(x) ^ ~q(x)`
* "There is at least one function that is differentiable but not continuous"
* "Some differentiable functions are not continuous"

## Negation of an existential statement with conjunction
An existential with conjunction can be expressed as:
`∃ x such that p(x) ^ q(x)`

The negation of an existential statement is formally defined as:
`∀ x, if p(x) then ~q(x)`

* Symbolically, the logical equivalence is:
`~(∃ x such that p(x) ^ q(x)) == (∀ x, if p(x) then ~q(x))`

Example:
"Some monkeys can speak French"

* `m(x)` = "x is a monkey"
* `f(x)` = "x speaks French"

Formally, `∃ x such that m(x) ^ f(x)`

The informal negation is: `(∀ x, if p(x) then ~q(x))`
* "All monkeys can not speak French"

## Variants of universal conditional statement
We know the most common variants of conditional statements, these definitions
can be extended to universal conditional statements also.

Given the universal conditional statement of:
`∀ x ∈ D , if p(x) then q(x)`

* Contrapositive - `∀ x ∈ D , if ~q(x) then ~p(x)`
* Converse - `∀ x ∈ D , if q(x) then p(x)`
* Inverse - `∀ x ∈ D , if ~p(x) then ~q(x)`

Example:
Given -
`∀ x ∈ R , if x > 3 then x^2 > 9`

* `p(x)` = "x > 3"
* `q(x)` = "x^2 > 9"

Contrapositive:
* `∀ x ∈ R , if ~q(x) then ~p(x)`
* "if a square of a real number is less than or equal to 9, then the number is
less than or equal to 3"

Converse:
* `∀ x ∈ D , if q(x) then p(x)`
* "if the square of a real number is greater than 9, then the number is greater than 3"

Inverse:
* `∀ x ∈ D , if ~p(x) then ~q(x)`
* "if a real number is less than or equal to 3, then the square of the numbe ris less
than or equal to 9"

## Necessary condition
The definitions of necessary, sufficient, and only-if conditions can be extended to apply
to universal conditional statements.

Given the sentence:
`∀ x ∈ D, r(x) is a necessary condition for s(x)`

Can be rewritten as:
`∀ x ∈ D, if ~r(x) then ~s(x) == ∀ x ∈ D, if s(x) then r(x)`

Example:
"Passing a comprehensive exam is a necessary condition for obtaining a master's degree"

* `m(x)` = "x obtains a master's degree"
* `r(x)` = "x passes a comprehensive exam"
* `D` = set of all persons

Formally rewritten as: `∀ x ∈ D, if ~r(x) then ~m(x)`
* Informally, "if a person does not pass a comprehensive exaxm then he/she does not obtain
a master's degree"
* `== ∀ x ∈ D, if m(x) then r(x)`
* Informally, "if a person obtains a master's degree then he/she passes a comprehensive exam"

## Sufficient condition
Given the sentence:
`∀ x ∈ D, r(x) is a sufficient condition for s(x)`

Can be rewritten as:
`∀ x ∈ D, if r(x) then s(x)`

Example:
"Squareness is a sufficient condition for rectangularity"
* `p(x)` = "x is a square"
* `q(x)` = "x is a rectangle"
* `F` = set of all plane figures

Formally rewritten as: `∀ x ∈ D, if p(x) then q(x)`
* Informally, "if a plane figure is a square, then it is a rectangle"

## Only if
Given the sentence:
`∀ x ∈ D, r(x) only if s(x)`

Can be rewritten as:
`∀ x ∈ D, if r(x) then s(x) == x ∈ D, if ~s(x) then ~r(x)`

Example:
Given a statement -
"A number is prime only if it is greater than 1"

* `s(x)` = "x is prime"
* `r(x)` = "x is greater than 1"
* `D` = set of all numbers

Formally rewritten as: `∀ x ∈ D, if r(x) then s(x)`
* Informally, "if a number is prime, then it is greater than 1"
* ` == x ∈ D, if ~s(x) then ~r(x)`
* Informally "if a number is less than or equal to 1, then it is not prime"

