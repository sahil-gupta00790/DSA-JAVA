# Java HashMap Cheat Sheet

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

🚀 **This cheat sheet helps you work with Java's HashMap efficiently!**

