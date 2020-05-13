---
layout: single
title: "Quicksort"
date: 2020-05-13
categories: algorithms
---
Efficient sorting method using divide-and-conquer and pivots.

## Idea:
- `Divide-and-conquer` and `recursion`
- Utilize pivots (aka swaps) using `two-pointer` strategy
- In-place algorithm is most efficient space wise
- `queue` can be used, however space complexity is increased
- Runtime:
  - Average, Best: \\( O(n\log n)\\)
  - Worst: \\(O(n^2)\\)

## Algorithm:
1. (Base Case) Return if indices are same
2. Initialize pivot, left, right
3. Scan left to right for potential candidates
4. Scan right to left for potential candidates
5. Swap until left <= right
6. Swap pivot into right place
7. Recursion call to left (a, left-1) and right (left+1, b)

```python
def in_place_qsort(nums, a, b):
    # base case
    if a >= b:
        return
    pivot = nums[b]
    left = a
    right = b - 1

    while left <= right:
        while left <= right and nums[left] < pivot:
            left += 1
        while left <= right and nums[right] > pivot:
            right -= 1
        if left <= right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1

    # place pivot in right place
    nums[left], nums[b] = nums[b], nums[left]
    in_place_qsort(nums, a, left-1)
    in_place_qsort(nums, left+1, b)
    return nums


if __name__ == '__main__':
    from random import randint
    test = [randint(0, 100) for _ in range(10)]
    print(in_place_qsort(test, 0, len(test)-1))
```
