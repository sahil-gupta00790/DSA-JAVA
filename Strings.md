# Java String Functions for DSA - Complete Reference Guide

## Table of Contents
- [1. Basic String Operations](#1-basic-string-operations)
- [2. String Comparison](#2-string-comparison)
- [3. String Modification](#3-string-modification)
- [4. StringBuilder Operations](#4-stringbuilder-operations)
- [5. String Splitting](#5-string-splitting)
- [6. Character Operations](#6-character-operations)
- [7. String-Number Conversion](#7-string-number-conversion)
- [8. String Content Checking](#8-string-content-checking)
- [9. Common DSA Patterns](#9-common-dsa-patterns)
- [10. Common String Problems](#10-common-string-problems)
- [11. Best Practices](#11-best-practices)
- [12. Performance Tips](#12-performance-tips)

## 1. Basic String Operations

### Length and Character Access
```java
String str = "Hello World";

// Length
int length = str.length();  // 11

// Character at index
char ch = str.charAt(0);    // 'H'
```

### Substring Operations
```java
String str = "Hello World";

// Substring with end index (exclusive)
String sub1 = str.substring(0, 5);     // "Hello"

// Substring from start index to end
String sub2 = str.substring(6);        // "World"
```

### Finding Indices
```java
String str = "Hello World";

// First occurrence of character
int index1 = str.indexOf('o');         // 4

// Last occurrence of character
int index2 = str.lastIndexOf('o');     // 7

// Index of substring
int index3 = str.indexOf("World");     // 6

// When character/substring not found
int index4 = str.indexOf('z');         // -1
```

## 2. String Comparison

### Basic Comparison
```java
String s1 = "hello";
String s2 = "HELLO";

// Case-sensitive equality
boolean equals1 = s1.equals(s2);           // false

// Case-insensitive equality
boolean equals2 = s1.equalsIgnoreCase(s2); // true
```

### Lexicographical Comparison
```java
String s1 = "hello";
String s2 = "HELLO";

// Case-sensitive comparison
int comp1 = s1.compareTo(s2);          // positive (because 'h' > 'H')

// Case-insensitive comparison
int comp2 = s1.compareToIgnoreCase(s2); // 0 (equal when ignoring case)
```

## 3. String Modification

### Whitespace Handling
```java
String str = "  Hello World  ";

// Remove leading and trailing whitespace
String trimmed = str.trim();  // "Hello World"
```

### Case Conversion
```java
String str = "Hello World";

// Convert to uppercase
String upper = str.toUpperCase();  // "HELLO WORLD"

// Convert to lowercase
String lower = str.toLowerCase();  // "hello world"
```

### Character/String Replacement
```java
String str = "Hello World";

// Replace single character
String replaced = str.replace('l', 'x');     // "Hexxo Worxd"

// Replace all occurrences of substring
String replacedAll = str.replaceAll("l", "x"); // "Hexxo Worxd"
```

## 4. StringBuilder Operations

### Basic StringBuilder Usage
```java
// Create and append
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World");
String result = sb.toString();  // "Hello World"

// Insert at specific position
sb.insert(5, "!");  // "Hello! World"

// Delete characters
sb.delete(5, 7);    // "HelloWorld"

// Reverse string
sb.reverse();       // "dlroWolleH"
```

### String Joining
```java
// Join strings with delimiter
String joined = String.join("-", "Hello", "World");  // "Hello-World"
```

## 5. String Splitting

### Split Operations
```java
String str = "Hello,World,Java";

// Split into array
String[] parts = str.split(",");  // ["Hello", "World", "Java"]

// Split with limit
String[] limited = str.split(",", 2);  // ["Hello", "World,Java"]
```

## 6. Character Operations

### Character Type Checking
```java
char c = 'A';

boolean isDigit = Character.isDigit(c);      // false
boolean isLetter = Character.isLetter(c);    // true
boolean isLetterOrDigit = Character.isLetterOrDigit(c);  // true
boolean isLowerCase = Character.isLowerCase(c);  // false
boolean isUpperCase = Character.isUpperCase(c);  // true
boolean isWhitespace = Character.isWhitespace(c);  // false
```

### Character Case Conversion
```java
char lower = Character.toLowerCase('A');  // 'a'
char upper = Character.toUpperCase('a');  // 'A'
```

## 7. String-Number Conversion

### String to Number
```java
int num1 = Integer.parseInt("123");        // 123
long num2 = Long.parseLong("123456789");   // 123456789
double num3 = Double.parseDouble("123.45"); // 123.45
```

### Number to String
```java
String str1 = String.valueOf(123);         // "123"
String str2 = Integer.toString(123);       // "123"
String str3 = Double.toString(123.45);     // "123.45"
```

## 8. String Content Checking

### Content Verification
```java
String str = "Hello World";

// Check if contains substring
boolean contains = str.contains("Hello");  // true

// Check start/end
boolean starts = str.startsWith("He");     // true
boolean ends = str.endsWith("ld");         // true

// Empty checks
boolean isEmpty = str.isEmpty();           // false
boolean isBlank = str.isBlank();          // false (true for whitespace only)
```

## 9. Common DSA Patterns

### String-Array Conversion
```java
// Convert string to char array
char[] chars = str.toCharArray();

// Build string from char array
String fromChars = new String(chars);
```

### ASCII Operations
```java
// Get ASCII value
int ascii = (int)'A';  // 65

// Convert ASCII to char
char fromAscii = (char)65;  // 'A'
```

### Quick Checks
```java
// Check if character is vowel
boolean isVowel = "aeiouAEIOU".indexOf(c) != -1;
```


## 10. Common String Problems

### Palindrome Check
```java
// Method 1: Using StringBuilder
public boolean isPalindrome(String s) {
    String cleanStr = s.toLowerCase().replaceAll("[^a-z0-9]", "");
    return cleanStr.equals(new StringBuilder(cleanStr).reverse().toString());
}

// Method 2: Two Pointers
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) return false;
        left++;
        right--;
    }
    return true;
}
```

### Anagram Check
```java
public boolean isAnagram(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    
    int[] freq = new int[26];
    for (int i = 0; i < s1.length(); i++) {
        freq[s1.charAt(i) - 'a']++;
        freq[s2.charAt(i) - 'a']--;
    }
    
    for (int f : freq) {
        if (f != 0) return false;
    }
    return true;
}
```

### Longest Common Prefix
```java
public String longestCommonPrefix(String[] strs) {
    if (strs == null || strs.length == 0) return "";
    
    String prefix = strs[0];
    for (int i = 1; i < strs.length; i++) {
        while (strs[i].indexOf(prefix) != 0) {
            prefix = prefix.substring(0, prefix.length() - 1);
            if (prefix.isEmpty()) return "";
        }
    }
    return prefix;
}
```

## 11. Best Practices

### String Pool Usage
```java
// Using String Pool
String s1 = "hello";  // Creates in string pool
String s2 = "hello";  // Reuses from pool
boolean sameRef = (s1 == s2);  // true

// Not using String Pool
String s3 = new String("hello");  // Creates new object
boolean differentRef = (s1 == s3);  // false
```

### StringBuilder vs String
```java
// Bad practice - creates many string objects
String result = "";
for (int i = 0; i < 1000; i++) {
    result += "a";
}

// Good practice - uses StringBuilder
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append("a");
}
String result = sb.toString();
```

### Pattern Compilation
```java
// For repeated use, compile pattern once
Pattern pattern = Pattern.compile("[0-9]+");
Matcher matcher = pattern.matcher(text);
while (matcher.find()) {
    // Process matches
}
```

## 12. Performance Tips

### Memory Optimization
```java
// Pre-size StringBuilder
StringBuilder sb = new StringBuilder(calculatedCapacity);

// Avoid substring() in loops
for (String s : strings) {
    // Bad: Creates many substring objects
    process(s.substring(1));
    
    // Better: Use char array or StringBuilder
    char[] chars = s.toCharArray();
    process(new String(chars, 1, chars.length - 1));
}
```

### Efficient String Comparison
```java
// More efficient for prefix check
if (str.startsWith(prefix))  // Better than substring(0, prefix.length())

// More efficient for suffix check
if (str.endsWith(suffix))    // Better than substring(str.length() - suffix.length())
```

### String Interning
```java
String s1 = new String("hello").intern();
String s2 = "hello";
boolean sameRef = (s1 == s2);  // true after interning
```

## Extended Time Complexity Reference

| Operation | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| length() | O(1) | O(1) |
| charAt() | O(1) | O(1) |
| substring() | O(n) | O(n) |
| indexOf() | O(n*m) | O(1) |
| contains() | O(n*m) | O(1) |
| replace() | O(n) | O(n) |
| split() | O(n) | O(n) |
| StringBuilder append() | O(1) amortized | O(n) |
| StringBuilder toString() | O(n) | O(n) |
| Pattern matching | O(n*m) | O(m) |

Where:
- n is the length of the string
- m is the length of the pattern/substring

## Common Gotchas

1. Modifying String in Loop
```java
// Inefficient
String s = "";
for (int i = 0; i < n; i++) {
    s += i;  // Creates new string each time
}

// Efficient
StringBuilder sb = new StringBuilder();
for (int i = 0; i < n; i++) {
    sb.append(i);
}
String s = sb.toString();
```

2. String Comparison
```java
// Wrong
if (str1 == str2)  // Compares references

// Correct
if (str1.equals(str2))  // Compares content
```

3. Null Checks
```java
// Safer
if ("constant".equals(variable))  // No NPE if variable is null

// Dangerous
if (variable.equals("constant"))  // NPE if variable is null
```

## Important Notes

1. Strings in Java are immutable - each modification creates a new string
2. Use StringBuilder for multiple string modifications
3. String indices are 0-based
4. Most string operations that don't find a match return -1
5. substring() end index is exclusive
6. indexOf() is case-sensitive
7. Regular expressions can be used with replaceAll() and split()

## Time Complexity Reference

- length(): O(1)
- charAt(): O(1)
- substring(): O(n)
- indexOf(): O(n)
- equals(): O(n)
- compareTo(): O(n)
- StringBuilder operations: O(1) amortized
- split(): O(n)
- replace(): O(n)
- toCharArray(): O(n)

Where n is the length of the string or the length of the substring being processed.