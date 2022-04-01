---
path: '/2022/3/truth-tables-for-logical-equivalence-20220331202056'
title: 'truth tables for logical equivalence'
date: '20220331202056'
category: 'discrete math'
tags: ['math', 'truth tables', 'logical equivalence']
---

# truth tables for logical equivalence

## Logical equivalence

Examples:
1. The grass is green and the sky is blue
1. The sky is blue and the grass is green

Any two statements where the logical forms are equivalent means that they would
both be either true or false.

| p | q | p^q | q^p |
|---|---|-----|-----|
| T | T |  T  |  T  |
| T | F |  F  |  F  |
| F | T |  F  |  F  |
| F | F |  F  |  F  |

The above shows that these two forms are logically equivalent.

## Definition
Two statement forms are logically equivalent if and only if they have identical
truth values for each possible subsitution of statements for their statement
variables.

The logical equivalence of statement forms P and Q is denoted by:
`P == Q` (equals with 3 lines)

### Testing logical equivalence
1. Construct a truth table with 1 column for truth values of `p` and another column
for the truth values of `q`
1. Check each combination of truth values of the statement variables for `p` is the same as `q`
    * If each row is the same as the truths of another, then they're logically equivalent
    * If some rows differ then they are not logically equivalent

### Showing equivalence
Construct a truth table to show that this is logically equivalent.

`p` is logically equivalent to `p^(pvq)`

| p | q | pvq | p^(pvq) |
|---|---|-----|---------|
| T | T |  T  |    T    |
| T | F |  T  |    T    |
| F | T |  T  |    F    |
| F | F |  F  |    F    |

**Note:** Column 1 and column 4 have the same truth values, these are logically equivalent.

### Showing nonequivalence
Construct a truth table to show that the pair is not logically equivalent.

`~(p v q)` and `~p v ~q`

| p | q | ~p | ~q | pvq | ~(pvq) | ~p v ~q |
|---|---|----|----|-----|--------|---------|
| T | T | F  | F  |  T  |    F   |    F    |
| T | F | F  | T  |  T  |    F   |    T    |
| F | T | T  | F  |  T  |    F   |    T    |
| F | F | T  | T  |  F  |    T   |    T    |

Because `~(pvq)` and `~p v ~q` have differing rows they are not logically equivalent.

## De Morgan's Laws
Augustus De Morgan, the first to state these two laws in mathematical terms.

1. The negation of an *and* statement is logically equivalent to the *or* statement
in which each component is negated.
    * `~(p ^ q) == ~p v ~q`
1. The negation of an *or* statement is logically equivalent to the *and* statement
in which each omponent is negated
    * `~(p v q) == ~p ^ ~q`

### Proving the first of the laws

1. The first of De Morgan's laws, proven. `~(p ^ q) == ~p v ~q`
`~(p ^ q)` and `~p v ~q` are logically equivalent

| p | q | ~p | ~q | p^q | ~(p^q) | ~p v ~q |
|---|---|----|----|-----|--------|---------|
| T | T | F  | F  |  T  |    F   |    F    |
| T | F | F  | T  |  F  |    T   |    T    |
| F | T | T  | F  |  F  |    T   |    T    |
| F | F | T  | T  |  F  |    T   |    T    |

## Tautologies and contradictions
1. Tautology - a statement that is always true regardless of the truth values of the statements
substituted for statement variables
1. Contradiction - a statement form that is always false regardless of substitutions for
statement variables

**Note:** This can be validated with a truth table.
* Tautology will have only `T` in the truth table.
* Contradiction will have only `F` in the truth table.

### Tautology truth table
Construct a truth table to show that the statement form is a tautology.

`(pvq) v (~p^~q)`

| p | q | ~p | ~q | pvq | ~p v ~q | (pvq) v (~p^~q) |
|---|---|----|----|-----|---------|-----------------|
| T | T | F  | F  |  T  |    F    |       T         |
| T | F | F  | T  |  T  |    F    |       T         |
| F | T | T  | F  |  T  |    F    |       T         |
| F | F | T  | T  |  F  |    T    |       T         |

The final column is all `T`, this is a tautology.

### Proving a tautology and contradiction
If `t` is a tautology and `c` is a contradiction, show:

`p ^ t == p` and `p ^ c == c`

| p | t | p^t | p | c | p^c |
|---|---|-----|---|---|-----|
| T | T |  T  | T | F |  F  |
| F | T |  F  | F | F |  F  |

`p^t` has the same truth values, so `p^t == p`
`p^c` has the same truth values, so `p^c == c`

