---
path: '/2022/4/logic-of-conditional-statements-20220401173843'
title: 'logic of conditional statements'
date: '20220401173843'
category: 'discrete math'
tags: ['math', 'conditional statements']
---

# logic of conditional statements
Conditional statements are a foundation of building logic. The "if this, then something"
is the basis of conditional statements. Another term for conditional statements is
a logical implication.

Example:
"if it rains tomorrow, then John will stay at home"

`p` = "it rains tomorrow"
`q` = "John will stay at home"

Statement form:
`if p then q`

Conditional statement (implication):
`p -> q`

This reads as "p implies q"

`p` is the hypothesis (antecedent)
`q` is the conclusion (consequent)

Truth table representation:

| p | q | p -> q |
|---|---|--------|
| T | T |    T   |
| T | F |    F   |
| F | T |    T   |
| F | F |    T   |

**Note:**
* When the hypothesis (`p`) of the conditional statement is true but the conclusion (`q`)
is false, the statement as a whole is false
* When the hypothesis (`p`) of the conditional statement is false, the statement as a
whole is true

## Equivalent sentences for conditional statements
A condition `p -> q` can be stated as:
* If `p` then `q`
* `p` implies `q`
* if `p`, `q`
* `p` only if `q`
* `q` if `p`
* `q` unless `~p`
* `q` when `p`
* `q` whenever `p`
* `q` follows from `p`
* `p` is a sufficient condition for `q` (`p` is sufficient for `q`)
* `q` is a necessary condition for `p` (`q` is necessary for `p`)

## Converting statements to logic
Note that some statements can be compound statements.

Example:
"You can access the Internet from campus only if you are not a freshman or you are a computer
science major"

Let:
`p` = "You can access the Internet from campus"
`q` = "You are a freshman"
`r` = "You are a computer science major"

The statement form is:
`p -> ~q V r`

Would actually be evaluated as:
`p -> ((~q) V r)`
* Evaluates negation first
* Then `(~q V r)`
* Then `p -> the result`

## Constructing a truth table
In expressions with `->` as well as other logical operators (`^ V ~`) the order
is that `->` is performed last.

Example:
`p V ~q -> ~p`

Is interpreted as `(p V (~q)) -> (~p)`

| p | q | ~q | ~p | p V ~q | p V ~q -> ~p |
|---|---|----|----|--------|--------------|
| T | T | F  | F  |   T    |      F       |
| T | F | T  | F  |   T    |      F       |
| F | T | F  | T  |   F    |      T       |
| F | F | T  | T  |   T    |      T       |

## Logical equivalence in conditional statements
The statements `(p -> q)` and `((~p) V q)` are logically equivalent.

Example:
"My car is not in the repair shop, or I will miss the class"

`~p` = "My car is not in the repair shop"
`q` = "I will miss the class"

Meaning:
`~p V q`

The equivalent `p -> q` is:
"If my car is in the repair shop then I will miss the class"

## Showing logical equivalence
It is possible to show that logical equivalence exists through truth tables
for conditional statements.

`p -> q` and `((~p) V q)` are logically equivalent

| p | q | ~p | p -> q | ~p V q |
|---|---|----|--------|--------|
| T | T | F  |   T    |   T    |
| T | F | F  |   F    |   F    |
| F | T | T  |   T    |   T    |
| F | F | T  |   T    |   T    |

## Determine negation of conditional statements
By definition `p -> q` is false if and only if its hypotehsis, `p` is true
and its conclusion, `q` is false.

`~(p -> q) == (p ^ (~q))`

Example:
"If you run 10 laps daily, then you will be healthy"

`p` = "If you run 10 laps daily"
`q` = "you will be healthy"

Statement:
`p -> q`

Negation:
`(p ^ (~q))`
"You run 10 laps daily and you will not be healthy"

### Logical equivalence in negation
It is possible to show that two statements `~(p -> q)` and `(p ^ (~q))` are
logically equivalent using known logical equivalences.

Using laws:
`~(p -> q) == ~(~p V q)`   by implication law
== `~(~p) ^ ~q`            by De Morgan's law
== `p ^ ~q`                by double negative law

