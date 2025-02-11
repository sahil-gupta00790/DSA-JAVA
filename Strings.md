# Java String Functions for DSA - Quick Reference Guide

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