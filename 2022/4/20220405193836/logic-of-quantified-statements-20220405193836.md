---
path: '/2022/4/logic-of-quantified-statements-20220405193836'
title: 'logic of quantified statements'
date: '20220405193836'
category: 'discrete math'
tags: ['math', 'quantified statements']
---

# logic of quantified statements
The idea of a quantifier is that it expresses how many of the values in the domain make
the claim to be `true`. The statements here use the following to express `true` over a range:
* all, some, many, none, and few

Quantified statements are used to express mathematics and complex logic in computer science.

## Predicates
* Predicate - a sentence that contains a finite # of variables and becomes a statement
when specific values are substituted for the variables

Example:
If the patient is an infant, then the patient has no children

Work:
assume "the patient" = "Alex"

Statement now becomes:
`AlexIsInfant -> ~AlexHasChild`

* This expression is only about Alex
* If we wanted to check this as some constraint for validation, we want to be able
to generalize this - not just have it against 1 patient
* This allows us to say `if any patient is an infant, then the patient has no children`
    * Propositional logic expressions can't express these broader statements
        * We need to make "arbitrary" patient statements

Revised statement:
* `p(x)` = predicate "x is an infant"
* `q(x)` = predicate "x has a child"

`p(Alex) -> ~q(Alex)`

Proposition based on predicate `p(x)`, proposition based on predicate `q(x)`
* Note: This statement is still about "Alex" and isn't be generalized

## Quantifiers

### Universal quantifier
`∀` is the universal quantifier and denotes "for all", "given any", "for any",
"for each", or "for every".

Working from the same example in the predicates section:
* `p(x)` is a predicate with domain of discourse `D`
    * `D` is the domain of `x`

A universal statement is a statement formally defined as:
`∀ x ∈  D, p(x)`

* `x` is restricted to `D`
* The statement is true of `p(x)` is true for all `x` in `D`
* The statement is false if `p(x)` is false for at least 1 `x` in `D`

Example:
Find the truth values of the following statements

`D = {1, 2, 3, 4, 5} `
`∀ x ∈  D, x^2 >= 1` this is `True`
    * All values in the domain are true for the statement

Using all real numbers:
`∀ x ∈  R, x^2 >= 1` this is `False`
    * Not all values are true, if `x = 1/2` then it yields `1/4 < 1`

### Existential quantifier
The symbol `∃` is the existential quantifier and denotes "there exists", "for soem",
"there is a", or "for at least one".

Example:
* `p(x)` is a predicate with domain `D`

An existential statement could be formally defined as:
`∃ x ∈ D such that p(x)`

* `x` is restricted to `D`
* It is true iff (if-and-only-if) `p(x)` is true for at least one `x` in `D`
* It is false iff `p(x)` is false for every `x` in `D`

Example:
Find the truth values of the following statements:

`∃ m ∈ Z, m^2 = m` this is `True`
    * We can determine that there would be at least 1 number that would exist that when squared makes this true

`E = {2, 3, 4, 5, 6}`
`∃ m ∈ Z, m^2 = m` this is `False`
    * Not a single one of these numbers satisfies the statement

### Universal conditional statements
These are used for defining theorems formally. These are a statement formally
written as:

`∀ x, if p(x) then q(x)` or `∀ x, (p(x) -> q(x))`

* This statement is only `False` if there exists a value `x` where the hypothesis is `True`
but the conclusion is `False`

Predicate variables aren't always used for rewriting conditional statements formally.
* **Note:** A pair of parentheses around the conditional statement makes things readable.

Example:
Rewrite the below statement.

"All CS students are required to take Data Structures"

* `c(x)` = "x is a CS student"
* `d(x)` = "x is required to take Data Structures"
* The domain `S` consists of all students

Rewritten, this is:
`∀ x ∈ S, if c(x) then d(x)` or `∀ x ∈ S, (c(x) -> d(x))`

## Translating english sentences to quantified statements
An existential statement of the form "Some p(x) are q(x)".

`∃ x such that p(x) ^ q(x)`

Example:
Rewrite the below.

"Some sunny days are windy"

* `s(x)` = "x is sunny"
* `w(x)` = "x is windy"
* `D` = set of all days

`∃ x ∈ D such that s(x) ^ w(x)`

### Common mistakes in translating sentences
1. Given "Some students in this class has have taken calculus"
    * `s(x)` = "x is a student in this class"
    * `c(x)` = "x has taken calculus"
    * `D` = students at the school
    * Improper statement would be:
        * `∃ x ∈ D, if s(x) then c(x)`
        * This is weaker, because it includes students that aren't in the class or haven't taken calculus
    * Proper form:
        * `∃ x ∈ D such that s(x) ^ c(x)`
        * This ensures it's students that are **in** the class that **have taken** calculus
1. "All horses are mammals"
    * `h(x)` = "x is a horse"
    * `m(x)` = "x is a mammal"
    * `D` = all living beings
    * Improper statement would be:
        * `∀ x ∈  D such that h(x) ^ m(x)`
        * Makes claim too tight as it is only true when every living being in the domain
        is both a horse and a mammal
    * Proper statement:
        * `∀ x ∈  D, if h(x) then m(x)`
        * Checking that it is a horse first, then implying it is a mammal

