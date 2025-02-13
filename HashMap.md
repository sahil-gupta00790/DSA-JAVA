# Java HashMap Cheat Sheet

## Table of Contents
- [Creating a HashMap](#1-creating-a-hashmap)
- [Adding & Updating Elements](#2-adding--updating-elements)
- [Retrieving Elements](#3-retrieving-elements)
- [Removing Elements](#4-removing-elements)
- [Checking Existence](#5-checking-existence)
- [Iterating Over HashMap](#6-iterating-over-hashmap)
- [Bulk Operations](#7-bulk-operations)
- [Functional Operations](#8-functional-operations)
- [Frequency Counting](#9-using-merge-for-frequency-counting)
- [Time Complexity](#10-time-complexity)
- [Common Patterns](#11-common-patterns)
- [Common Pitfalls](#12-common-pitfalls)



## **1. Creating a HashMap**
```java
// Default HashMap
HashMap<String, Integer> map = new HashMap<>();

// HashMap with Initial Capacity
HashMap<String, Integer> map2 = new HashMap<>(100);
```

---

## **2. Adding & Updating Elements**
```java
map.put("Alice", 25); // Adds a key-value pair
map.putIfAbsent("Bob", 30); // Adds only if key is absent
map.merge("Alice", 5, Integer::sum); // Adds 5 to existing value
```

---

## **3. Retrieving Elements**
```java
System.out.println(map.get("Alice")); // 25
System.out.println(map.getOrDefault("Charlie", 0)); // 0 (default if key not found)
```

---

## **4. Removing Elements**
```java
map.remove("Alice"); // Removes key Alice
map.remove("Bob", 30); // Removes Bob only if value matches
```

---

## **5. Checking Existence**
```java
map.containsKey("Alice"); // true if key exists
map.containsValue(30); // true if value exists
```

---

## **6. Iterating Over HashMap**
```java
// Iterate over keys
for (String key : map.keySet()) {
    System.out.println("Key: " + key);
}

// Iterate over values
for (Integer value : map.values()) {
    System.out.println("Value: " + value);
}

// Iterate over key-value pairs
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
}
```

---

## **7. Bulk Operations**
```java
map.putAll(map2); // Adds all entries from another map
map.clear(); // Removes all elements
map.isEmpty(); // true if empty
```

---

## **8. Functional Operations**
```java
// Modify existing values
map.compute("Alice", (k, v) -> v + 10); // Adds 10 to Alice's value

// Update only if key exists
map.computeIfPresent("Alice", (k, v) -> v + 5);

// Add only if key is absent
map.computeIfAbsent("Bob", k -> 50);
```

---

## **9. Using `merge()` for Frequency Counting**
```java
int[] nums = {1, 2, 1, 3, 2, 2};
Map<Integer, Integer> freq = new HashMap<>();

for (int num : nums) {
    freq.merge(num, 1, Integer::sum);
}

System.out.println(freq); // {1=2, 2=3, 3=1}
```

---

## **🚀 Summary Table**

| **Category**         | **Methods** |
|----------------------|------------|
| **Adding Elements**  | `put()`, `putIfAbsent()`, `merge()` |
| **Retrieving Elements** | `get()`, `getOrDefault()` |
| **Removing Elements** | `remove()` (key-only & key-value) |
| **Checking Existence** | `containsKey()`, `containsValue()` |
| **Iterating** | `keySet()`, `values()`, `entrySet()` |
| **Bulk Operations** | `putAll()`, `clear()`, `isEmpty()` |
| **Functional Operations** | `compute()`, `computeIfPresent()`, `computeIfAbsent()` |





## **10. Time Complexity**
```java
// All basic operations are O(1) average case, O(n) worst case
put()           - O(1)
get()           - O(1)
remove()        - O(1)
containsKey()   - O(1)
containsValue() - O(n)
```

## **11. Common Patterns**

### Two Sum Problem
```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] {map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[0];
}
```

### Group By Pattern
```java
// Group strings by their lengths
Map<Integer, List<String>> lengthMap = new HashMap<>();
for (String str : strings) {
    lengthMap.computeIfAbsent(str.length(), k -> new ArrayList<>()).add(str);
}
```

### Counter Pattern with getOrDefault
```java
Map<String, Integer> counter = new HashMap<>();
for (String word : words) {
    counter.put(word, counter.getOrDefault(word, 0) + 1);
}
```

## **12. Common Pitfalls**

### Mutating While Iterating
```java
// Wrong way - ConcurrentModificationException
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    if (entry.getValue() < 0) {
        map.remove(entry.getKey());  // Don't do this!
    }
}

// Correct way
map.entrySet().removeIf(entry -> entry.getValue() < 0);
```

### Custom Objects as Keys
```java
class Person {
    String name;
    int age;
    
    // Must override these for proper HashMap functionality
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person person = (Person) o;
        return age == person.age && Objects.equals(name, person.name);
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}
```

## **13. Thread Safety**
```java
// Create thread-safe map
Map<String, Integer> synchronizedMap = Collections.synchronizedMap(new HashMap<>());

// Or use ConcurrentHashMap
ConcurrentHashMap<String, Integer> concurrentMap = new ConcurrentHashMap<>();
```

## **14. Memory Management**
```java
// Initialize with expected size to avoid resizing
int expectedSize = 100;
Map<String, Integer> map = new HashMap<>(expectedSize / 0.75f + 1);

// Clear references when no longer needed
map.clear();
map = null;  // Allow for garbage collection
```

## **🚀 Additional Tips**

- Default initial capacity is 16 with a load factor of 0.75
- Capacity is always a power of 2
- Null keys and values are allowed (unlike Hashtable)
- Not thread-safe by default
- Iteration order is not guaranteed

## **Performance Considerations**
- Choose initial capacity wisely to avoid resizing
- Use appropriate load factor (default 0.75 is usually good)
- Consider EnumMap for enum keys
- Use IdentityHashMap when reference equality is needed