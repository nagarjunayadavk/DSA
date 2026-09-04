# The 14 Core Algorithmic Patterns for Coding Interviews

> **Philosophy:** Don't memorize 500 individual LeetCode solutions. Master these **14 patterns**. Almost every interview question at top tech firms (Amazon, Google, Microsoft, Walmart, Razorpay, PhonePe) is a variation of one of these patterns.

---

## Pattern Quick Index

1. [Sliding Window](#1-sliding-window)
2. [Two Pointers](#2-two-pointers)
3. [Fast & Slow Pointers (Tortoise & Hare)](#3-fast--slow-pointers)
4. [Merge Intervals](#4-merge-intervals)
5. [Cyclic Sort](#5-cyclic-sort)
6. [In-Place Reversal of a Linked List](#6-in-place-reversal-of-a-linked-list)
7. [Tree Breadth-First Search (Level Order)](#7-tree-breadth-first-search-bfs)
8. [Tree Depth-First Search (DFS / Recursion)](#8-tree-depth-first-search-dfs)
9. [Two Heaps (Dynamic Median)](#9-two-heaps)
10. [Subsets & Backtracking](#10-subsets--backtracking)
11. [Modified Binary Search](#11-modified-binary-search)
12. [Top 'K' Elements (Heap / QuickSelect)](#12-top-k-elements)
13. [Monotonic Stack / Queue](#13-monotonic-stack--queue)
14. [Graph BFS & DFS (Topological Sort)](#14-graph-bfs--dfs-topological-sort)

---

## 1. Sliding Window

### When to Use / Trigger Words
* Problems involving **contiguous subarrays**, substrings, or sub-lists.
* Phrases: *"Longest substring with..."*, *"Subarray of size K with maximum sum"*, *"Minimum window containing all characters"*.

### Core Idea
Maintain two pointers `left` and `right`. Expand `right` to grow the window until a condition is met or violated, then shrink `left` to optimize.

### Java Template
```java
public int slidingWindowTemplate(String s) {
    int left = 0, maxLen = 0;
    Map<Character, Integer> counts = new HashMap<>();

    for (int right = 0; right < s.length(); right++) {
        char rChar = s.charAt(right);
        counts.put(rChar, counts.getOrDefault(rChar, 0) + 1);

        // Window invalid condition: shrink from left
        while (/* window is invalid condition */) {
            char lChar = s.charAt(left);
            counts.put(lChar, counts.get(lChar) - 1);
            if (counts.get(lChar) == 0) counts.remove(lChar);
            left++;
        }

        // Update answer
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

### Must-Solve Problems
- [LC 3] Longest Substring Without Repeating Characters (Medium)
- [LC 76] Minimum Window Substring (Hard)
- [LC 424] Longest Repeating Character Replacement (Medium)
- [LC 209] Minimum Size Subarray Sum (Medium)

---

## 2. Two Pointers

### When to Use / Trigger Words
* **Sorted arrays** or lists searching for pairs, triplets, or palindromes.
* Phrases: *"Find two numbers that sum to target"*, *"Remove duplicates in-place"*, *"Reverse array / palindrome check"*.

### Core Idea
Initialize `left = 0` and `right = nums.length - 1`. Compare values and move pointers inward:
- If `sum < target`, move `left++` to increase sum.
- If `sum > target`, move `right--` to decrease sum.

### Java Template
```java
public int[] twoSumSorted(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) {
            return new int[]{left, right};
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    return new int[]{-1, -1};
}
```

### Must-Solve Problems
- [LC 167] Two Sum II - Input Array Is Sorted (Medium)
- [LC 15] 3Sum (Medium)
- [LC 11] Container With Most Water (Medium)
- [LC 125] Valid Palindrome (Easy)

---

## 3. Fast & Slow Pointers

### When to Use / Trigger Words
* Linked lists or cyclic sequences.
* Phrases: *"Detect cycle in linked list"*, *"Find the middle node in single pass"*, *"Find starting node of cycle"*.

### Core Idea
`slow` advances by 1 node; `fast` advances by 2 nodes. If a cycle exists, `slow` and `fast` will eventually meet.

### Java Template
```java
public boolean hasCycle(ListNode head) {
    if (head == null) return false;
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true; // Cycle detected
    }
    return false;
}
```

### Must-Solve Problems
- [LC 141] Linked List Cycle (Easy)
- [LC 142] Linked List Cycle II (Medium - find cycle start)
- [LC 876] Middle of the Linked List (Easy)
- [LC 287] Find the Duplicate Number (Medium - Floyd's algorithm)

---

## 4. Merge Intervals

### When to Use / Trigger Words
* Intervals with start and end times.
* Phrases: *"Overlapping intervals"*, *"Meeting rooms"*, *"Merge schedule intervals"*.

### Core Idea
1. Sort intervals by `start` time: `Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]))`.
2. Iterate through: if `current.start <= previous.end`, merge by setting `previous.end = Math.max(previous.end, current.end)`.

### Java Template
```java
public int[][] merge(int[][] intervals) {
    if (intervals.length <= 1) return intervals;
    Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

    List<int[]> result = new ArrayList<>();
    int[] current = intervals[0];
    result.add(current);

    for (int[] interval : intervals) {
        if (interval[0] <= current[1]) {
            // Overlap: merge
            current[1] = Math.max(current[1], interval[1]);
        } else {
            // Disjoint: new interval
            current = interval;
            result.add(current);
        }
    }
    return result.toArray(new int[result.size()][]);
}
```

### Must-Solve Problems
- [LC 56] Merge Intervals (Medium)
- [LC 57] Insert Interval (Medium)
- [LC 435] Non-overlapping Intervals (Medium)
- [LC 253] Meeting Rooms II (Medium)

---

## 5. Cyclic Sort

### When to Use / Trigger Words
* Unsorted arrays containing numbers in a given range from `[0, n]` or `[1, n]`.
* Phrases: *"Find the missing number"*, *"Find the duplicate number in 1 to n"*, *"All numbers that disappeared"*.

### Core Idea
Place each number at its corresponding index in $O(N)$ time and $O(1)$ space. Number `x` belongs at index `x - 1`.

### Java Template
```java
public void cyclicSort(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        int correctIndex = nums[i] - 1; // For 1 to n range
        if (nums[i] > 0 && nums[i] <= nums.length && nums[i] != nums[correctIndex]) {
            swap(nums, i, correctIndex);
        } else {
            i++;
        }
    }
}
private void swap(int[] nums, int i, int j) {
    int temp = nums[i]; nums[i] = nums[j]; nums[j] = temp;
}
```

### Must-Solve Problems
- [LC 268] Missing Number (Easy)
- [LC 448] Find All Numbers Disappeared in an Array (Easy)
- [LC 442] Find All Duplicates in an Array (Medium)
- [LC 41] First Missing Positive (Hard)

---

## 6. In-Place Reversal of a Linked List

### When to Use / Trigger Words
* Reversing all or a sub-portion of a singly linked list without allocating auxiliary space ($O(1)$ memory).

### Core Idea
Maintain 3 pointers: `prev = null`, `curr = head`, and `next = null`. Invert pointers iteratively.

### Java Template
```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

### Must-Solve Problems
- [LC 206] Reverse Linked List (Easy)
- [LC 92] Reverse Linked List II (Between positions left and right) (Medium)
- [LC 25] Reverse Nodes in k-Group (Hard)

---

## 7. Tree Breadth-First Search (BFS)

### When to Use / Trigger Words
* Tree traversal **level by level**, finding shortest paths, or zigzag ordering.
* Phrases: *"Level order traversal"*, *"Minimum depth of binary tree"*, *"View of binary tree (left/right/top)"*.

### Core Idea
Use a `Queue<TreeNode>`. Inside the `while (!queue.isEmpty())` loop, loop `for (int i = 0; i < size; i++)` to process an entire level at once.

### Java Template
```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int levelSize = queue.size();
        List<Integer> currentLevel = new ArrayList<>(levelSize);

        for (int i = 0; i < levelSize; i++) {
            TreeNode node = queue.poll();
            currentLevel.add(node.val);

            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        result.add(currentLevel);
    }
    return result;
}
```

### Must-Solve Problems
- [LC 102] Binary Tree Level Order Traversal (Medium)
- [LC 103] Binary Tree Zigzag Level Order Traversal (Medium)
- [LC 199] Binary Tree Right Side View (Medium)
- [LC 111] Minimum Depth of Binary Tree (Easy)

---

## 8. Tree Depth-First Search (DFS)

### When to Use / Trigger Words
* Preorder, Inorder, or Postorder traversals.
* Phrases: *"Path sum"*, *"Maximum path sum"*, *"Validate Binary Search Tree"*, *"Lowest Common Ancestor"*.

### Core Idea
Solve recursively: compute the answer for left subtree, right subtree, and combine at the current root.

### Java Template (Max Path / Height)
```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    int leftDepth = maxDepth(root.left);
    int rightDepth = maxDepth(root.right);
    return 1 + Math.max(leftDepth, rightDepth);
}
```

### Must-Solve Problems
- [LC 112] Path Sum & [LC 113] Path Sum II (Medium)
- [LC 236] Lowest Common Ancestor of a Binary Tree (Medium)
- [LC 98] Validate Binary Search Tree (Medium)
- [LC 124] Binary Tree Maximum Path Sum (Hard)
- [LC 543] Diameter of Binary Tree (Easy)

---

## 9. Two Heaps

### When to Use / Trigger Words
* Maintaining the median of a dynamic stream of numbers, or balancing two partitions.
* Phrases: *"Find median from continuous data stream"*, *"Sliding window median"*.

### Core Idea
- `maxHeap`: stores the smaller half of numbers (top is the largest of the lower half).
- `minHeap`: stores the larger half of numbers (top is the smallest of the upper half).
- Maintain balance: `maxHeap.size() == minHeap.size()` or `maxHeap.size() == minHeap.size() + 1`.

### Java Template
```java
class MedianFinder {
    private PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    private PriorityQueue<Integer> minHeap = new PriorityQueue<>();

    public void addNum(int num) {
        maxHeap.offer(num);
        minHeap.offer(maxHeap.poll());
        if (maxHeap.size() < minHeap.size()) {
            maxHeap.offer(minHeap.poll());
        }
    }

    public double findMedian() {
        if (maxHeap.size() > minHeap.size()) return maxHeap.peek();
        return (maxHeap.peek() + minHeap.peek()) / 2.0;
    }
}
```

### Must-Solve Problems
- [LC 295] Find Median from Data Stream (Hard)
- [LC 480] Sliding Window Median (Hard)

---

## 10. Subsets & Backtracking

### When to Use / Trigger Words
* Generating all permutations, combinations, subsets, or solving constraint satisfactions (Sudoku, N-Queens).
* Phrases: *"Find all combinations that sum to target"*, *"Generate all permutations"*, *"Word search in grid"*.

### Core Idea
The 3-step Backtracking recipe:
1. **Choose:** Add candidate to the temporary list.
2. **Explore:** Call recursion with next index.
3. **Un-choose (Backtrack):** Remove the last added candidate before returning.

### Java Template
```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums, int start, List<Integer> current, List<List<Integer>> result) {
    result.add(new ArrayList<>(current)); // Deep copy

    for (int i = start; i < nums.length; i++) {
        current.add(nums[i]);              // 1. Choose
        backtrack(nums, i + 1, current, result); // 2. Explore
        current.remove(current.size() - 1);// 3. Backtrack
    }
}
```

### Must-Solve Problems
- [LC 78] Subsets & [LC 90] Subsets II (Medium)
- [LC 46] Permutations & [LC 47] Permutations II (Medium)
- [LC 39] Combination Sum & [LC 40] Combination Sum II (Medium)
- [LC 79] Word Search (Medium)

---

## 11. Modified Binary Search

### When to Use / Trigger Words
* Sorted or rotated sorted arrays, or **Binary Search on Answer Space** where answer is bounded within `[min, max]`.
* Phrases: *"Search in rotated sorted array"*, *"Find minimum in rotated array"*, *"Find peak element"*, *"Minimum capacity to ship packages"*.

### Core Idea
Avoid integer overflow using `int mid = left + (right - left) / 2`. Check which half is sorted, or whether a condition function `isPossible(mid)` returns true/false.

### Java Template (Binary Search on Answer Space)
```java
public int binarySearchOnAnswer(int[] weights, int days) {
    int left = maxElement(weights); // Smallest possible answer
    int right = sum(weights);       // Largest possible answer
    int ans = right;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (isValid(weights, days, mid)) {
            ans = mid;        // Candidate found, try to minimize
            right = mid - 1;
        } else {
            left = mid + 1;   // Not enough capacity, increase
        }
    }
    return ans;
}
```

### Must-Solve Problems
- [LC 33] Search in Rotated Sorted Array (Medium)
- [LC 153] Find Minimum in Rotated Sorted Array (Medium)
- [LC 875] Koko Eating Bananas (Medium)
- [LC 1011] Capacity To Ship Packages Within D Days (Medium)

---

## 12. Top 'K' Elements

### When to Use / Trigger Words
* Finding the $K$ largest, smallest, or most frequent elements in an unsorted stream or array.
* Phrases: *"Top K frequent items"*, *"Kth largest element"*, *"K closest points to origin"*.

### Core Idea
Instead of full sorting ($O(N \log N)$), use a **Min-Heap of size $K$** ($O(N \log K)$). Keep inserting; whenever heap size exceeds $K$, remove the minimum element (`heap.poll()`). The heap will retain the top $K$ largest elements.

### Java Template
```java
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    for (int num : nums) {
        minHeap.offer(num);
        if (minHeap.size() > k) {
            minHeap.poll(); // Discard smaller elements
        }
    }
    return minHeap.peek();
}
```

### Must-Solve Problems
- [LC 215] Kth Largest Element in an Array (Medium)
- [LC 347] Top K Frequent Elements (Medium)
- [LC 973] K Closest Points to Origin (Medium)
- [LC 692] Top K Frequent Words (Medium)

---

## 13. Monotonic Stack / Queue

### When to Use / Trigger Words
* Searching for the **Next Greater Element**, **Next Smaller Element**, or calculating bounded rectangular areas.
* Phrases: *"Daily temperatures"*, *"Next warmer day"*, *"Largest rectangle in histogram"*, *"Trapping rain water"*.

### Core Idea
Maintain elements in strictly monotonic (increasing or decreasing) order. When a new element violates the order, pop from the stack and compute the answer for the popped element.

### Java Template (Next Greater Element)
```java
public int[] dailyTemperatures(int[] temperatures) {
    int n = temperatures.length;
    int[] result = new int[n];
    Deque<Integer> stack = new ArrayDeque<>(); // Stores indices

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
            int prevIndex = stack.pop();
            result[prevIndex] = i - prevIndex;
        }
        stack.push(i);
    }
    return result;
}
```

### Must-Solve Problems
- [LC 739] Daily Temperatures (Medium)
- [LC 496] Next Greater Element I (Easy)
- [LC 503] Next Greater Element II (Circular) (Medium)
- [LC 84] Largest Rectangle in Histogram (Hard)
- [LC 42] Trapping Rain Water (Hard)

---

## 14. Graph BFS & DFS (Topological Sort)

### When to Use / Trigger Words
* Node/vertex networks, grids (2D matrices treated as graphs), dependency resolution, or cycle detection in Directed Acyclic Graphs (DAG).
* Phrases: *"Course prerequisite schedule"*, *"Number of islands"*, *"Shortest path in grid"*, *"Alien dictionary"*.

### Core Idea
- **Matrix DFS/BFS:** Use `visited[][]` or mutate in-place (e.g. `'1' -> '0'`).
- **Topological Sort (Kahn's Algorithm):** Compute in-degrees of all nodes. Push all nodes with `inDegree == 0` into a Queue. Pop, decrement neighbors' in-degrees, and repeat.

### Java Template (Topological Sort / Kahn's Algorithm)
```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    List<List<Integer>> adj = new ArrayList<>();
    for (int i = 0; i < numCourses; i++) adj.add(new ArrayList<>());
    int[] inDegree = new int[numCourses];

    for (int[] edge : prerequisites) {
        adj.get(edge[1]).add(edge[0]);
        inDegree[edge[0]]++;
    }

    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < numCourses; i++) {
        if (inDegree[i] == 0) queue.offer(i);
    }

    int visitedCount = 0;
    while (!queue.isEmpty()) {
        int node = queue.poll();
        visitedCount++;
        for (int neighbor : adj.get(node)) {
            if (--inDegree[neighbor] == 0) {
                queue.offer(neighbor);
            }
        }
    }
    return visitedCount == numCourses; // True if no cycle
}
```

### Must-Solve Problems
- [LC 200] Number of Islands (Medium)
- [LC 207] Course Schedule & [LC 210] Course Schedule II (Medium)
- [LC 994] Rotting Oranges (Medium - Multi-source BFS)
- [LC 133] Clone Graph (Medium)
- [LC 127] Word Ladder (Hard)
