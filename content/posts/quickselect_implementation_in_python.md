+++
title = "Quickselect implementation in Python"
author = ["Cash Weaver"]
date = 2022-07-01T16:54:00-07:00
lastmod = 2022-07-13T20:35:35-07:00
tags = ["concept", "concept"]
categories = ["concept"]
draft = false
+++

An implementation of [Quickselect]({{< relref "quickselect.md" >}}) in [Python]({{< relref "python.md" >}}).

```python
from typing import List, Optional

def swap(ints: List[int], indexA: int, indexB: int) -> None:
    valueA = ints[indexA]
    ints[indexA] = ints[indexB]
    ints[indexB] = valueA

def partition(ints: List[int], left_index: int, right_index: int, pivot_index: int) -> int:
    """Partition the subsection of INTS from [LEFT_INDEX, RIGHT_INDEX].

    Values left of returned index will be less than the value at the returned index."""
    pivot_value = ints[pivot_index]
    swap(ints, pivot_index, right_index)

    i = left_index - 1
    for j in range(left_index, right_index):
        if ints[j] <= pivot_value:
            i += 1
            swap(ints, i, j)
    i += 1
    swap(ints, i, right_index)
    return i

def select_pivot_index(low: int, high: int) -> int:
    """Return a value between [low, high]."""
    return high

def select_nth_smallest_inner(ints: List[int], target_index: int, left_index: int, right_index: int) -> int:
    """Inner recursion for select_nth_smallest."""
    pivot_index = select_pivot_index(left_index, right_index)
    pivot_index = partition(ints, left_index, right_index, pivot_index)

    if pivot_index == target_index:
        return ints[pivot_index]

    if target_index < pivot_index:
        return select_nth_smallest_inner(ints, target_index, left_index, pivot_index - 1)

    return select_nth_smallest_inner(ints, target_index, pivot_index + 1, right_index)

def select_nth_smallest(ints: List[int], n: int) -> Optional[int]:
    """Return the N-th smallest value from a list of integers, INTS."""
    if n >= len(ints) || n < 0:
        return None

    return select_nth_smallest_inner(ints, n, 0, len(ints) - 1)

a = [10, 4, 2, 1, 5, 15]
# Expect to print "4": [1, 2, 4, 5, 10, 15]
print(select_nth_smallest(a, 2))
# Expect to print "10": [1, 2, 4, 5, 10, 15]
print(select_nth_smallest(a, 4))
```
