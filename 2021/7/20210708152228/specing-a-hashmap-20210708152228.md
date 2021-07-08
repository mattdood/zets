---
path: '/2021/7/specing-a-hashmap-20210708152228'
title: 'specing a hashmap'
date: '20210708152228'
category: 'dsa'
tags: ['hashmap']
---

# specing a hashmap
Collisions are the source of most inefficiencies in hashmaps.

Collision resolution strategies are where most time is spent when working on a hashmap,
though having good planning reduces the need for the strategies.

## Picking a hash function
Formally, a hash function is `h: K -> Z`, which means a mapping from keys to integers.
This is necessary because keys might not be numerical like a phone number.

Ex: If the key is a string then we have to convert `String` -> `Integer`.

Technically we only require that if two keys *k1* and *k2* are equal then
the hash functions `h(k1)` and `h(k2)` are equal.

The reverse should be close to true also, if the hash function evaluations are equal,
then the keys are also equal. In some cases it is possible, in many
cases it may not be possible without infinite memory.

Example hash function:
Converting strings to integers based on a numeric value.

`ABAB` having a number assigned -> `1 + 2 + 1 + 2 = 6`

However, this does not respect the order of the letters so any string of length 4 with
A and B will collide.

A potential fix could be multiplying by powers of base 10 from right to left.

`1 x 10^3 + 2 x 10^2 + 1 x 10^1 + 2 x 10^0 = 1212`

## Additional considerations
Once a hash function is chosen we have to consider: **compression function, table
size, and load factor**.

* **Compression function** - to shrink and shift the output of the hash function to fit into the range backing table (array)
    * This is because for most application it is not reasonable to have a table of capacity of the largest hash function value
    * The most common compression is to mod by table length
* **Table size** - Compression uses a table size to "spread out" data in a range it is commont o have the table size be a prime number
    * Minimizes the number of collisiosn due to compression
    * Other choices exist but the prime number is a lazy attempt
    * Another common choice is a power of 2 because modulo then becomes much more efficient
* **Load factor** - defined as the `size / capacity` which determines how high we're willing to set the load before resizing
    * This varies in implementation but helps in reducing collisions
    * As load factor increases, the table will be inundated with entries and is more likely to have collisions
    * To keep the threshold of collisions low we can almost guarantee O(1) search time
    * More resizing will use more memory, so we have to balance

