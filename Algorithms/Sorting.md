
# Selection Sort

```Python
# Selection sort in python

def selectionSort(array, size):

    for step in range(size):
        min_idx = step

        for i in range(step + 1, size):
         
            # to sort in descending order, change > to < in this line
            # select the minimum element in each loop
            if array[i] < array[min_idx]:
                min_idx = i
         
        # put min at the correct position
        (array[step], array[min_idx]) = (array[min_idx], array[step])
```

| Property | |
| ---- | --------------- |
| Best | $O(n^2)$ |
| Worst | $O(n^2)$ |
| Average | $O(n^2)$ |
| Space Complexity | $O(1)$ |
| Stability | No |

---

# Insertion Sort

```Python
# Insertion sort in python

def insertionSort(array):

    for step in range(1, len(array)):
        key = array[step]
        j = step - 1
        
        # Compare key with each element on the left of it until 
        # an element smaller than it is found
        # For descending order, change key<array[j] to key>array[j].        
        while j >= 0 and key < array[j]:
            array[j + 1] = array[j]
            j = j - 1
        
        # Place key at after the element just smaller than it.
        array[j + 1] = key
```

| Property | |
| -------- |-|
|Best|$O(n)$|
|Worst|$O(n^2)$|
|Average|$O(n^2)$|
|Space Complexity|$O(1)$|
|Stability|Yes|

---

# Merge Sort

![Algorithms/Attachments/Merge Sort example](merge-sort-example_0.png)

```Python
# MergeSort in Python


def mergeSort(array):
    if len(array) > 1:

        #  r is the point where the array is divided into two subarrays
        r = len(array)//2
        L = array[:r]
        M = array[r:]

        # Sort the two halves
        mergeSort(L)
        mergeSort(M)

        i = j = k = 0

        # Until we reach either end of either L or M, pick larger among
        # elements L and M and place them in the correct position at A[p..r]
        while i < len(L) and j < len(M):
            if L[i] < M[j]:
                array[k] = L[i]
                i += 1
            else:
                array[k] = M[j]
                j += 1
            k += 1

        # When we run out of elements in either L or M,
        # pick up the remaining elements and put in A[p..r]
        while i < len(L):
            array[k] = L[i]
            i += 1
            k += 1

        while j < len(M):
            array[k] = M[j]
            j += 1
            k += 1
```

| Property | |
| -------- |-|
|Best|$O(n \cdot log n)$|
|Worst|$O(n \cdot log n)$
|Average|$O(n \cdot log n)$
|Space Complexity|$O(n)$|
|Stability|Yes|

---

# Quicksort

Quicksort is [a sorting algorithm](https://www.programiz.com/dsa/sorting-algorithm) based on the **divide and conquer approach** where

1.  An array is divided into subarrays by selecting a **pivot element** (element selected from the array).  
	
    While dividing the array, the pivot element should be positioned in such a way that elements less than pivot are kept on the left side and elements greater than pivot are on the right side of the pivot.
2.  The left and right subarrays are also divided using the same approach. This process continues until each subarray contains a single element.
3.  At this point, elements are already sorted. Finally, elements are combined to form a sorted array.

```Python
# Quick sort in Python

# function to find the partition position
def partition(array, low, high):

  # choose the rightmost element as pivot
  pivot = array[high]

  # pointer for greater element
  i = low - 1

  # traverse through all elements
  # compare each element with pivot
  for j in range(low, high):
    if array[j] <= pivot:
      # if element smaller than pivot is found
      # swap it with the greater element pointed by i
      i = i + 1

      # swapping element at i with element at j
      (array[i], array[j]) = (array[j], array[i])

  # swap the pivot element with the greater element specified by i
  (array[i + 1], array[high]) = (array[high], array[i + 1])

  # return the position from where partition is done
  return i + 1

# function to perform quicksort
def quickSort(array, low, high):
  if low < high:

    # find pivot element such that
    # element smaller than pivot are on the left
    # element greater than pivot are on the right
    pi = partition(array, low, high)

    # recursive call on the left of pivot
    quickSort(array, low, pi - 1)

    # recursive call on the right of pivot
    quickSort(array, pi + 1, high)
```


| Property | |
| -------- |-|
|Best|$O(n \cdot log n)$|
|Worst|$O(n^2)$
|Average|$O(n \cdot log n)$
|Space Complexity|$O(log n)$|
|Stability|No|

---

# Heap Sort

![Algorithms/Attachments/Max Heap and Min Heap](max-heap-min-heap.png)

```Python
# Heap Sort in python


def heapify(arr, n, i):
  # Find largest among root and children
  largest = i
  l = 2 * i + 1
  r = 2 * i + 2

  if l < n and arr[i] < arr[l]:
	  largest = l

  if r < n and arr[largest] < arr[r]:
	  largest = r

  # If root is not largest, swap with largest and continue heapifying
  if largest != i:
	  arr[i], arr[largest] = arr[largest], arr[i]
	  heapify(arr, n, largest)


def heapSort(arr):
  n = len(arr)

  # Build max heap
  for i in range(n//2, -1, -1):
	  heapify(arr, n, i)

  for i in range(n-1, 0, -1):
	  # Swap
	  arr[i], arr[0] = arr[0], arr[i]

	  # Heapify root element
	  heapify(arr, i, 0)
```

| Property | |
| -------- |-|
|Best|$O(n \cdot log n)$|
|Worst|$O(n \cdot log n)$
|Average|$O(n \cdot log n)$
|Space Complexity|$O(1)$|
|Stability|No|
