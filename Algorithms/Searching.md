
# Linear Search

## How Linear Search Works?

The following steps are followed to search for an element `k = 1` in the list below.

![./Algorithms/Attachments/Array to be searched for](linear-search-initial-array.webp)
1. Start from the first element, compare `k` with each element `x`.

![./Algorithms/Attachments/Compare with each element](linear-search-comparisons.webp)
2. If `x == k`, return the index.

![Algorithms/Attachments/Element found](linear-search-found.webp)
3.  Else, return `not found`.

```Python
# Linear Search in Python


def linearSearch(array, n, x):

    # Going through array sequencially
    for i in range(0, n):
        if (array[i] == x):
            return i
    return -1
```

## Complexity
- **Time complexity:** O(n)

---

# Binary Search

## How Binary Search Works?

![Algorithms/Attachments/Initial array](binary-search-initial-array.webp)
![Setting pointers](binary-search-set-pointers.webp)
![Algorithms/Attachments/Finding mid element](binary-search-mid.webp)
![Algorithms/Attachments/Mid element](binary-search-find-mid.webp)
![Algorithms/Attachments/Found](binary-search-mid-again.webp)

```Python
# Binary Search in python


def binarySearch(array, x, low, high):

    # Repeat until the pointers low and high meet each other
    while low <= high:

        mid = low + (high - low)//2

        if array[mid] == x:
            return mid

        elif array[mid] < x:
            low = mid + 1

        else:
            high = mid - 1

    return -1
```

## Complexity
-   **Best case complexity**: `O(1)`
-   **Average case complexity**: `O(log n)`
-   **Worst case complexity**: `O(log n)`
