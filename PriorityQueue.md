# Java Priority Queue Guide for DSA

## Table of Contents
- [Introduction](#introduction)
- [Basic Operations](#basic-operations)
- [Implementation Details](#implementation-details)
- [Common Use Cases](#common-use-cases)
- [Custom Comparators](#custom-comparators)
- [Time Complexity](#time-complexity)
- [Common Patterns and Tricks](#common-patterns-and-tricks)
- [Common Pitfalls](#common-pitfalls)

## Introduction

A PriorityQueue in Java is a special type of queue where:
- Elements are processed according to their priority
- By default, the priority is natural ordering (min heap)
- It's implemented as a binary heap
- It's not thread-safe (use PriorityBlockingQueue for thread-safety)

## Basic Operations

```java
// Creation
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
PriorityQueue<Integer> withSize = new PriorityQueue<>(initialCapacity);

// Basic Operations
pq.offer(element);     // Add element (same as add())
pq.poll();            // Remove and return head element
pq.peek();            // View head element without removing
pq.size();            // Get current size
pq.isEmpty();         // Check if empty
pq.clear();           // Remove all elements

// Converting to array
Object[] arr = pq.toArray();
```

## Implementation Details

### Creating Different Types of Heaps

```java
// Min Heap (default)
PriorityQueue<Integer> minHeap = new PriorityQueue<>();

// Max Heap
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

// Custom Heap
PriorityQueue<Integer> customHeap = new PriorityQueue<>((a, b) -> a - b);
```

### With Custom Objects

```java
class Point {
    int x, y;
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

// Using Comparator
PriorityQueue<Point> pq = new PriorityQueue<>((p1, p2) -> {
    if (p1.x != p2.x) return p1.x - p2.x;
    return p1.y - p2.y;
});

// Using a separate Comparator class
class PointComparator implements Comparator<Point> {
    public int compare(Point p1, Point p2) {
        if (p1.x != p2.x) return p1.x - p2.x;
        return p1.y - p2.y;
    }
}
PriorityQueue<Point> pq = new PriorityQueue<>(new PointComparator());
```

## Common Use Cases

### 1. K-th Largest/Smallest Element

```java
// Kth largest using min heap
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>();
    for (int num : nums) {
        pq.offer(num);
        if (pq.size() > k) {
            pq.poll();
        }
    }
    return pq.peek();
}

// Kth smallest using max heap
public int findKthSmallest(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
    for (int num : nums) {
        pq.offer(num);
        if (pq.size() > k) {
            pq.poll();
        }
    }
    return pq.peek();
}
```

### 2. Merge K Sorted Lists

```java
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);
    
    // Add first node from each list
    for (ListNode list : lists) {
        if (list != null) {
            pq.offer(list);
        }
    }
    
    ListNode dummy = new ListNode(0);
    ListNode tail = dummy;
    
    while (!pq.isEmpty()) {
        ListNode node = pq.poll();
        tail.next = node;
        tail = tail.next;
        
        if (node.next != null) {
            pq.offer(node.next);
        }
    }
    
    return dummy.next;
}
```

## Custom Comparators

### For Primitive Types

```java
// Reverse order
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);

// Custom comparison
PriorityQueue<Integer> customHeap = new PriorityQueue<>((a, b) -> {
    int modA = a % 2;
    int modB = b % 2;
    if (modA != modB) return modA - modB;
    return a - b;
});
```

### For Objects

```java
class Item {
    String name;
    int price;
    
    Item(String name, int price) {
        this.name = name;
        this.price = price;
    }
}

// Multiple criteria sorting
PriorityQueue<Item> pq = new PriorityQueue<>((a, b) -> {
    if (a.price != b.price) {
        return b.price - a.price;  // Sort by price desc
    }
    return a.name.compareTo(b.name);  // Then by name asc
});
```

## Time Complexity

| Operation | Time Complexity |
|-----------|----------------|
| offer()   | O(log n)      |
| poll()    | O(log n)      |
| peek()    | O(1)          |
| size()    | O(1)          |
| isEmpty() | O(1)          |
| clear()   | O(n)          |

## Common Patterns and Tricks

### 1. Sliding Window Maximum

```java
public int[] maxSlidingWindow(int[] nums, int k) {
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> b[0] - a[0]);
    int[] result = new int[nums.length - k + 1];
    
    // Add first k elements
    for (int i = 0; i < k; i++) {
        pq.offer(new int[]{nums[i], i});
    }
    
    result[0] = pq.peek()[0];
    
    // Process rest of the array
    for (int i = k; i < nums.length; i++) {
        while (!pq.isEmpty() && pq.peek()[1] <= i - k) {
            pq.poll();
        }
        pq.offer(new int[]{nums[i], i});
        result[i - k + 1] = pq.peek()[0];
    }
    
    return result;
}
```

### 2. Maintaining K Elements

```java
// Keep only k largest elements
public void maintainKLargest(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>();  // min heap
    for (int num : nums) {
        pq.offer(num);
        if (pq.size() > k) {
            pq.poll();  // remove smallest
        }
    }
}
```

## Common Pitfalls

1. **Integer Overflow**: When using comparators with subtraction
```java
// Bad - can overflow
(a, b) -> a - b

// Good - handles overflow
(a, b) -> Integer.compare(a, b)
```

2. **Modifying Elements**: Don't modify elements while they're in the queue
```java
// Bad practice
for (Item item : pq) {
    item.value *= 2;  // Don't modify while in queue
}
```

3. **Null Elements**: PriorityQueue doesn't allow null elements
```java
pq.offer(null);  // Throws NullPointerException
```

4. **Iterator Order**: Iterator doesn't guarantee priority order
```java
// Don't do this expecting priority order
for (Integer num : pq) {
    // Elements won't be in priority order
}

// Do this instead
while (!pq.isEmpty()) {
    int num = pq.poll();
    // Elements will be in priority order
}
```