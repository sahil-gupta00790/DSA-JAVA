# Java Queue&lt;TreeNode&gt; Guide for DSA

## Table of Contents
- [Introduction](#introduction)
- [Basic Operations](#basic-operations)
- [Implementation Details](#implementation-details)
- [Common Use Cases](#common-use-cases)
- [Common Tree Traversal Patterns](#common-tree-traversal-patterns)
- [Time Complexity](#time-complexity)
- [Common Patterns and Tricks](#common-patterns-and-tricks)
- [Common Pitfalls](#common-pitfalls)

## Introduction

A `Queue<TreeNode>` in Java is typically implemented using `LinkedList` and is commonly used for:

- Level-order traversal (Breadth-First Search)
- Processing tree nodes in FIFO (First-In-First-Out) order
- Implementing algorithms like level counting, finding tree width, and zigzag traversal

Key Features:
- FIFO ordering: elements are processed in the order they were added
- Allows `null` elements (though you typically shouldn't store null nodes)
- Not thread-safe (use `ConcurrentLinkedQueue` for thread-safety)

## Basic Operations

```java
// Creating a Queue of TreeNodes
Queue<TreeNode> q = new LinkedList<>();
Queue<TreeNode> q = new ArrayDeque<>();  // Alternative implementation

// Adding elements
q.offer(node);        // Add a node to the queue (returns false if it fails)
q.add(node);          // Similar to offer but throws exception if it fails

// Viewing/Removing elements
q.peek();             // View the head node without removing (returns null if empty)
q.element();          // Same as peek() but throws exception if empty
q.poll();             // Remove and return the head node (returns null if empty)
q.remove();           // Same as poll() but throws exception if empty

// Additional Methods
q.size();             // Get current size of the queue
q.isEmpty();          // Check if queue is empty
q.clear();            // Remove all nodes from queue
q.contains(node);     // Check if a specific node is in the queue
q.remove(node);       // Remove a specific node if present
q.toArray();          // Convert queue contents to array
```

## Implementation Details

### Common Implementations

```java
// Using LinkedList (most common)
Queue<TreeNode> q = new LinkedList<>();
// Good for most tree traversal operations
// Allows null elements (though you typically shouldn't store nulls)

// Using ArrayDeque (slightly more efficient)
Queue<TreeNode> q = new ArrayDeque<>();
// Better performance but doesn't accept null elements
// Generally preferred if you're certain not to have null nodes
```

### With Level Information

```java
// Tracking node's level
Queue<TreeNode> nodeQueue = new LinkedList<>();
Queue<Integer> levelQueue = new LinkedList<>();  // Parallel queue for levels

nodeQueue.offer(root);
levelQueue.offer(0);  // Root is at level 0

while (!nodeQueue.isEmpty()) {
    TreeNode node = nodeQueue.poll();
    int level = levelQueue.poll();
    
    // Process the node with its level information
    
    if (node.left != null) {
        nodeQueue.offer(node.left);
        levelQueue.offer(level + 1);
    }
    if (node.right != null) {
        nodeQueue.offer(node.right);
        levelQueue.offer(level + 1);
    }
}
```

### Using Custom TreeNode Objects

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    
    TreeNode() {}
    
    TreeNode(int val) {
        this.val = val;
    }
    
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

Queue<TreeNode> q = new LinkedList<>();
q.offer(new TreeNode(1));
```

## Common Use Cases

### 1. BFS (Breadth-First Search) in Trees

```java
public void bfs(TreeNode root) {
    if (root == null) return;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        TreeNode node = queue.poll();
        // process node here
        System.out.println(node.val);

        if (node.left != null) queue.offer(node.left);
        if (node.right != null) queue.offer(node.right);
    }
}
```

### 2. Finding Shortest Path in Binary Trees

```java
public int minDepth(TreeNode root) {
    if (root == null) return 0;
    
    Queue<TreeNode> q = new LinkedList<>();
    Queue<Integer> depths = new LinkedList<>();
    
    q.offer(root);
    depths.offer(1);
    
    while (!q.isEmpty()) {
        TreeNode node = q.poll();
        int depth = depths.poll();
        
        if (node.left == null && node.right == null) {
            return depth;  // Found first leaf node
        }
        
        if (node.left != null) {
            q.offer(node.left);
            depths.offer(depth + 1);
        }
        
        if (node.right != null) {
            q.offer(node.right);
            depths.offer(depth + 1);
        }
    }
    
    return 0;
}
```

### 3. Task Scheduling with Tree Dependencies

```java
public List<Integer> taskScheduling(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;
    
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    
    while (!q.isEmpty()) {
        TreeNode task = q.poll();
        result.add(task.val);  // Execute this task
        
        // Add dependent tasks to queue
        if (task.left != null) q.offer(task.left);
        if (task.right != null) q.offer(task.right);
    }
    
    return result;
}
```

## Common Tree Traversal Patterns

### Level-Order Traversal

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    
    while (!q.isEmpty()) {
        int levelSize = q.size();
        List<Integer> currentLevel = new ArrayList<>();
        
        for (int i = 0; i < levelSize; i++) {
            TreeNode node = q.poll();
            currentLevel.add(node.val);
            
            if (node.left != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        
        result.add(currentLevel);
    }
    
    return result;
}
```

### Right-Side View of Tree

```java
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;
    
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    
    while (!q.isEmpty()) {
        int levelSize = q.size();
        
        for (int i = 0; i < levelSize; i++) {
            TreeNode node = q.poll();
            
            // The last node in each level is visible from right side
            if (i == levelSize - 1) {
                result.add(node.val);
            }
            
            if (node.left != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
    }
    
    return result;
}
```

## Time Complexity

| Operation | Time Complexity |
|-----------|----------------|
| offer()   | O(1)           |
| add()     | O(1)           |
| poll()    | O(1)           |
| remove()  | O(1)           |
| peek()    | O(1)           |
| element() | O(1)           |
| size()    | O(1)           |
| isEmpty() | O(1)           |
| clear()   | O(n)           |
| contains()| O(n)           |

> Note: All operations are amortized O(1) due to LinkedList's internal structure.

## Common Patterns and Tricks

### 1. Zigzag Level Order Traversal

```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    boolean leftToRight = true;
    
    while (!q.isEmpty()) {
        int levelSize = q.size();
        List<Integer> currentLevel = new ArrayList<>();
        
        for (int i = 0; i < levelSize; i++) {
            TreeNode node = q.poll();
            
            if (leftToRight) {
                currentLevel.add(node.val);
            } else {
                currentLevel.add(0, node.val);  // Insert at beginning
            }
            
            if (node.left != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        
        result.add(currentLevel);
        leftToRight = !leftToRight;  // Toggle direction
    }
    
    return result;
}
```

### 2. Finding Maximum Width of Binary Tree

```java
public int widthOfBinaryTree(TreeNode root) {
    if (root == null) return 0;
    
    Queue<TreeNode> nodeQueue = new LinkedList<>();
    Queue<Integer> indexQueue = new LinkedList<>();  // Track positions
    
    nodeQueue.offer(root);
    indexQueue.offer(0);  // Root has position 0
    int maxWidth = 0;
    
    while (!nodeQueue.isEmpty()) {
        int size = nodeQueue.size();
        int leftIndex = 0, rightIndex = 0;
        
        for (int i = 0; i < size; i++) {
            TreeNode node = nodeQueue.poll();
            int index = indexQueue.poll();
            
            if (i == 0) leftIndex = index;
            if (i == size - 1) rightIndex = index;
            
            // For left child: 2*i
            // For right child: 2*i + 1
            if (node.left != null) {
                nodeQueue.offer(node.left);
                indexQueue.offer(2 * index);
            }
            
            if (node.right != null) {
                nodeQueue.offer(node.right);
                indexQueue.offer(2 * index + 1);
            }
        }
        
        maxWidth = Math.max(maxWidth, rightIndex - leftIndex + 1);
    }
    
    return maxWidth;
}
```

### 3. Rotating Elements (Queue Simulation)

```java
public TreeNode rotateTree(TreeNode root, int k) {
    if (root == null) return null;
    
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    
    // First collect all nodes in level order
    while (!q.isEmpty()) {
        TreeNode node = q.poll();
        if (node.left != null) q.offer(node.left);
        if (node.right != null) q.offer(node.right);
    }
    
    // Then rotate the queue k times
    Queue<TreeNode> rotated = new LinkedList<>();
    int size = q.size();
    
    for (int i = 0; i < size; i++) {
        if (i < k % size) {
            rotated.offer(q.poll());
        } else {
            q.offer(q.poll());
        }
    }
    
    // Rebuild the tree (simplified example)
    return buildTree(rotated);
}

private TreeNode buildTree(Queue<TreeNode> nodes) {
    // Implementation to rebuild tree from queue of nodes
    // This would depend on specific requirements
    return null;
}
```

## Common Pitfalls

1. **Forgetting null checks**: Always check if a node is null before adding it to the queue
   ```java
   // Do this
   if (node.left != null) q.offer(node.left);
   
   // Not this
   q.offer(node.left);  // Could add null nodes
   ```

2. **Using `remove()` or `element()` on an empty queue**: These throw exceptions if the queue is empty
   ```java
   Queue<TreeNode> q = new LinkedList<>();
   q.remove();   // Throws NoSuchElementException
   q.element();  // Throws NoSuchElementException
   
   // Use poll() and peek() instead, which return null
   ```

3. **Missing the level structure**: When doing level order traversal, process each level separately
   ```java
   // Use this pattern to separate levels
   int levelSize = q.size();
   for (int i = 0; i < levelSize; i++) {
       // Process current level
   }
   ```

4. **Modifying Queue During Iteration**: This can cause ConcurrentModificationException
   ```java
   // Don't do this
   for (TreeNode node : q) {
       if (node.val == 5) q.remove(node);  // ConcurrentModificationException risk
   }
   ```

5. **Confusing offer vs add**
   ```java
   q.add(node);    // Throws exception if fails
   q.offer(node);  // Returns false if fails
   ```

6. **Using ArrayDeque with null nodes**: ArrayDeque doesn't allow null elements
   ```java
   Queue<TreeNode> q = new ArrayDeque<>();
   q.offer(null);  // Throws NullPointerException
   ```

7. **Mixing Stack vs Queue Logic**: Queue is FIFO, don't expect LIFO behavior
   ```java
   // Don't expect this to get the most recently added element
   TreeNode latest = q.poll();  // This gets the OLDEST element, not newest
   ```  