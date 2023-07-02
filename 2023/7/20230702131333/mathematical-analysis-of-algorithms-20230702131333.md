---
path: '/2023/7/mathematical-analysis-of-algorithms-20230702131333'
title: 'mathematical analysis of algorithms'
date: '20230702131333'
category: 'algorithms'
tags: ['math', 'big-o', 'big-theta', 'big-omega']
---

# mathematical analysis of algorithms
Using big-O, theta, and omega notations to analyze time complexity of simple non-recursive
algorithms.

## Analysis of non-recursive algorithms
Consider finding the max number in an array of size `n` and we'll use it to outline
steps for time complexity.

Example `FindMax` algo:
```
FindMax(Arr):
    max = Arr[0]
    for i = 1 to n-1
        if A[i] > max
            max = Arr[i]
    return max
```

### Questions to ponder
* What is the parameter that impacts the executiont ime of the algorithm?
    * Array size of `n`
* What is the operation that will be executed most often in this algorithm?
    * The instructions in the for loop `if A[i] > max` and `max = Arr[i]`.
    * The comparison will execute for each iteration of the loop and the assignment
    will only be executed when the comparison is `true`.
    * That means the true answer is `if A[i] > max` will be executed the most.
    * Note: We didn't consider the loop while identifying the basic operation.
* Whether the size of comparisons will vary for differentarrays of size `n`?
    * The number of comparisons will be the same for all arrays of size `n`,
    so we don't need to distinguish between the worst/best/average case for this.
* Number of times the comparison is executed is `n-1`
