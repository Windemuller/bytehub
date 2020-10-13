# Algorithms

## Searching

### Linear Search
+ works on unordered arrays.
+ $O(n)$

```java
    public static int linear(int[] array, int x) {
        for (int i = 0; i < array.length; i++) {
            if (array[i] == x) {
                return i;
            }
        }
        return -1;
    }
```

### Binary Search
+ works only on ordered arrays.
+ $O(\log_2 n)$


#### Iterative
```java
    public static int binarySearchIterative(int[] array, int x) {
        int upperLimit = array.length -1;
        int lowerLimit = 0;
        int mid;

        while (upperLimit >= lowerLimit) {
            mid = (upperLimit + lowerLimit) / 2;
            if (array[mid] == x) {
                return mid;
            }

            if (array[mid] > x) {
                upperLimit = mid - 1;
            } else {
                lowerLimit = mid + 1;
            }
        }
        return -1;
    }
```

#### Recursive
```java
    public static int binarySearchRecursive(int[] array, int lowerLimit, int upperLimit, int x) {
        if (upperLimit >= lowerLimit) {
            int mid = (upperLimit + lowerLimit) / 2;

            if (array[mid] == x) {
                return mid;
            }

            if (array[mid] > x) {
                return binarySearchRecursive(array, lowerLimit, mid - 1, x);
            }

            return binarySearchRecursive(array, mid + 1, upperLimit, x);
        }
        return -1;
    }

    public static int binarySearch(int[] array, int element) {
        return binarySearchRecursive(array, 0, array.length - 1, element);
    }
```

## Sorting

### Selection Sort
*The selection sort algorithm sorts an array by repeatedly finding the minimum element from an unsorted part of an array and placing it at the start of the unsorted part.*
+ Time Complexity: $O(n^2)$ because there is a nested loop.

```java
    public static void selectionSort(int[] array) {
        for (int i = 0; i < array.length ; i++) {
            int minIndex = i;
            // find smallest element in array.
            for (int j = i + 1; j < array.length; j++) {
                if (array[j] < array[minIndex]) {
                    minIndex = j;
                }
            }
            // swap i with the found element.
            int temp = array[i];
            array[i] = array[minIndex];
            array[minIndex] = i;
        }
    }
```
### Insertion Sort

+ Time complexity $O(n^2)$

```java
    public static void insertionSort(int[] array) {
        for (int i = 1; i < array.length; i++) {
            int key = array[i];
            int j = i - 1;

            while (j >= 0 && array[j] > key) {
                array[j + 1] = array[j];
                j--;
            }
            array[j + 1] = key;
        }
    }
```
### Bubble Sort
+ Time complexity $O(n^2)$

```java
    public static void bubbleSort(int[] array) {
        for (int i = 0; i < array.length; i++) {
            for (int j = i + 1; j < array.length; j++) {
                if (array[i] > array[j]) {
                    int temp = array[i];
                    array[i] = array[j];
                    array[j] = temp;
                }
            }
        }
    }
```

### Quick Sort
+ worst case $O(n^2)$
+ average case $O(n\log_2 n)$

the time complexity of quick sort depends on the chosen pivot.
the first element of the array can be chosen or the highest element in the array.
But the best approach is to choose a random pivot.

```java
    public static void quickSort(int[] array) {
        quickSortRecursive(array, 0, array.length-1);
    }

    public static void quickSortRecursive(int[] array, int low, int high) {
        if (low < high + 1) {
            int partition = partition(array, low, high);
            quickSortRecursive(array, low, partition - 1);
            quickSortRecursive(array, partition + 1, high);
        }
    }

    public static int partition(int[] arr, int low, int high) {
        int pivot = getPivotIndex(low, high);
        int partitionIndex = 0;

        swap(arr, pivot, high);

        for (int i = 0; i < high; i++) {
            // we put the pivot arr[high]
            if (arr[i] <= arr[high]) {
                swap(arr, i, partitionIndex);
                partitionIndex++;
            }
        }
        swap(arr, partitionIndex, high);

        return partitionIndex;
    }

    private static int getPivotIndex(int low, int up)
    {
        Random rand = new Random();
        return rand.nextInt((up - low) + 1) + low;
    }

    public static void swap(int[] arr, int a, int b) {
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }
```

### Merge Sort
+ $O(n\log n)$

### Radix Sort

### Shell Sort

Sources:
+ [alemoraru's algorithms pages](https://alemoraru.github.io/algorithms)
