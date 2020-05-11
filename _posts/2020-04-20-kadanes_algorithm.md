---
layout: single
title:  "Maximum Subarray"
date:   2020-04-20
categories: algorithms
---
Also known as the Kadane's algorithm.

# Problem
- **Idea**: find the maximum sum of a contiguous subarray
- **Properties**:
  - Dynamic Programming Paradigm
  - \\( O(n) \\) Runtime and \\(O(1)\\) Space

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/kadane-Algorithm.png)

# Algorithm
## Basic
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
## Return Indices
```python
def maximum_subarray_with_indices(nums):
    best_sum = 0
    best_start = best_end = 0
    cur_sum = 0

    for cur_end, x in enumerate(nums):
        if cur_sum <= 0:
            # start a new seqeunce
            cur_start = cur_end
            cur_sum = x
        else:
            # extend existing sequence with cur elem
            cur_sum += x

        if cur_sum > best_sum:
            # set best indices to max and range
            best_sum = cur_sum
            best_start = cur_start
            best_end = cur_end + 1  # note in python end index are exclusive
    return best_sum, best_start, best_end
```

# Sources
[geeksforgeeks](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/), [wikipedia](https://en.wikipedia.org/wiki/Maximum_subarray_problem)
