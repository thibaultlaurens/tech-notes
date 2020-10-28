---
description: 'https://livebook.manning.com/book/grokking-algorithms'
---

# Grokking Algorithms

[Online version of the book.](https://livebook.manning.com/book/grokking-algorithms/table-of-contents/)

## 1. Introduction to Algorithms

### Binary Search

Binary search is an efficient algorithm for finding an item from a **sorted list of items**. It works by repeatedly **dividing in half** the portion of the list that could contain the item, until you've narrowed down the possible locations to just one. The time complexity is **O\(Log n\)**: for any list of n element, binary search will take log\(n\) steps.

Example with python 3:

```python
def binary_search(list, item):
    # keep track of which part of the list we search in
    start = 0
    end = len(list) - 1

    step = 0
    while (start <= end):
        # rounds the result down to the nearest whole number
        mid = (start + end) // 2
        guess = list[mid]
        print(f"Step {step}: guessing {guess} (index {mid}) in {list[start:end+1]}")

        # found the item
        if item == guess:
            print(f"Found {item} at index is {mid}")
            return mid

        # guess is too high
        if guess > item:
            end = mid - 1
        # guess is too low
        else:
            start = mid + 1

        step += 1
    return -1

sorted_list = [1,2,3,4,5,6,7,8,9,10]
binary_search(sorted_list, 9)
```

Output:

```text
Step 0: guessing 5 (index 4) in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Step 1: guessing 8 (index 7) in [6, 7, 8, 9, 10]
Step 2: guessing 9 (index 8) in [9, 10]
Found 9 at index is 8
```

### Big O notation

Big O notation tells how **fast** an algorithm **running time grows**. Big O notation is written `O(n)` where `O` means "Big O" and `n` is the number of operations.

Big O establishes **worst-case run time**: A simple / linear search algorithm \(a sequential search is made over all items one by on\) takes **O\(n\)** time to run. However, if the first entry match the search, it only took **O\(1\)**.

Some common Big O run times sorted from fastest to slowest:

* **O\(log n\)** also known as _log time_ \(ex: binary search\)
* **O\(n\)**: also known as _linear time_ \(ex: simple search\)
* **O\(n \* log n\)**: a fast sorting algorithm \(ex: quicksort, see chapter 4\)
* **O\(n^2\)**: a slow sorting algorithm \(ex: selection sort, see chapter 2\)
* **O\(n!\)**: a really slow algorithm \(ex: the traveling salesperson: he wants to hit a n number of cities while travelling the minimum distance\)

![](../.gitbook/assets/big-o-complexity-chart.jpeg)

## 2. Selection Sort

## 3. Recursion

## 4. Quicksort

## 5. Hash Tables

## 6. Breadth-first Search

## 7. Dijkstra’s algorithm

## 8. Greedy algorithms

## 9. Dynamic programming

## 10. K-nearest neighbors

## 11. Where to go next

