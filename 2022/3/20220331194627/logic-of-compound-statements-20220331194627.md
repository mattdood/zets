---
path: '/2022/3/logic-of-compound-statements-20220331194627'
title: 'logic of compound statements'
date: '20220331194627'
category: 'discrete math'
tags: ['math', 'compound statements']
---

# logic of compound statements
Logic is precise rather than ambiguous like natural languages. These are clear-cut
statements that are unambiguous.

Logic provides formal, structured language for writing proof strategies and statements.

## Propositional logic
Various types of logic exist in math and other disciplines.
    * First-order logic, modal logic, temporal logic, etc.

Propositional logic is composed of:
* Atomic statements
* Compound statements

### Statements/propositions
Statements and propositions are interchangeable, these are declarative sentences
that can be either TRUE or FALSE.
    * Can't be both TRUe and FALSE

Examples:
* "1 + 1 = 3"
* "Tom is a human"
* "1 + 1" - not a statement (not making a statement for an outcome)
* "x^2 = 4" - not a statement, we don't know about "x" and the TRUE value is dependent upon it

### Shorthand
Letters are typically used to denote statements:
* `p`, `q`, `r`, `s`
* `T`: True
* `F`: False

Example:
* Let `p` denote the statement "1 + 1 = 2"
* Let q denote the statement "1 + 1 = 3"

Now we know:
`p` is `T`
`q` is `F`

## Compound statements
Given a set of atomic statements, we can compose new statements with logical operations.

### Negation (not)
Let `p` be a statement. The **negation of `p`** is `~p`

The `~p` is pronounced "not p" and is a new statement

The truth value of `~p` is the opposite of `p`

Example:
Let `p` be "Tom is a human"

If `p` is `True` then `~p` is "Tom is not a human"

### Conjunction (and)
The **conjunction** of `p` and `q` is `p^q` (pronounced "p and q")

`p^q` is true if and only if **`p` and `q` are both true**

Example:
Let `p` be "Tom is a human", `q` be "Tom is tall"

`p^q` is "Tom is human and Tom is tall"

### Disjunction (or)
The **disjunction** of `p` and `q` is `p v q` (pronounced "p or q")

`p v q` is true if and only if **`p` is true or `q` is true`**

Example:
Let `p` be "Tom is a human", `q` be "Tom is tall"

`p v q` is "Tom is human or Tom is tall"

## Statement forms
A statement form is an expression made of statement variables and local operators

Examples:
Let `p` be "Bob is a CS student", `q` be "Bob is taking DS class"

`~p ^ q` "Bob is not a CS student and Bob is taking DS class"

`p v (~p ^ q)` "Either Bob is a CS student or Bob is not a CS student and Bob is taking DS class"

`~p ^ ~q` "Bob is not a CS student and Bob is not taking DS class"

**Note:** Truth tables show determinations of truths in statement forms

## Compound statements - truth tables
We can evaluate truth values of any complex statement form.
* Label columns accordingly, then fill in with steps
    * Add component variables
    * Add expressions in parentheses
        * Any non-nested parentheses are considered left->right
    * Add expressions with logical operators
        * Negation
        * Conjunction/disjunction

| p | ~p |
|---|----|
| T |  F |
| F |  T |

| p | q | p^q |
|---|---|-----|
| T | T |  T  |
| T | F |  F  |
| F | T |  F  |
| F | F |  F  |

| p | q | pvq |
|---|---|-----|
| T | T |  T  |
| T | F |  T  |
| F | T |  T  |
| F | F |  F  |

Example:
Construct the truth table for the statement form `(p v q) ^ ~(p ^ q)`

### Exclusive OR
Exclusive OR is denoted as `(p v q) ^ ~(p ^ q)`.

This is often abbreviated as `(p XOR q)`.

The statement `p XOR q` means `p or q and not both p and q`.

| p | q | pvq | p^q | ~(p^q) | (pvq) ^ ~(p^q) |
|---|---|-----|-----|--------|----------------|
| T | T |  T  |  T  |    F   |       F        |
| T | F |  T  |  F  |    T   |       T        |
| F | T |  T  |  F  |    T   |       T        |
| F | F |  F  |  F  |    T   |       F        |

