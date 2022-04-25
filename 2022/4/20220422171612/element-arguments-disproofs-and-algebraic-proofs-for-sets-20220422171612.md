---
path: '/2022/4/element-arguments-disproofs-and-algebraic-proofs-for-sets-20220422171612'
title: 'element arguments disproofs and algebraic proofs for sets'
date: '20220422171612'
category: 'discrete math'
tags: ['math', 'set theory', 'sets']
---

# element arguments disproofs and algebraic proofs for sets
It is possible to list many relations involving unions, intersections, complements, and
differences of sets. Some are true for all sets, others fail in some cases.

Establishing basic set properties using element arguments is important for disproving
a proposed set property (via counterexample). Algebraic techniques to derive
new properties can be used on known-true sets as well.

**Useful symbols:** ∈  ∉ ⊆ ⊂ ⊇ ⊃ ∅ ∪ ∩ ×

## Element arguments for set properties
* Element argument - The proof technique for establishing basic set properties
    * Shows a set to be a subset of another by demonstrating that every element
    in the set is available in another set
    * In math the element arguments are the standard method for relating sets
    * Often we use this instead of Venn diagrams because it is more rigorous

## Set properties
To construct rules for the set we need to know the procedural definitions of the
set operations.

Let `A, B` be subsets of a universal set `U` and suppose `x, y` are elements of `U`:
`x ∈ A ∪ B ↔ x ∈ A or x ∈ B`
`x ∈ A ∩ B ↔ x ∈ A and x ∈ B`
`x ∈ B - A ↔ x ∈ B and x ∉ A`
`x ∈ A^c ↔ x ∉ A`
`(x, y) ∈ A X B ↔ x ∈ A and y ∈ A`

## Proving a subset relation

Example:
"For sets `A, B` prove that `A ∩ B ⊆  A`"

The statement to be proved is universal -
for any subset A of B, prove that A is always a subset of B

`∀ sets A and B, A ∩ B ⊆  A`

Suppose that A and B are any (particular but arbitrarily chosen) sets

To show `A ∩ B ⊆  A`, we must show:
    `∀ x, x ∈ A ∩ B -> x ∈  A`

Where some arbitrary `x` is in the set intersection `A` and `B`, then that means `x` is in `A`

Suppose `x` is any (particular but arbitrarily chosen) element in `A ∩ B`

By definition of `A ∩ B`, our `x ∈  A` is true, meaning that `x ∈  B` as well.
Therefore, `x ∈  A`.

Finally, `A ∩ B ⊆  A` (proved to be true)

## Set identities
Just like in logic where we have identities/logical equivalences, we can use formulas
to derive identical meanings with sets and set operations.

The identities are very similar to logical identities.

**For all sets `A, B, C`:**
* Commutative laws: `A ∪ B = B ∪ A` and `A ∩ B = B ∩ A`
* Associative laws: `(A ∪ B) ∪ C = A ∪ (B ∪ C)` and `(A ∩ B) ∩ C = A ∩ (B ∩ C)`
* Distributive laws: `A ∪ (B ∩ C) = (A ∪ B) ∩ (A ∪ C)` and `A ∩ (B ∪ C) = (A ∩ B) ∪ (A ∩ C)`
* Identity laws: `A ∪ ∅  = A` and `A ∩ U = A`
* Complement laws: `A ∪ A^c = U` and `A ∩ A^c = ∅ `
* Double negative law: `(A^c)^c = A`
* Idempotent laws: `A ∪ A = A` and `A ∩ A = A`
* Universal bound laws: `A ∪ U = U` and `A ∩ ∅  = ∅ `
* De Morgan's Laws: `(A ∪ B)^c = A^c ∩ B^c` and `(A ∩ B)^c = A^c ∪ B^c`
* Absorption laws: `A ∪ (A ∩ B) = A` and `A ∩ (A ∪ B) = A`
* Complements of U and ∅ : `U^c = ∅ ` and `∅ ^c = U`
* Set difference law: `A - B = A ∩ B^c`

## Proving a set identity - using the subset property

Example:
"For any sets `A, B`, if `A ⊆ B` then `A ∩ B = A`"

To show that `A ∩ B = A`, we have to show:
1. `A ∩ B ⊆ A`
1. `A ⊆ A ∩ B`

Proving these:
1. `A ∩ B ⊆ A` is true by the inclusion of intersection property
1. `A ⊆ A ∩ B`
* Suppose that `x ∈ A` (arbitrarily chosen). We have to show that `x ∈ A ∩ B`
    * From `A ⊆ B`, then `x ∈ B` (by definition of subset relation)
    * From `x ∈ A` and `x ∈ B`, thus `x ∈ A ∩ B` (by definition of ∩)
    * So, `A ⊆ A ∩ B` is proven to be true

