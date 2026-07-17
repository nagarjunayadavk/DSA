
Here is the comprehensive breakdown of all the primary data structures within the `java.util` package that you will use for DSA, organized into a clear, comparative table along with their basic usage methods.

---

## The Ultimate Java Collections Cheat Sheet for DSA

Every class listed below belongs to the `java.util` package (e.g., `import java.util.HashMap;`).

| Data Structure / Concept | Java Interface | Java Implementation Class | Time Complexity (Average) | Best Used For |
| --- | --- | --- | --- | --- |
| **Dynamic Array** | `List<E>` | `ArrayList<E>` | Access: $O(1)$ <br> <br> Insert/Delete: $O(n)$ | Random access, simple lists, grids, and graphs (adjacency lists). |
| **Doubly Linked List** | `List<E>` / `Deque<E>` | `LinkedList<E>` | Access: $O(n)$ <br> <br> Insert/Delete at ends: $O(1)$ | Implementing queues/stacks or when frequent middle deletions are needed via iterators. |
| **Unordered Map** | `Map<K, V>` | `HashMap<K, V>` | Get/Put: $O(1)$ | Frequency counting, two-pointer complements, caching, memoization. |
| **Insertion-Ordered Map** | `Map<K, V>` | `LinkedHashMap<K, V>` | Get/Put: $O(1)$ | LRU Cache implementations, maintaining history order. |
| **Sorted Map** | `NavigableMap<K,V>` | `TreeMap<K, V>` | Get/Put: $O(\log n)$ | Range queries, keeping keys sorted automatically (Red-Black Tree). |
| **Unordered Set** | `Set<E>` | `HashSet<E>` | Add/Contains: $O(1)$ | Tracking unique visited nodes (BFS/DFS), removing duplicates. |
| **Insertion-Ordered Set** | `Set<E>` | `LinkedHashSet<E>` | Add/Contains: $O(1)$ | Unique collections where the exact insertion order matters. |
| **Sorted Set** | `NavigableSet<E>` | `TreeSet<E>` | Add/Contains: $O(\log n)$ | Finding closest elements via `ceiling()` and `floor()`. |
| **Queue / Stack / Deque** | `Deque<E>` | `ArrayDeque<E>` | Insert/Delete at ends: $O(1)$ | **Standard Choice** for BFS (Queue) and DFS/Backtracking (Stack). Faster than `Stack` or `LinkedList`. |
| **Min/Max Heap** | `Queue<E>` | `PriorityQueue<E>` | Peek: $O(1)$ <br> <br> Offer/Poll: $O(\log n)$ | Dijkstra's algorithm, K-way merging, Top-K frequent elements. |

---

## Basic Usage & Code Reference

Here is how you initialize and perform the core operations for each of these structures:

### 1. Lists

```java
List<Integer> list = new ArrayList<>();
list.add(5);                // Add element to end
list.add(0, 2);             // Insert 2 at index 0 -> [2, 5]
int val = list.get(1);      // Get element at index 1 (5)
list.set(1, 10);            // Update index 1 to 10 -> [2, 10]
list.remove(list.size() - 1); // Remove last element

```

### 2. Maps (`HashMap`, `LinkedHashMap`, `TreeMap`)

```java
Map<String, Integer> map = new HashMap<>(); // Swap with TreeMap / LinkedHashMap as needed
map.put("Apple", 10);
map.put("Banana", 20);

int count = map.getOrDefault("Orange", 0); // Safe way to get value (returns 0 if key missing)
boolean hasKey = map.containsKey("Apple"); // Check if key exists (true)

// Iterating over a Map
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}

```

### 3. Sets (`HashSet`, `LinkedHashSet`, `TreeSet`)

```java
Set<Integer> set = new HashSet<>(); // Swap with TreeSet / LinkedHashSet as needed
set.add(10);
set.add(10); // Duplicate ignored, returns false

if (set.contains(10)) {
    set.remove(10); // Removes 10 from the set
}

// Special TreeSet methods:
TreeSet<Integer> treeSet = new TreeSet<>();
treeSet.add(5); treeSet.add(10); treeSet.add(15);
int lower = treeSet.floor(9);   // Returns 5 (greatest element <= 9)
int higher = treeSet.ceiling(9); // Returns 10 (smallest element >= 9)

```

### 4. Queues & Deques (`ArrayDeque`)

```java
// FIFO Queue Behavior (for BFS)
Queue<Integer> queue = new ArrayDeque<>();
queue.offer(1);      // Enqueue
int front = queue.peek(); // Look at front
int removed = queue.poll(); // Dequeue

// LIFO Stack Behavior (for DFS/Backtracking)
Deque<Integer> stack = new ArrayDeque<>();
stack.push(5);       // Push to top
int top = stack.peek();   // Look at top
int popped = stack.pop();  // Pop from top

```

### 5. PriorityQueue (Heaps)

```java
// Min-Heap (default)
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
minHeap.offer(10);
minHeap.offer(5);
int smallest = minHeap.poll(); // Returns 5

// Max-Heap (Custom Comparator)
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
maxHeap.offer(10);
maxHeap.offer(5);
int largest = maxHeap.poll(); // Returns 10

```

## Contains Duplicate:

| Collection      | Can check duplicates? | Good choice?                                          |
| --------------- | --------------------- | ----------------------------------------------------- |
| `HashSet`       | ✅ Yes (`contains()`)  | ⭐ Best                                                |
| `LinkedHashSet` | ✅ Yes                 | Good, but preserves insertion order (not needed here) |
| `TreeSet`       | ✅ Yes                 | Works, but slower because it keeps elements sorted    |
| `ArrayList`     | ✅ Yes (`contains()`)  | Not recommended; checking `contains()` is `O(n)`      |
| `HashMap`       | ✅ Yes (using keys)    | Good, but a `HashSet` is simpler                      |
| `LinkedHashMap` | ✅ Yes                 | Works, but unnecessary                                |
| `TreeMap`       | ✅ Yes                 | Works, but slower                                     |

### HashSet
```
HashSet<Integer> set = new HashSet<>();

for (int num : nums) {
    if (set.contains(num)) {
        return true;
    }
    set.add(num);
}
return false;
```
### HasMap
```
HashMap<Integer, Integer> map = new HashMap<>();

for (int num : nums) {
    if (map.containsKey(num)) {
        return true;
    }
    map.put(num, 1);
}
return false;
```
### ArrayList
```
ArrayList<Integer> list = new ArrayList<>();

for (int num : nums) {
    if (list.contains(num)) {
        return true;
    }
    list.add(num);
}
return false;
```

**Why HashSet is preferred:**

HashSet.contains() → average O(1)

ArrayList.contains() → O(n)

**Overall:**

HashSet → O(n) time

ArrayList → O(n²) time


## Character Methods Cheat Sheet

| Method                      | Purpose                        |
| --------------------------- | ------------------------------ |
| `s.charAt(i)`               | Character at index             |
| `s.toCharArray()`           | Convert string to `char[]`     |
| `Character.isLetter(c)`     | Letter?                        |
| `Character.isDigit(c)`      | Digit?                         |
| `Character.isUpperCase(c)`  | Uppercase?                     |
| `Character.isLowerCase(c)`  | Lowercase?                     |
| `Character.isWhitespace(c)` | Space/tab/newline?             |
| `Character.toUpperCase(c)`  | Convert to uppercase           |
| `Character.toLowerCase(c)`  | Convert to lowercase           |
| `(int)c`                    | Character's numeric value      |
| `c - 'a'`                   | Alphabet index (0–25)          |
| `c - '0'`                   | Digit value (e.g. `'7'` → `7`) |

## HashMap Methods Cheat Sheet


| Method                       | Purpose                   |
| ---------------------------- | ------------------------- |
| `put(key, value)`            | Add/update                |
| `get(key)`                   | Get value                 |
| `getOrDefault(key, default)` | Get value or default      |
| `containsKey(key)`           | Check key exists          |
| `remove(key)`                | Delete key                |
| `isEmpty()`                  | Check empty               |
| `size()`                     | Number of key-value pairs |
| `keySet()`                   | All keys                  |
| `values()`                   | All values                |
| `entrySet()`                 | Key-value pairs           |


## Examples of Linear Collections

1. **Array**

   * Elements are stored in contiguous memory.
   * Fast access using an index.
   * Example: `[10, 20, 30, 40]`

2. **Linked List**

   * Each element (node) stores data and a reference to the next node.
   * Example:

     ```
     10 → 20 → 30 → 40 → NULL
     ```

3. **Stack**

   * Follows **LIFO (Last In, First Out)**.
   * Example: Stack of plates.

4. **Queue**

   * Follows **FIFO (First In, First Out)**.
   * Example: People waiting in a line.

## Linear vs. Non-Linear Collection

| Linear Collection                                           | Non-Linear Collection                                 |
| ----------------------------------------------------------- | ----------------------------------------------------- |
| Elements are arranged sequentially.                         | Elements are arranged hierarchically or as a network. |
| Each element has at most one predecessor and one successor. | A node can have multiple connections.                 |
| Easier to traverse sequentially.                            | Traversal is more complex.                            |
| Examples: Array, Linked List, Stack, Queue                  | Examples: Tree, Graph                                 |

