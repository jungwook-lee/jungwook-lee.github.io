---
layout: single
title:  "Binary Search"
date:   2020-04-21
categories: algorithms
---
Efficient search by dividing things by halves
![](https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/Binary_Search_Depiction.svg/1280px-Binary_Search_Depiction.svg.png)

# Problem
- Provide an efficient search algorithm for a sorted array.
  - The runtime is \\(O(\log(n))\\)
- Note the implementation matters for **space efficient** binary search!
  - Recursive version will yield \\(O(\log(n))\\) due to stack space.
  - You would ideally want to implement the iterative version \\(O(1)\\).
- **Idea**: Split the search space in halves.

# Implementation

```python
def binary_search(num, val):
    # returns the index of the val in num if it exists, else -1

    # Empty input array or invalid val
    if not num or val is None:
      return -1

    l, r = 0, len(num) - 1
    while l <= r:
        mid = (l + r) >> 1
        if num[mid] == val:
            return mid
        elif num[mid] < val:
            l = mid + 1
        else:
            r = mid - 1
    return -1
```

- Some Implementation Key points:
  - Note the midpoint calculation. More detail [here](https://ai.googleblog.com/2006/06/extra-extra-read-all-about-it-nearly.html)
  - The exit condition of while loop `l <= r`
  - Remember to move mid `left` or `right` when reselecting the left and right points
  - Remember to return failed search status

# Practice Problems
- Leetcode: [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

# Sources
[wikipedia](https://en.wikipedia.org/wiki/Binary_search_algorithm), [google ai blog](https://ai.googleblog.com/2006/06/extra-extra-read-all-about-it-nearly.html)
