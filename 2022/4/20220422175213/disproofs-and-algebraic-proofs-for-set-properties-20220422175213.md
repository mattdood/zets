---
path: '/2022/4/disproofs-and-algebraic-proofs-for-set-properties-20220422175213'
title: 'disproofs and algebraic proofs for set properties'
date: '20220422175213'
category: 'discrete math'
tags: ['math', 'set theory', 'sets']
---

# disproofs and algebraic proofs for set properties
If a proposed set property is false then we can discuss how to disprove a proposed
property. We will use the algebraic method for deriving new set properties from existing
set properties that are already known to be true.

**Useful symbols:** ∈  ∉ ⊆ ⊂ ⊇ ⊃ ∅ ∪ ∩ ×

## Disproving a set equality
* Disproving an alleged set property amounts to finding a single counterexample
for which the property is false

**Note:** We can use a Venn diagram to show a counter example. Alternatively,
we can construct a concrete example using set properties/laws.

Example:
Disprove that for all sets `A, B, C`
`(A - B) U (B - C) = A - C`?

The property is false, there are sets `A, B, C` for which the equality does not hold.

Counterexample:
`A = {1, 2, 4, 5}, B = {2, 3, 4, 5, 6}, C = {4, 5, 6, 7}`

`(A - B) U (B - C) = {1, 4} U {2, 3} = {1, 2, 3, 4}` and `A - C = {1, 2}`

`(A - B) U (B - C) <> A - C`

**Question:** How will you know that two sets aren't equal?
    * We don't know in advance. We first have to try proving the equality, then
    if we don't find it to be true we have to give a counterexample.

## Algebraic proofs of set identities
* Algebraic proofs - Use of laws to prove new identities without having to use the
element method of proving sets
    * We can prove that two sets are equal without having to use our element method
    strategies
    * This is similar to proving logical equivalence with laws in propositional logic

**These laws are the same as the other set laws:**
* Commutative laws: `A ∪ B = B ∪ A` and `A ∩ B = B ∩ A`
* Associative laws: `(A ∪ B) ∪ C = A ∪ (B ∪ C)` and `(A ∩ B) ∩ C = A ∩ (B ∩ C)`
* Distributive laws: `A ∪ (B ∩ C) = (A ∪ B) ∩ (A ∪ C)` and `A ∩ (B ∪ C) = (A ∩ B) ∪ (A ∩ C)`
* Identity laws: `A ∪ ∅  = A` and `A ∩ U = A`
* Complement laws: `A ∪ A^c = U` and `A ∩ A^c = ∅ `
* Double negative law: `(A^c)^c = A`
* Idempotent laws: `A ∪ A = A` and `A ∩ A = A`
* Universal bound laws: `A ∪ U = U` and `A ∩ ∅  = ∅ `
* De Morgan's Laws: `(A ∪ B)^c = A^c ∩ B^c` and `(A ∩ B)^c = A^c ∪ B^c`
* Absorption laws: `A ∪ (A ∩ B) = A` and `A ∩ B (A ∪ B) = A`
* Complements of U and ∅ : `U^c = ∅ ` and `∅ ^c = U`
* Set difference law: `A - B = A ∩ B^c`

Example:
"for all sets `A, B, C`, `(A U B) - C = (A - C) U (B - C)`"

`= (A U B) - C` (restated)
`= (A U B) ∩ C^c` (by set difference law)
`=  C^c ∩ (A U B)` (by commutative law for ∩ )
`=  (C^c ∩ A) U (C^c ∩ B)` (by distributive law)
`=  (A ∩ C^c) U (B ∩ C^c)` (by commutative law for ∩ )
`=  (A - C) U (B - C)` (by set difference law)

We've proven that the statement for the sets is true.
`(A U B) - C = (A - C) U (B - C)` is true

