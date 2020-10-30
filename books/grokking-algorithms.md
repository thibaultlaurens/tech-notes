---
description: An illustrated guide for programmers and other curious people.
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

- **O\(log n\)** also known as _log time_ \(ex: binary search\)
- **O\(n\)**: also known as _linear time_ \(ex: simple search\)
- **O\(n \* log n\)**: a fast sorting algorithm \(ex: quicksort, see chapter 4\)
- **O\(n^2\)**: a slow sorting algorithm \(ex: selection sort, see chapter 2\)
- **O\(n!\)**: a really slow algorithm \(ex: the traveling salesperson: he wants to hit a n number of cities while travelling the minimum distance\)

![](../.gitbook/assets/big-o-complexity-chart.jpeg)

## 2. Selection Sort

### Arrays and Linked Lists

Both Arrays and Linked Lists are **linear data structures**, but they have some advantages and disadvantages over each other.

Arrays:

- **Index based** data structure where each elements are associated with an index.
- They are stored in **sequential** memory location.
- They have a **fixed size**, specifided during declaration and allocated during compile time.
- Elements are accessed **directly** (specifying the element index), at **O(1)**.
- Insertion and deletion is relatively slow (as shifting is required), at **O(n)**.

Linked Lists:

- **Reference based** data structure where each node consists of the data and the reference to the next element.
- They are stored **randomly** in memory.
- They have a **variable** numbere of elements and grow and shrink during run time.
- Elements are accessed **sequentially** (traversing the node, starting from the first one) at **O(n)**.
- Insertion and deletion is fast, at **O(1)**.

### Selection Sort

Selection sort is a simple **in-place comparison-based** sorting algorithm. It has **O(n^2)** complexity. The list is divided into two parts, the sorted part at the left end and the unsorted part at the right end. Initially, the sorted part is empty and the unsorted part is the entire list.

The smallest element is selected from the unsorted array and **swapped** with the leftmost element, and that element becomes a part of the sorted array. This process continues moving unsorted array boundary by one element to the right.

Example with python 3:

```python
def selection_sort(list):
    print(f"Selection sort on: {list}")

    # range over all the array indexes
    for i in range(len(list)):
        min_idx = i

        # find the index of the smallest element in the remaining array
        for j in range(i+1, len(list)):
            if list[j] < list[min_idx]:
                min_idx = j

        # swap the smallest element with the current one
        list[i], list[min_idx] = list[min_idx], list[i]
        print(f"Swapped {list[i]} with {list[min_idx]}: {list}")

unsorted_list = [9,6,5,8,4,2,1,3,7]
selection_sort(unsorted_list)
```

Output:

```text
Selection sort on: [9, 6, 5, 8, 4, 2, 1, 3, 7]
Swapped 1 with 9: [1, 6, 5, 8, 4, 2, 9, 3, 7]
Swapped 2 with 6: [1, 2, 5, 8, 4, 6, 9, 3, 7]
Swapped 3 with 5: [1, 2, 3, 8, 4, 6, 9, 5, 7]
Swapped 4 with 8: [1, 2, 3, 4, 8, 6, 9, 5, 7]
Swapped 5 with 8: [1, 2, 3, 4, 5, 6, 9, 8, 7]
Swapped 6 with 6: [1, 2, 3, 4, 5, 6, 9, 8, 7]
Swapped 7 with 9: [1, 2, 3, 4, 5, 6, 7, 8, 9]
Swapped 8 with 8: [1, 2, 3, 4, 5, 6, 7, 8, 9]
Swapped 9 with 9: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

{% hint style="info" %}
Note: another simple sort algorithm is **insertion sort**. Insertion sort works by taking elements from the list one by one and inserting them in their correct position into **a new** sorted list. Insertion sort is generally faster than selection sort in practice, due to fewer comparisons and good performance on almost-sorted data, and thus is preferred in practice, but selection sort uses fewer writes, and thus is used when write performance is a limiting factor.
{% endhint %}

## 3. Recursion

## 4. Quicksort

## 5. Hash Tables

## 6. Breadth-first Search

## 7. Dijkstra’s algorithm

## 8. Greedy algorithms

## 9. Dynamic programming

## 10. K-nearest neighbors

## 11. Where to go next
