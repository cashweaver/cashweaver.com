+++
title = "Quicksort implementation in Python"
author = ["Cash Weaver"]
date = 2022-06-30T13:57:00-07:00
lastmod = 2022-07-13T20:37:04-07:00
tags = ["concept", "concept"]
categories = ["concept"]
draft = false
+++

An implementation of [Quicksort]({{< relref "quicksort.md" >}}) in [Python]({{< relref "python.md" >}}).

```python
from typing import List, Callable

def swap(ints: List[int], indexA: int, indexB: int) -> None:
    """Swap the values in INTS at INDEXA and INDEXB."""
    valueA = ints[indexA]
    ints[indexA] = ints[indexB]
    ints[indexB] = valueA

def partition(ints: List[int], comparator: Callable[[int, int], bool], low_index: int, high_index: int) -> int:
    """Sorts sublist into [{<= pivot}, pivot, {> than pivot}]"""
    pivot_index = high_index
    i = low_index - 1

    for j in range(low_index, high_index):
        if comparator(ints[j], ints[pivot_index]):
            i += 1
            swap(ints, i, j)
    i += 1
    swap(ints, i, pivot_index)

    return i

def quick_sort_inner(ints: List[int], comparator: Callable[[int, int], bool], low_index: int, high_index: int) -> List[int]:
    if low_index >= high_index or low_index < 0:
        return

    pivot_index = partition(ints, comparator, 0, high_index)

    quick_sort_inner(ints, comparator, 0, pivot_index - 1)
    quick_sort_inner(ints, comparator, pivot_index + 1, high_index)

    return ints

def quick_sort(ints: List[int], comparator: Callable[[int, int], bool]) -> List[int]:
       return quick_sort_inner(ints, comparator, 0, len(ints) - 1)


a = [10, 5, 8, 2, 1, 3]
print(quick_sort(a, lambda a, b: a <= b))
```
