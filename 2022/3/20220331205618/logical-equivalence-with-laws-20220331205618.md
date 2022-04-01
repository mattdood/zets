---
path: '/2022/3/logical-equivalence-with-laws-20220331205618'
title: 'logical equivalence with laws'
date: '20220331205618'
category: 'discrete math'
tags: ['math', 'logical equivalence']
---

# logical equivalence with laws
We can explain logical equivalence using predetermined known truths/equivalences.

This is useful for creating ladder logic in computation.

We know that for every statement form we have 2^n number of truth table rows.
For statement forms with large numbers of variables this is not a good method.

To remedy this, we can transofrm a statement into an equivalent to reduce complexity.

## Simplifying statement forms
To simplify one statement form `p` to a desired equivalent `q`:
1. Take the statement form `p`
1. Continue making replacements until you obtain a statement form `q` on the right
    * On each step, use the laws to replace sections of the statement form by
    logically changing things

## List of known logical equivalences (laws)
These are a number of logical equivalences that are proven, which can be used to
reduce complexity.

* Commutative laws: `p^q == q^p` and `pvq == qvp`
* Associative laws: `(p^q) ^ r == p ^ (q^r)` and `(pvq) v r == p v (qvr)`
* Distributive laws: `p ^ (qvr) == (p^q) v (p^r)` and `p v (q^r) == (pvq) ^ (pvr)`
* Identity laws: `p ^ t == p` and `p v c == p`
* Negation laws: `p v ~p == t` and `p ^ ~p == c`
* Double negative law: `~(~p) == p`
* Idempotent laws: `p ^ p == p` and `p v p == p`
* Universal bound laws: `p v t == t` and `p ^ c == c`
* De Morgan's Laws: `~(p^q) == ~p v ~q` and `~(pvq) == ~p ^ ~q`
* Absorption laws: `p v (p^q) == p` and `p ^ (pvq) == p`
* Negations of t and c: `~t == c` and `~c == t`

## The order to apply logical equivalence laws
To simplify a statement form consists of statement variables and conjunction (^),
disjunction (v) and negation (~) operators:
* Push negations inward with De Morgan's laws and the double negation law until negations
appear only before statement variables
* Apply commutative, associative, and distributive laws to obtain the correct intermediate
forms
* Finally, simplify with absorption, universal bound, identity, idempotent, and
negation laws

**Example 1:**
To show that the statement form is logically equivalent to a tautology.

`~(p^q) v (pvq) == t`

Simplification:
`~(p^q) v (pvq)`
== `(~p v ~q) v (pvq)` (by De Morgan's law)
== `(p v ~q) v (q v ~q)` (by associative and commutative laws)
== `t v t` (by the negation law)
== `t` (by the idempotent law)

Therefore:
`~(p^q) v (pvq) == t` is logically equivalent

**Example 2:**
To show that the statement form is logically equivalent.

`(p v ~q) ^ (~p v ~q) == ~q`

Simplification:
`(p v ~q) ^ (~p v ~q) == ~q`
== `(~q v p) ^ (~q v ~p)` (by commutative law)
== `~q v (p ^ ~p)` (by the distributive law)
== `~q v c` (by the negation law)
== `~q` (by the identity law)

Therefore:
`(p v ~q) ^ (~p v ~q) == ~q` is logically equivalent

