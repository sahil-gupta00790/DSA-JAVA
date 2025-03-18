# Java TreeMap Cheat Sheet

## Table of Contents
- [Creating a TreeMap](#1-creating-a-treemap)
- [Adding & Updating Elements](#2-adding--updating-elements)
- [Retrieving Elements](#3-retrieving-elements)
- [Removing Elements](#4-removing-elements)
- [Checking Existence](#5-checking-existence)
- [Navigational Methods](#6-navigational-methods)
- [Iterating Over TreeMap](#7-iterating-over-treemap)
- [Bulk Operations](#8-bulk-operations)
- [Functional Operations](#9-functional-operations)
- [Performance Considerations](#10-performance-considerations)

---

## **1. Creating a TreeMap**
```java
// Default TreeMap (Sorted by natural order of keys)
TreeMap<Integer, String> map = new TreeMap<>();

// TreeMap with custom Comparator
TreeMap<Integer, String> map2 = new TreeMap<>(Comparator.reverseOrder());
```

---

## **2. Adding & Updating Elements**
```java
map.put(10, "A"); // Adds key-value pair
map.putIfAbsent(20, "B"); // Adds only if key is absent
map.replace(10, "C"); // Replaces value if key exists
```

---

## **3. Retrieving Elements**
```java
System.out.println(map.get(10)); // "A"
System.out.println(map.getOrDefault(15, "Not Found")); // "Not Found"
```

---

## **4. Removing Elements**
```java
map.remove(10); // Removes key 10
map.remove(20, "B"); // Removes entry only if key-value matches
```

---

## **5. Checking Existence**
```java
map.containsKey(10); // true if key exists
map.containsValue("A"); // true if value exists
```

---

## **6. Navigational Methods**
```java
map.firstKey(); // Smallest key
map.lastKey(); // Largest key
map.floorKey(15); // Greatest key <= 15
map.ceilingKey(15); // Smallest key >= 15
map.lowerKey(15); // Greatest key < 15
map.higherKey(15); // Smallest key > 15
```
```java
map.firstEntry(); // Smallest key-value pair
map.lastEntry(); // Largest key-value pair
map.floorEntry(15); // Greatest key-value pair <= 15
map.ceilingEntry(15); // Smallest key-value pair >= 15
map.lowerEntry(15); // Greatest key-value pair < 15
map.higherEntry(15); // Smallest key-value pair > 15
```

---

## **7. Iterating Over TreeMap**
```java
// Iterate over keys
for (Integer key : map.keySet()) {
    System.out.println("Key: " + key);
}

// Iterate over values
for (String value : map.values()) {
    System.out.println("Value: " + value);
}

// Iterate over key-value pairs
for (Map.Entry<Integer, String> entry : map.entrySet()) {
    System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
}
```

---

## **8. Bulk Operations**
```java
map.putAll(map2); // Adds all entries from another map
map.clear(); // Removes all elements
map.isEmpty(); // true if empty
```

---

## **9. Functional Operations**
```java
// Modify existing values
map.compute(10, (k, v) -> v + " updated");

// Update only if key exists
map.computeIfPresent(20, (k, v) -> v + " modified");

// Add only if key is absent
map.computeIfAbsent(30, k -> "New Value");
```

---

## **10. Performance Considerations**
- **Operations like `put()`, `get()`, `remove()`, and `containsKey()` run in O(log n) time complexity** due to the underlying Red-Black Tree structure.
- **Navigational methods (`higherKey()`, `lowerKey()`, etc.) also run in O(log n) time complexity.**
- **TreeMap maintains keys in sorted order**, unlike `HashMap` which has O(1) average lookup time but no ordering.

---

## **🚀 Summary Table**

| **Category**         | **Methods** |
|----------------------|------------|
| **Adding Elements**  | `put()`, `putIfAbsent()`, `replace()` |
| **Retrieving Elements** | `get()`, `getOrDefault()` |
| **Removing Elements** | `remove()` (key-only & key-value) |
| **Checking Existence** | `containsKey()`, `containsValue()` |
| **Navigational Methods** | `firstKey()`, `lastKey()`, `floorKey()`, `ceilingKey()` |
| **Iterating** | `keySet()`, `values()`, `entrySet()` |
| **Bulk Operations** | `putAll()`, `clear()`, `isEmpty()` |
| **Functional Operations** | `compute()`, `computeIfPresent()`, `computeIfAbsent()` |

---

## **🚀 Additional Tips**
- `TreeMap` **does not allow null keys**, but allows multiple null values.
- If you need **descending order**, use `map.descendingMap()`.
- Consider `LinkedHashMap` if you need **insertion order preservation** and `HashMap` for **O(1) average lookup time**.

---

## **Example Usage of `ceilingEntry()` for Leetcode 436 (Find Right Interval)**
```java
TreeMap<Integer, Integer> map = new TreeMap<>();
map.put(1, 0); // start: 1, index: 0
map.put(2, 1); // start: 2, index: 1
map.put(3, 2); // start: 3, index: 2

int end = 2;
Map.Entry<Integer, Integer> entry = map.ceilingEntry(end);
System.out.println(entry.getValue()); // Output: 1 (since start=2 is the smallest >= 2)
```

---

## **Thread Safety**
```java
// Synchronize a TreeMap
SortedMap<Integer, String> syncMap = Collections.synchronizedSortedMap(new TreeMap<>());
```

---

Would you like any additional explanations or examples? 🚀

