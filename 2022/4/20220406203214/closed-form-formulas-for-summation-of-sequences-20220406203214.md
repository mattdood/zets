---
path: '/2022/4/closed-form-formulas-for-summation-of-sequences-20220406203214'
title: 'closed form formulas for summation of sequences'
date: '20220406203214'
category: 'discrete math'
tags: ['math', 'summations', 'sequences', 'closed form formulas']
---

# closed form formulas for summation of sequences
There are quite a few useful closed form formulas for summation of sequences. These
are for different types of sequence progression (arithmetic, geometric, exponential, etc.).

## Arithmetic progression
```latex

\sum_{k=1}^n k = ((n+1) * n)/2

```

## Geometric progression
```latex

\sum_{k=0}^d r{k} = (r{n+1} - 1)/(r - 1)

```

## Exponential progression
```latex

\sum_{k=1}^n k{2} = ((n * (n + 1) * (2n + 1))/6)

```

## Arbitrary powers progression
```latex

\sum_{k=j}^n r{k} = ((r{n + 1} - r{j})/(r - 1))

```

## Splitting two summations
If we have two or more summations together with the same constants we can
handle them separately.

```latex

\sum_{k=m}^n (a_k + b_k) = \sum_{k=m}^n a_k + \sum_{k=m}^n b_k

```

## Multiplying by a constant factor
When multiplying we can pull the factor out then multiply afterward.

```latex

\sum_{k=m}^n ca_k = c * \sum_{k=m}^n a_k

```

## The sum of constant terms
When utilizing a constant we can determine the summation of the constant's terms
by utilizing the below.

```latex

\sum_{k=m}^n c = c(n - m + 1)

```

## Subtracting extra terms
We can subtract the extra terms from one summation to get another summation.

```latex

\sum_{k=m}^n a_k = \sum_{k=1}^n a_k - \sum_{k=1}^m-1 a_k

```

Example:
We can determine the summation of the below by creating 2 summations, then subtracting
the difference.

```latex

\sum_{k=5}^10 k = \sum_{k=1}^10 k - \sum_{k=1}^4 k

```

The above is now transformed to the closed forms:
```
= (10(10 + 1))/2 - (4(4 + 1))/2
```

## Adding or subtracting numbers to indexes/limits to work with it easier
We can change the values of our upper/lower limits by a constant (the same for each)
to make the value of the total easier to work with.

```latex

\sum_{k=m}^n a_k = \sum_{j=m+l}^n+l a_{j-l}

```

Example:

```latex

\sum_{k=5}^10 k, Say j = k - 4, k=j + 4

```

```latex

\sum_{j=1}^6 (j + 4) = \sum_{j=1}^6 j + \sum_{j=1}^6 4

```

The above is now:
```
= (6(6 + 1))/2 + 4 * (6 - 1 + 1)
```

## The telescoping sum in summations
If a summand can be expressed as a difference of two terms, then we can have
a cascade of cancellations that greatly simplifies our end formula.

```latex

\sum_{k=1}^n (a_k - a_{k+1}) = a_1 - a_{n+1}

```

**Note:** We can rewrite our summands to reach this.

Example:
```latex

\sum_{k=1}^n (1/(n(n+1)))

= \sum_{k=1}^n ((1/n) - (1/(n + 1)))

= (1/1 - 1/2) + (1/2 - 1/3) + (1/3 - 1/4) + ... + (1/(n-1) - 1/n) + (1/n - (1/(n + 1)))

```

## Exploring double sums, nested summations
These are similar to nested for loops. We have to compute the inner summation, then
calculate the outer summation.

```latex

\sum_{i=1}^n \sum_{j=1}^m a_{ij} = \sum_{i=1} a_{i1} + a_{i2} + ... + a_{im}

```

Example:

```

\sum_{i=1}^3 \sum_{j=1}^2 ij = \sum_{i=1} (i * 1 + i * 2) = \sum_{i=1}^3 3i = 3 * 3(3 + 1)/2 = 18

```

