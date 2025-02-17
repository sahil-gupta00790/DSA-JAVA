# Java Arrays for DSA - Complete Reference Guide

## Table of Contents
- [1. Basic Array Operations](#1-basic-array-operations)
- [2. Array Initialization](#2-array-initialization)
- [3. Array Utility Methods](#3-array-utility-methods)
- [4. Multi-dimensional Arrays](#4-multi-dimensional-arrays)
- [5. Array List Operations](#5-array-list-operations)
- [6. Common DSA Patterns](#6-common-dsa-patterns)
- [7. Array Algorithms](#7-array-algorithms)
- [8. Best Practices](#8-best-practices)
- [9. Performance Tips](#9-performance-tips)

## 1. Basic Array Operations

### Array Creation and Access
```java
// Array declaration
int[] arr = new int[5];

// Array initialization with values
int[] arr = {1, 2, 3, 4, 5};

// Accessing elements
int first = arr[0];          // First element
int last = arr[arr.length-1];// Last element

// Array length
int length = arr.length;     // Array length property
```

### Array Modification
```java
// Setting values
arr[0] = 10;                 // Set first element
arr[arr.length-1] = 20;      // Set last element

// Copying arrays
int[] copy1 = arr.clone();   // Create shallow copy
int[] copy2 = Arrays.copyOf(arr, arr.length);
int[] copy3 = Arrays.copyOfRange(arr, 1, 4); // Copy subarray
```

## 2. Array Initialization

### Different Ways to Initialize
```java
// Method 1: Declaration and initialization separately
int[] arr1 = new int[5];
arr1[0] = 1; arr1[1] = 2; // etc.

// Method 2: Inline initialization
int[] arr2 = {1, 2, 3, 4, 5};

// Method 3: Anonymous array
method(new int[]{1, 2, 3, 4, 5});

// Method 4: Using Arrays.fill()
int[] arr4 = new int[5];
Arrays.fill(arr4, 10);  // All elements become 10
```

### Type-Specific Arrays
```java
// Primitive type arrays
byte[] byteArray = new byte[5];
short[] shortArray = new short[5];
int[] intArray = new int[5];
long[] longArray = new long[5];
float[] floatArray = new float[5];
double[] doubleArray = new double[5];
boolean[] boolArray = new boolean[5];
char[] charArray = new char[5];

// Object arrays
String[] stringArray = new String[5];
Integer[] integerArray = new Integer[5];
```

## 3. Array Utility Methods

### Arrays Class Methods
```java
// Sorting
Arrays.sort(arr);                    // Sort entire array
Arrays.sort(arr, 1, 4);             // Sort subarray
Arrays.sort(arr, Collections.reverseOrder()); // Reverse sort (objects only)

// Searching
int index = Arrays.binarySearch(arr, key);    // Binary search (array must be sorted)

// Comparison
boolean equals = Arrays.equals(arr1, arr2);   // Compare arrays
boolean deepEquals = Arrays.deepEquals(arr1, arr2); // Compare nested arrays

// Fill operations
Arrays.fill(arr, value);            // Fill entire array
Arrays.fill(arr, fromIndex, toIndex, value);  // Fill subarray

// Convert to String
String str = Arrays.toString(arr);            // Convert to string
String deepStr = Arrays.deepToString(arr);    // Convert nested array to string
```

## 4. Multi-dimensional Arrays

### 2D Arrays
```java
// Declaration and initialization
int[][] matrix = new int[3][4];  // 3 rows, 4 columns

// Inline initialization
int[][] matrix = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};

// Accessing elements
int element = matrix[1][2];      // Row 1, Column 2

// Getting dimensions
int rows = matrix.length;        // Number of rows
int cols = matrix[0].length;     // Number of columns
```

### Jagged Arrays
```java
// Different length for each row
int[][] jaggedArray = new int[3][];
jaggedArray[0] = new int[4];
jaggedArray[1] = new int[2];
jaggedArray[2] = new int[5];
```

## 5. Array List Operations

### ArrayList vs Array
```java
// Converting Array to ArrayList
Integer[] arr = {1, 2, 3, 4, 5};
List<Integer> list = Arrays.asList(arr);
ArrayList<Integer> arrayList = new ArrayList<>(Arrays.asList(arr));

// Converting ArrayList to Array
Integer[] arr2 = list.toArray(new Integer[0]);
```

### ArrayList Methods
```java
ArrayList<Integer> list = new ArrayList<>();
list.add(1);                  // Add element
list.add(0, 2);              // Add at index
list.remove(0);              // Remove at index
list.set(0, 3);              // Set element
int element = list.get(0);    // Get element
int size = list.size();       // Get size
boolean exists = list.contains(3); // Check existence
```

## 6. Common DSA Patterns

### Two Pointer Technique
```java
public void twoPointers(int[] arr) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        // Process elements from both ends
        left++;
        right--;
    }
}
```

### Sliding Window
```java
public int slidingWindow(int[] arr, int k) {
    int windowSum = 0;
    // First window
    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    
    int maxSum = windowSum;
    // Slide window
    for (int i = k; i < arr.length; i++) {
        windowSum = windowSum - arr[i-k] + arr[i];
        maxSum = Math.max(maxSum, windowSum);
    }
    return maxSum;
}
```

### Prefix Sum
```java
public int[] buildPrefixSum(int[] arr) {
    int[] prefix = new int[arr.length];
    prefix[0] = arr[0];
    for (int i = 1; i < arr.length; i++) {
        prefix[i] = prefix[i-1] + arr[i];
    }
    return prefix;
}
```

## 7. Array Algorithms

### Binary Search
```java
public int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

### Quick Sort
```java
public void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

private int partition(int[] arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    
    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            swap(arr, i, j);
        }
    }
    swap(arr, i + 1, high);
    return i + 1;
}
```

### Merge Sort
```java
public void mergeSort(int[] arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

private void merge(int[] arr, int left, int mid, int right) {
    int[] temp = new int[right - left + 1];
    int i = left, j = mid + 1, k = 0;
    
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) temp[k++] = arr[i++];
        else temp[k++] = arr[j++];
    }
    
    while (i <= mid) temp[k++] = arr[i++];
    while (j <= right) temp[k++] = arr[j++];
    
    for (i = 0; i < k; i++) {
        arr[left + i] = temp[i];
    }
}
```

## 8. Best Practices

### Memory Management
```java
// Prefer ArrayList for dynamic size
ArrayList<Integer> list = new ArrayList<>();

// Pre-size ArrayList when size is known
ArrayList<Integer> list = new ArrayList<>(initialCapacity);

// Clear references when done
array = null;  // Allow garbage collection
```

### Bounds Checking
```java
// Always check array bounds
if (index >= 0 && index < array.length) {
    // Safe to access array[index]
}

// Use try-catch for potential ArrayIndexOutOfBoundsException
try {
    value = array[index];
} catch (ArrayIndexOutOfBoundsException e) {
    // Handle exception
}
```

## 9. Performance Tips

### Time Complexity Reference
| Operation | Array | ArrayList |
|-----------|--------|-----------|
| Access | O(1) | O(1) |
| Search | O(n) | O(n) |
| Insert | N/A | O(n) |
| Append | N/A | O(1) amortized |
| Delete | N/A | O(n) |

### Space Optimization
```java
// Use primitive arrays instead of object arrays when possible
int[] arr = new int[1000];         // More efficient than
Integer[] arr = new Integer[1000];  // this

// Use appropriate initial capacity
ArrayList<Integer> list = new ArrayList<>(expectedSize);
```

### Common Gotchas

1. Array Size is Fixed
```java
// Cannot resize array after creation
int[] arr = new int[5];
// Need to create new array to change size
arr = Arrays.copyOf(arr, 10);
```

2. Object Array Initialization
```java
// Objects are initialized to null
String[] arr = new String[5];
// Must initialize each element
for (int i = 0; i < arr.length; i++) {
    arr[i] = "";
}
```

3. Multi-dimensional Array Memory
```java
// Each row can be different length
int[][] arr = new int[3][];
// Must initialize each row separately
for (int i = 0; i < arr.length; i++) {
    arr[i] = new int[i + 1];  // Different lengths
}
```

## Important Notes

1. Arrays are fixed-size in Java
2. Array indices are 0-based
3. Arrays.sort() uses modified quicksort for primitives and modified mergesort for objects
4. ArrayList provides dynamic sizing but with some performance overhead
5. Binary search requires sorted array
6. System.arraycopy() is faster than manual copying
7. Arrays.asList() returns fixed-size list
8. Primitive arrays are covariant but generic arrays are not