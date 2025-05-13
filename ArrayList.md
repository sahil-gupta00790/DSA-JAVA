# Java ArrayList Guide for DSA

## Table of Contents
- [Introduction](#introduction)
- [Basic Operations](#basic-operations)
- [Common Methods](#common-methods)
- [ArrayList vs Array](#arraylist-vs-array)
- [Time Complexity](#time-complexity)
- [Common Patterns](#common-patterns)
- [Tips and Tricks](#tips-and-tricks)
- [Common Pitfalls](#common-pitfalls)

## Introduction

ArrayList in Java is a resizable array implementation that:
- Grows and shrinks dynamically
- Implements List interface
- Maintains insertion order
- Allows duplicates
- Permits null values
- Is not synchronized (use Collections.synchronizedList() for thread-safety)

## Basic Operations

```java
// Creation
ArrayList<Integer> list = new ArrayList<>();              // Empty list
ArrayList<Integer> list = new ArrayList<>(initialCapacity); // With initial capacity
ArrayList<Integer> list = new ArrayList<>(anotherList);   // From another collection

// Adding elements
list.add(element);           // Add at end
list.add(index, element);    // Add at index
list.addAll(collection);     // Add all elements from collection
list.addAll(index, collection); // Add all elements at index

// Removing elements
list.remove(index);         // Remove by index
list.remove(Object o);      // Remove first occurrence
list.removeAll(collection); // Remove all elements in collection
list.clear();              // Remove all elements

// Accessing elements
list.get(index);           // Get element at index
list.set(index, element);  // Replace element at index


Collections.reverse(list);//just reverses the list
```

## Common Methods

### Searching and Checking

```java
// Search operations
list.contains(object);     // Check if element exists
list.indexOf(object);      // First occurrence index
list.lastIndexOf(object);  // Last occurrence index
list.isEmpty();            // Check if list is empty
list.size();              // Get number of elements

// Sublist and Range Operations
list.subList(fromIndex, toIndex);  // Get view of portion of list
```

### Conversion Operations

```java
// To Array conversions
Object[] arr = list.toArray();              // Convert to Object array
Integer[] arr = list.toArray(new Integer[0]); // Convert to Integer array

// From Array to ArrayList
String[] arr = {"a", "b", "c"};
ArrayList<String> list = new ArrayList<>(Arrays.asList(arr));

// Stream operations (Java 8+)
list.stream()
    .filter(x -> x > 0)
    .collect(Collectors.toList());
```

## ArrayList vs Array

```java
// Array (fixed size)
int[] arr = new int[5];
arr.length;  // Fixed size

// ArrayList (dynamic size)
ArrayList<Integer> list = new ArrayList<>();
list.size();  // Current size
```

### Key Differences

1. **Size**:
   - Array: Fixed size
   - ArrayList: Dynamic size

2. **Type**:
   - Array: Can hold primitives
   - ArrayList: Only objects (uses wrapper classes)

3. **Syntax**:
```java
// Array
int[] arr = new int[5];
arr[0] = 1;

// ArrayList
ArrayList<Integer> list = new ArrayList<>();
list.add(1);
```

## Time Complexity

| Operation               | Time Complexity |
|------------------------|-----------------|
| add(E element)         | O(1) amortized  |
| add(int index, E element) | O(n)        |
| get(int index)         | O(1)           |
| remove(int index)      | O(n)           |
| indexOf(Object o)      | O(n)           |
| contains(Object o)     | O(n)           |
| size()                 | O(1)           |
| clear()               | O(n)           |

## Common Patterns

### 1. List as Stack
```java
ArrayList<Integer> stack = new ArrayList<>();
stack.add(element);      // Push
stack.remove(stack.size() - 1);  // Pop
stack.get(stack.size() - 1);     // Peek
```

### 2. List Manipulation
```java
// Remove while iterating
Iterator<Integer> iter = list.iterator();
while (iter.hasNext()) {
    if (shouldRemove(iter.next())) {
        iter.remove();  // Safe removal during iteration
    }
}

// Filter elements
list.removeIf(x -> x < 0);  // Remove all negative numbers

// Sort list
Collections.sort(list);                    // Natural order
Collections.sort(list, Collections.reverseOrder()); // Reverse order
```

### 3. List as Queue
```java
ArrayList<Integer> queue = new ArrayList<>();
queue.add(element);     // Enqueue
queue.remove(0);        // Dequeue (inefficient, use LinkedList instead)
queue.get(0);          // Peek
```

## Tips and Tricks

### 1. Efficient Bulk Operations
```java
// Efficient addition of multiple elements
list.ensureCapacity(expectedSize);  // Prevent multiple resizing

// Bulk removal
list.removeAll(elementsToRemove);

// Bulk retention
list.retainAll(elementsToKeep);
```

### 2. Memory Optimization
```java
// Trim to size after bulk operations
list.trimToSize();  // Reduces internal array to current size
```

### 3. Custom Sorting
```java
// Sort by custom comparator
Collections.sort(list, (a, b) -> b - a);  // Descending order

// Sort custom objects
class Person {
    String name;
    int age;
}

Collections.sort(personList, (p1, p2) -> p1.age - p2.age);  // Sort by age
```

## Common Pitfalls

1. **Removing While Iterating**
```java
// Wrong way - ConcurrentModificationException
for (Integer num : list) {
    if (num < 0) list.remove(num);
}

// Correct ways
// Using Iterator
Iterator<Integer> iter = list.iterator();
while (iter.hasNext()) {
    if (iter.next() < 0) iter.remove();
}

// Using removeIf (Java 8+)
list.removeIf(num -> num < 0);

// Using backward iteration
for (int i = list.size() - 1; i >= 0; i--) {
    if (list.get(i) < 0) list.remove(i);
}
```

2. **Boxing/Unboxing Overhead**
```java
// Inefficient - involves boxing/unboxing
ArrayList<Integer> list = new ArrayList<>();
for (int i = 0; i < 1000000; i++) {
    list.add(i);
}

// More efficient for primitive operations
int[] array = new int[1000000];
for (int i = 0; i < 1000000; i++) {
    array[i] = i;
}
```

3. **Initial Capacity**
```java
// Inefficient if size known
ArrayList<Integer> list = new ArrayList<>();  // Default capacity: 10

// More efficient with known size
ArrayList<Integer> list = new ArrayList<>(10000);  // Preallocate capacity
```

4. **Equals and HashCode**
```java
// Remember to override equals and hashCode when using custom objects
class CustomObject {
    @Override
    public boolean equals(Object o) {
        // Implementation
    }
    
    @Override
    public int hashCode() {
        // Implementation
    }
}
```