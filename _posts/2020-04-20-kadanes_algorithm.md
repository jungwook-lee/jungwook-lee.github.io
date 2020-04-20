---
layout: single
title:  "Kadane's Algorithm"
date:   2020-04-20
categories: algorithms
---
Also known as the maximum subarray problem.

## Problem
- **Idea**: find the maximum sum of a contiguous subarray

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/kadane-Algorithm.png)

## Algorithm
1. Keep a running sum of all the positive elements of the array: `current_sum`
2. Keep a variable to save the maximum possible value of sum of subarray: `max_sum`
3. If `current_sum` is negative, keep reset to zero.
4. If `current > best_sum`, update `best_sum`

```python
# Python program to find maximum contiguous subarray from wikipedia
def max_subarray(numbers):
  best_sum = 0
  current_sum = 0
  for x in numbers:
    current_sum = max(0, current_sum + x)
    best_sum = max(best_sum, current_sum)
return best_sum
```

## Sources
[geeksforgeeks](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/), [wikipedia](https://en.wikipedia.org/wiki/Maximum_subarray_problem)
