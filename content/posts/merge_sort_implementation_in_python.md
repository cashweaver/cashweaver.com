+++
title = "Merge sort implementation in Python"
author = ["Cash Weaver"]
date = 2022-07-01T11:44:00-07:00
lastmod = 2022-07-13T20:34:30-07:00
tags = ["concept", "concept"]
categories = ["concept"]
draft = false
+++

An implementation of [Merge sort]({{< relref "merge_sort.md" >}}) in [Python]({{< relref "python.md" >}}).

```python
import math
from typing import List, Callable, Tuple

def split(ints: List[int]) -> Tuple[List[int], List[int]]:
    if len(ints) <= 1:
        return ints, []

    split_index = math.floor(len(ints) / 2)

    return ints[0:split_index], ints[split_index:len(ints)]

def merge(a: List[int], b: List[int], comparator: Callable[[int, int], bool]) -> List[int]:
    a_index = 0
    b_index = 0
    out = []

    for _ in range(len(a) + len(b)):
        if a_index >= len(a):
            out.append(b[b_index])
            b_index += 1
            continue

        if b_index >= len(b):
            out.append(a[a_index])
            a_index += 1
            continue

        if comparator(a[a_index], b[b_index]):
            out.append(a[a_index])
            a_index += 1
        else:
            out.append(b[b_index])
            b_index += 1

    return out


def merge_sort(ints: List[int], comparator: Callable[[int, int], bool]) -> None:
    if len(ints) <= 1:
        return ints

    left, right = split(ints)
    left = merge_sort(left, comparator)
    right = merge_sort(right, comparator)

    return merge(left, right, comparator)

a = [10, 5, 2, 20, 1]
print(merge_sort(a, lambda x, y: x <= y))
```
