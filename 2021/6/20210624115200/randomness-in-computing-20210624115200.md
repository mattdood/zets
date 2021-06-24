---
path: '/2021/6/randomness-in-computing-20210624115200'
title: 'randomness in computing'
date: '20210624115200'
category: 'dsa'
tags: ['randomness']
---

# randomness in computing
Randomness is a concept to model real-world phenomena like a coin flip or dice roll.

If we flip a coin we know that the probability of an outcome is 1/2.

However, in computing we would have to model the behavior as a computer would.

Computers operate in a **deterministic way**, they execute things the same way
every time, predictably. How do we get randomness out of predictability?

Can things be *truly random* in a predictable world?

*Would randomness help computation?* If we have access to it, can solutions to
problems be "better" than purely deterministic ones? Faster? More accurate?

## Accessing randomness in computation
An example using a **random number generator (RNG)** uses a **Pseudo-RNG (PRNG)**
which generates numbers in a completely deterministic way that appears random
for most apps.

Usually they have a base number called a *seed* that is used in large and complex
arithmetical operations to "spread" the numbers in order to appear random.

The problem is that because it is dterministic, if you know the seed and model
you can reverse-engineer the randomness of PRNG.

Some RNGs make use of real-world phenomena that are very complex (ex. atmospheric noise
or thermal fluctuations in the air) as a source of randomness. Whether it is
truly random may still be a valid question. Though reverse-engineering it is impossible.

## Usefulness of randomness in computing
An example would be determining if a number is prime. There was a deterministic
solution found, but it is much more difficult and inefficient to implement.

For many problems randomness plays a key role in **efficiency**.

