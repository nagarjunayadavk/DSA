# Java DSA Scanner Input Guide: Problem-by-Problem Implementation

This guide provides standalone, complete, and runnable Java implementations for **every problem** located in the [javaCode](file:///e:/PSB/javaCode) folder.

In platforms like LeetCode, solutions only require implementing a method signature (`Solution` class). However, in **online assessments (OAs), HackerRank, Codeforces, TCS CodeVita, HackerEarth, and local terminal debugging**, you must read input from standard input (`System.in`) and print output to standard output (`System.out`).

---

## Table of Contents
1. [Core Scanner Reading Patterns & Pitfalls](#1-core-scanner-reading-patterns--pitfalls)
2. [Problem 1: Contains Duplicate (LC 217)](#problem-1-contains-duplicate-lc-217)
3. [Problem 2: Valid Anagram (LC 242)](#problem-2-valid-anagram-lc-242)
4. [Problem 3: Group Anagrams (LC 49)](#problem-3-group-anagrams-lc-49)
5. [Problem 4: Subsets (LC 78)](#problem-4-subsets-lc-78)
6. [Problem 5: Valid Sudoku (LC 36)](#problem-5-valid-sudoku-lc-36)
7. [Problem 6: Maximum Depth of Binary Tree (LC 104)](#problem-6-maximum-depth-of-binary-tree-lc-104)
8. [Problem 7: Number of Islands (LC 200)](#problem-7-number-of-islands-lc-200)
9. [Problem 8: Pacific Atlantic Water Flow (LC 417)](#problem-8-pacific-atlantic-water-flow-lc-417)
10. [Problem 9: Flood Fill (LC 733)](#problem-9-flood-fill-lc-733)
11. [Problem 10: Rotting Oranges (LC 994)](#problem-10-rotting-oranges-lc-994)
12. [Problem 11: Find if Path Exists in Graph (LC 1971)](#problem-11-find-if-path-exists-in-graph-lc-1971)
13. [Problem 12: Number of Connected Components (LC 323)](#problem-12-number-of-connected-components-lc-323)
14. [Problem 13: Sum of Subarray Ranges (LC 2104)](#problem-13-sum-of-subarray-ranges-lc-2104)
15. [Quick Reference Input Mapping Table](#15-quick-reference-input-mapping-table)

---

## 1. Core Scanner Reading Patterns & Pitfalls

### Common Scanner Methods
- `sc.nextInt()`: Reads the next integer token.
- `sc.nextLong()`: Reads the next 64-bit integer token.
- `sc.next()`: Reads the next single whitespace-delimited word/token.
- `sc.nextLine()`: Reads the entire line including spaces until the `\n` newline character.
- `sc.hasNextInt()`, `sc.hasNext()`: Checks if further input tokens exist (vital for variable-length or EOF inputs).

> [!WARNING]
> ### The `nextInt()` followed by `nextLine()` Trap
> When `sc.nextInt()` parses a number, it leaves the trailing newline (`\n`) in the input buffer. If you immediately call `sc.nextLine()`, it reads this leftover empty line instead of the expected string.
> **Solution:** Always consume the leftover newline by inserting an extra `sc.nextLine();` after `sc.nextInt()`.

```java
int n = sc.nextInt();
sc.nextLine(); // CONSUME leftover newline!
String line = sc.nextLine();
```

> [!TIP]
> ### Parsing LeetCode Array String Formats `"[1,2,3]"`
> Some coding platforms supply inputs formatted like `[1,2,3]` or `[[1,2],[3,4]]`. Clean them easily using:
> ```java
> String raw = sc.nextLine().trim();
> raw = raw.replace("[", "").replace("]", "").trim();
> if (!raw.isEmpty()) {
>     String[] parts = raw.split(",");
>     // parse each parts[i].trim()
> }
> ```

---

## Problem 1: Contains Duplicate (LC 217)
- **Source Files**: [0217-contains-duplicate.java](file:///e:/PSB/javaCode/0217-contains-duplicate.java), [submission-0 (1).java](file:///e:/PSB/javaCode/submission-0%20(1).java)
- **Topic**: Arrays & HashSets

### Input Format
- Line 1: An integer `n` denoting the number of elements.
- Line 2: `n` space-separated integers representing the array `nums`.

### Complete Executable Code
```java
import java.util.Scanner;
import java.util.HashSet;
import java.util.Set;

public class ContainsDuplicateMain {

    public static boolean containsDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<>();
        for (int n : nums) {
            if (!seen.add(n)) { // add returns false if already present
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Check if input is available
        if (!sc.hasNextInt()) {
            System.out.println("No input provided.");
            sc.close();
            return;
        }

        int n = sc.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        boolean result = containsDuplicate(nums);
        System.out.println(result);

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
4
1 2 3 1
```
**Output:**
```text
true
```

---

## Problem 2: Valid Anagram (LC 242)
- **Source File**: [submission-0 (2).java](file:///e:/PSB/javaCode/submission-0%20(2).java)
- **Topic**: Strings & Frequency Counting

### Input Format
- Line 1: First string `s`.
- Line 2: Second string `t`.

### Complete Executable Code
```java
import java.util.Scanner;
import java.util.HashMap;
import java.util.Map;

public class ValidAnagramMain {

    public static boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        // Frequency counter using Map (as in submission)
        Map<Character, Integer> counterMap = new HashMap<>();
        for (char c : s.toCharArray()) {
            counterMap.put(c, counterMap.getOrDefault(c, 0) + 1);
        }

        for (char c : t.toCharArray()) {
            if (!counterMap.containsKey(c)) {
                return false;
            }
            counterMap.put(c, counterMap.get(c) - 1);
            if (counterMap.get(c) == 0) {
                counterMap.remove(c);
            }
        }

        return counterMap.isEmpty();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNext()) {
            sc.close();
            return;
        }

        // sc.next() reads single tokens (skips whitespace)
        String s = sc.next();
        String t = sc.next();

        boolean result = isAnagram(s, t);
        System.out.println(result);

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
anagram
nagaram
```
**Output:**
```text
true
```

---

## Problem 3: Group Anagrams (LC 49)
- **Source File**: [submission-1.java](file:///e:/PSB/javaCode/submission-1.java)
- **Topic**: Strings, Sorting & HashMaps

### Input Format
- Line 1: An integer `n` denoting the number of strings.
- Line 2: `n` space-separated strings.
*(Alternatively, strings on each separate line).*

### Complete Executable Code
```java
import java.util.*;

public class GroupAnagramsMain {

    public static List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();

        for (String str : strs) {
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            String key = new String(chars);

            map.computeIfAbsent(key, k -> new ArrayList<>()).add(str);
        }

        return new ArrayList<>(map.values());
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextInt()) {
            sc.close();
            return;
        }

        int n = sc.nextInt();
        String[] strs = new String[n];
        for (int i = 0; i < n; i++) {
            strs[i] = sc.next();
        }

        List<List<String>> grouped = groupAnagrams(strs);

        // Printing groups in formatted output
        System.out.println("[");
        for (List<String> group : grouped) {
            System.out.println("  " + group);
        }
        System.out.println("]");

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
6
eat tea tan ate nat bat
```
**Output:**
```text
[
  [eat, tea, ate]
  [bat]
  [tan, nat]
]
```

---

## Problem 4: Subsets (LC 78)
- **Source File**: [0078-subsets.java](file:///e:/PSB/javaCode/0078-subsets.java)
- **Topic**: Backtracking / Cascading Iterative Generation

### Input Format
- Line 1: An integer `n`.
- Line 2: `n` integers representing elements of `nums`.

### Complete Executable Code
```java
import java.util.*;

public class SubsetsMain {

    public static List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        // Start by adding the empty subset
        result.add(new ArrayList<>()); 

        for (int num : nums) {
            int size = result.size();
            // Duplicate all existing subsets and add current number to each
            for (int i = 0; i < size; i++) {
                List<Integer> newSubset = new ArrayList<>(result.get(i));
                newSubset.add(num);
                result.add(newSubset);
            }
        }
        return result;        
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextInt()) {
            sc.close();
            return;
        }

        int n = sc.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        List<List<Integer>> allSubsets = subsets(nums);

        System.out.println("Total subsets: " + allSubsets.size());
        for (List<Integer> subset : allSubsets) {
            System.out.println(subset);
        }

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
3
1 2 3
```
**Output:**
```text
Total subsets: 8
[]
[1]
[2]
[1, 2]
[3]
[1, 3]
[2, 3]
[1, 2, 3]
```

---

## Problem 5: Valid Sudoku (LC 36)
- **Source File**: [submission-3.java](file:///e:/PSB/javaCode/submission-3.java)
- **Topic**: 2D Matrices, HashMaps & Validation

### Input Format
9 lines, each containing 9 characters (digits `1-9` or `.` for empty cells).
*(Can be separated by spaces or formatted as continuous 9-character lines).*

### Complete Executable Code
```java
import java.util.*;

public class ValidSudokuMain {

    public static boolean hasDuplicates(char[] charArr) {
        Map<Character, Integer> countMap = new HashMap<>();
        for (char c : charArr) {
            if (c == '.') {
                continue;
            }
            countMap.put(c, countMap.getOrDefault(c, 0) + 1);
            if (countMap.get(c) > 1) {
                return true;
            }
        }
        return false;
    }

    public static boolean isValidSudoku(char[][] board) {
        // 1. Check rows
        for (int i = 0; i < 9; i++) {
            if (hasDuplicates(board[i])) {
                return false;
            }
        }

        // 2. Check columns
        for (int col = 0; col < 9; col++) {
            char[] column = new char[9];
            for (int row = 0; row < 9; row++) {
                column[row] = board[row][col];
            }
            if (hasDuplicates(column)) {
                return false;
            }
        }

        // 3. Check 3x3 boxes
        for (int boxRow = 0; boxRow < 9; boxRow += 3) {
            for (int boxCol = 0; boxCol < 9; boxCol += 3) {
                char[] box = new char[9];
                int index = 0;
                for (int i = boxRow; i < boxRow + 3; i++) {
                    for (int j = boxCol; j < boxCol + 3; j++) {
                        box[index++] = board[i][j];
                    }
                }
                if (hasDuplicates(box)) {
                    return false;
                }
            }
        }

        return true;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        char[][] board = new char[9][9];

        for (int i = 0; i < 9; i++) {
            // Read line or next token
            String line = sc.next();
            // In case input is space-separated or has brackets, extract clean tokens
            line = line.replaceAll("[\\s,\"\\[\\]]", "");
            while (line.length() < 9 && sc.hasNext()) {
                line += sc.next().replaceAll("[\\s,\"\\[\\]]", "");
            }
            for (int j = 0; j < 9; j++) {
                board[i][j] = line.charAt(j);
            }
        }

        boolean valid = isValidSudoku(board);
        System.out.println(valid);

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
53..7....
6..195...
.98....6.
8...6...3
4..8.3..1
7...2...6
.6....28.
...419..5
....8..79
```
**Output:**
```text
true
```

---

## Problem 6: Maximum Depth of Binary Tree (LC 104)
- **Source File**: [0104-maximum-depth-of-binary-tree.java](file:///e:/PSB/javaCode/0104-maximum-depth-of-binary-tree/0104-maximum-depth-of-binary-tree.java)
- **Topic**: Binary Trees & Tree Reconstruction from Level-Order Input

> [!NOTE]
> Trees are provided in standard level-order traversal format in competitive programming and interview platforms: e.g., `3 9 20 null null 15 7` or `3 9 20 -1 -1 15 7`. The `buildTree` helper reconstructs the tree using a Queue.

### Complete Executable Code
```java
import java.util.*;

public class MaxDepthBinaryTreeMain {

    // TreeNode definition
    public static class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int val) { this.val = val; }
    }

    public static int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        return 1 + Math.max(leftDepth, rightDepth);
    }

    // Helper: Construct binary tree from level-order tokens
    public static TreeNode buildTree(String[] tokens) {
        if (tokens.length == 0 || tokens[0].equals("null") || tokens[0].equals("-1") || tokens[0].isEmpty()) {
            return null;
        }

        TreeNode root = new TreeNode(Integer.parseInt(tokens[0]));
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        int index = 1;
        while (!queue.isEmpty() && index < tokens.length) {
            TreeNode current = queue.poll();

            // Left child
            if (index < tokens.length) {
                String val = tokens[index++];
                if (!val.equals("null") && !val.equals("-1")) {
                    current.left = new TreeNode(Integer.parseInt(val));
                    queue.offer(current.left);
                }
            }

            // Right child
            if (index < tokens.length) {
                String val = tokens[index++];
                if (!val.equals("null") && !val.equals("-1")) {
                    current.right = new TreeNode(Integer.parseInt(val));
                    queue.offer(current.right);
                }
            }
        }
        return root;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read entire line containing tree values
        if (!sc.hasNextLine()) {
            sc.close();
            return;
        }

        String line = sc.nextLine().trim();
        // Clean brackets if input is like [3,9,20,null,null,15,7]
        line = line.replace("[", "").replace("]", "").replace(",", " ").trim();
        String[] tokens = line.split("\\s+");

        TreeNode root = buildTree(tokens);
        int depth = maxDepth(root);
        System.out.println("Maximum Depth: " + depth);

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
3 9 20 null null 15 7
```
**Output:**
```text
Maximum Depth: 3
```

---

## Problem 7: Number of Islands (LC 200)
- **Source File**: [0200-number-of-islands.java](file:///e:/PSB/javaCode/0200-number-of-islands/0200-number-of-islands.java)
- **Topic**: 2D Grid DFS / Connected Components

### Input Format
- Line 1: Two integers `m` and `n` (number of rows and columns).
- Next `m` lines: Each contains a string of `n` characters (`'1'` for land, `'0'` for water).

### Complete Executable Code
```java
import java.util.Scanner;

public class NumberOfIslandsMain {

    static void dfs(int row, int col, char[][] grid) {
        grid[row][col] = '0'; // Sink island
        int[] dir = {-1, 0, 1, 0, -1}; // (up, right, down, left)

        int rows = grid.length;
        int cols = grid[0].length;

        for (int i = 0; i < 4; i++) {
            int newRow = row + dir[i];
            int newCol = col + dir[i + 1];

            if (newRow >= 0 && newRow < rows &&
                newCol >= 0 && newCol < cols &&
                grid[newRow][newCol] == '1') {
                dfs(newRow, newCol, grid);
            }
        }
    }

    public static int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0) return 0;
        int islandCount = 0;
        int rows = grid.length;
        int cols = grid[0].length;

        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (grid[row][col] == '1') {
                    dfs(row, col, grid);
                    islandCount++;
                }
            }
        }
        return islandCount;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextInt()) {
            sc.close();
            return;
        }

        int m = sc.nextInt();
        int n = sc.nextInt();

        char[][] grid = new char[m][n];
        for (int i = 0; i < m; i++) {
            String rowStr = sc.next();
            grid[i] = rowStr.toCharArray();
        }

        int result = numIslands(grid);
        System.out.println("Number of Islands: " + result);

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
4 5
11110
11010
11000
00000
```
**Output:**
```text
Number of Islands: 1
```

---

## Problem 8: Pacific Atlantic Water Flow (LC 417)
- **Source File**: [0417-pacific-atlantic-water-flow.java](file:///e:/PSB/javaCode/0417-pacific-atlantic-water-flow/0417-pacific-atlantic-water-flow.java)
- **Topic**: 2D Grid Multi-source DFS (Reverse Flow)

### Input Format
- Line 1: Two integers `m` and `n`.
- Next `m` lines: `n` space-separated integers representing the height of each cell.

### Complete Executable Code
```java
import java.util.*;

public class PacificAtlanticMain {

    public static List<List<Integer>> pacificAtlantic(int[][] heights) {
        List<List<Integer>> result = new ArrayList<>();
        if (heights == null || heights.length == 0 || heights[0].length == 0) {
            return result;
        }

        int rows = heights.length;
        int cols = heights[0].length;

        boolean[][] pacific = new boolean[rows][cols];
        boolean[][] atlantic = new boolean[rows][cols];

        // DFS from top (Pacific) and bottom (Atlantic) rows
        for (int c = 0; c < cols; c++) {
            dfs(heights, 0, c, pacific, Integer.MIN_VALUE);
            dfs(heights, rows - 1, c, atlantic, Integer.MIN_VALUE);
        }

        // DFS from left (Pacific) and right (Atlantic) columns
        for (int r = 0; r < rows; r++) {
            dfs(heights, r, 0, pacific, Integer.MIN_VALUE);
            dfs(heights, r, cols - 1, atlantic, Integer.MIN_VALUE);
        }

        // Cells reaching both oceans
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (pacific[r][c] && atlantic[r][c]) {
                    result.add(Arrays.asList(r, c));
                }
            }
        }
        return result;
    }

    private static void dfs(int[][] heights, int r, int c, boolean[][] visited, int prevHeight) {
        if (r < 0 || r >= heights.length || c < 0 || c >= heights[0].length
                || visited[r][c] || heights[r][c] < prevHeight) {
            return;
        }

        visited[r][c] = true;
        int[] dir = {-1, 0, 1, 0, -1};

        for (int i = 0; i < 4; i++) {
            dfs(heights, r + dir[i], c + dir[i + 1], visited, heights[r][c]);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextInt()) {
            sc.close();
            return;
        }

        int m = sc.nextInt();
        int n = sc.nextInt();

        int[][] heights = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                heights[i][j] = sc.nextInt();
            }
        }

        List<List<Integer>> coordinates = pacificAtlantic(heights);
        System.out.println("Coordinates flowing to both oceans:");
        for (List<Integer> coord : coordinates) {
            System.out.println(coord.get(0) + " " + coord.get(1));
        }

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
5 5
1 2 2 3 5
3 2 3 4 4
2 4 5 3 1
6 7 1 4 5
5 1 1 2 4
```
**Output:**
```text
Coordinates flowing to both oceans:
0 4
1 3
1 4
2 2
3 0
3 1
4 0
```

---

## Problem 9: Flood Fill (LC 733)
- **Source File**: [0733-flood-fill.java](file:///e:/PSB/javaCode/0733-flood-fill/0733-flood-fill.java)
- **Topic**: 2D Grid DFS / Connected Component Coloring

### Input Format
- Line 1: Integers `m` and `n` (matrix dimensions).
- Next `m` lines: `n` space-separated integers for the image pixels.
- Next Line: Starting row `sr`, starting column `sc`, and `color` (new replacement color).

### Complete Executable Code
```java
import java.util.Scanner;

public class FloodFillMain {

    static void dfs(int[][] img, int x, int y, int oldColor, int newColor) {
        if (x < 0 || x >= img.length ||
            y < 0 || y >= img[0].length ||
            img[x][y] != oldColor) {
            return;
        }

        img[x][y] = newColor;

        dfs(img, x + 1, y, oldColor, newColor);
        dfs(img, x - 1, y, oldColor, newColor);
        dfs(img, x, y + 1, oldColor, newColor);
        dfs(img, x, y - 1, oldColor, newColor);
    }

    public static int[][] floodFill(int[][] image, int sr, int sc, int color) {
        if (image[sr][sc] == color) {
            return image;
        }
        int oldColor = image[sr][sc];
        dfs(image, sr, sc, oldColor, color);
        return image;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextInt()) {
            sc.close();
            return;
        }

        int m = sc.nextInt();
        int n = sc.nextInt();

        int[][] image = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                image[i][j] = sc.nextInt();
            }
        }

        int sr = sc.nextInt();
        int scCol = sc.nextInt();
        int color = sc.nextInt();

        floodFill(image, sr, scCol, color);

        System.out.println("Modified Matrix:");
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                System.out.print(image[i][j] + (j == n - 1 ? "" : " "));
            }
            System.out.println();
        }

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
3 3
1 1 1
1 1 0
1 0 1
1 1 2
```
**Output:**
```text
Modified Matrix:
2 2 2
2 2 0
2 0 1
```

---

## Problem 10: Rotting Oranges (LC 994)
- **Source File**: [0994-rotting-oranges.java](file:///e:/PSB/javaCode/0994-rotting-oranges/0994-rotting-oranges.java)
- **Topic**: 2D Grid Multi-source BFS

### Input Format
- Line 1: `m` (rows) and `n` (columns).
- Next `m` lines: `n` space-separated integers (0 = empty, 1 = fresh, 2 = rotten).

### Complete Executable Code
```java
import java.util.*;

public class RottingOrangesMain {

    public static int orangesRotting(int[][] grid) {
        int[] dir = { -1, 0, 1, 0, -1 };
        int rows = grid.length;
        int cols = grid[0].length;

        Deque<int[]> rottenOrangesPositions = new ArrayDeque<>();
        int freshCount = 0;

        // Locate all initially rotten oranges and count fresh ones
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (grid[row][col] == 2) {
                    rottenOrangesPositions.offer(new int[] {row, col});
                }
                if (grid[row][col] == 1) {
                    freshCount++;
                }
            }
        }

        int minutes = 0;

        // BFS level by level
        while (!rottenOrangesPositions.isEmpty() && freshCount > 0) {
            minutes++;
            int levelSize = rottenOrangesPositions.size();

            for (int i = 0; i < levelSize; i++) {
                int[] current = rottenOrangesPositions.poll();
                int currentRow = current[0];
                int currentCol = current[1];

                for (int d = 0; d < 4; d++) {
                    int newRow = currentRow + dir[d];
                    int newCol = currentCol + dir[d + 1];

                    if (newRow >= 0 && newRow < rows &&
                        newCol >= 0 && newCol < cols &&
                        grid[newRow][newCol] == 1) {

                        grid[newRow][newCol] = 2; // rot it
                        rottenOrangesPositions.offer(new int[] {newRow, newCol});
                        freshCount--;
                    }
                }
            }
        }

        return freshCount == 0 ? minutes : -1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextInt()) {
            sc.close();
            return;
        }

        int m = sc.nextInt();
        int n = sc.nextInt();

        int[][] grid = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }

        int time = orangesRotting(grid);
        System.out.println("Time taken: " + time);

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
3 3
2 1 1
1 1 0
0 1 1
```
**Output:**
```text
Time taken: 4
```

---

## Problem 11: Find if Path Exists in Graph (LC 1971)
- **Source File**: [1971-find-if-path-exists-in-graph.java](file:///e:/PSB/javaCode/1971-find-if-path-exists-in-graph/1971-find-if-path-exists-in-graph.java)
- **Topic**: Graph Traversal (DFS on Undirected Graph)

### Input Format
- Line 1: `n` (number of vertices) and `m` (number of edges).
- Next `m` lines: Two integers `u` and `v` representing an undirected edge between `u` and `v`.
- Last Line: `source` and `destination`.

### Complete Executable Code
```java
import java.util.*;

public class PathExistsGraphMain {

    static boolean dfs(int curr, int dest, List<List<Integer>> adj, boolean[] visited) {
        if (curr == dest) return true;
        visited[curr] = true;

        for (int neighbor : adj.get(curr)) {
            if (!visited[neighbor]) {
                if (dfs(neighbor, dest, adj, visited)) {
                    return true;
                }
            }
        }
        return false;
    }

    public static boolean validPath(int n, int[][] edges, int source, int destination) {
        boolean[] vis = new boolean[n];
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adj.add(new ArrayList<>());
        }

        for (int[] edge : edges) {
            adj.get(edge[0]).add(edge[1]);
            adj.get(edge[1]).add(edge[0]);
        }

        return dfs(source, destination, adj, vis);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextInt()) {
            sc.close();
            return;
        }

        int n = sc.nextInt();
        int m = sc.nextInt();

        int[][] edges = new int[m][2];
        for (int i = 0; i < m; i++) {
            edges[i][0] = sc.nextInt();
            edges[i][1] = sc.nextInt();
        }

        int source = sc.nextInt();
        int destination = sc.nextInt();

        boolean pathExists = validPath(n, edges, source, destination);
        System.out.println(pathExists);

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
3 3
0 1
1 2
2 0
0 2
```
**Output:**
```text
true
```

---

## Problem 12: Number of Connected Components (LC 323)
- **Source File**: [submission-0.java](file:///e:/PSB/javaCode/submission-0.java)
- **Topic**: Undirected Graph Components (DFS / BFS)

### Input Format
- Line 1: `n` (number of nodes labeled `0` to `n-1`) and `m` (number of edges).
- Next `m` lines: Two integers `nodeA` and `nodeB`.

### Complete Executable Code
```java
import java.util.*;

public class ConnectedComponentsMain {

    public static int countComponents(int n, int[][] edges) {
        // 1. Initialize adjacency list
        List<List<Integer>> adjacencyList = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adjacencyList.add(new ArrayList<>());
        }

        // 2. Build undirected graph
        for (int[] edge : edges) {
            int nodeA = edge[0];
            int nodeB = edge[1];
            adjacencyList.get(nodeA).add(nodeB);
            adjacencyList.get(nodeB).add(nodeA);
        }

        // 3. Track visited nodes
        boolean[] visited = new boolean[n];
        int componentCount = 0;

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                componentCount++;
                dfs(i, adjacencyList, visited);
            }
        }

        return componentCount;
    }

    private static void dfs(int currentNode, List<List<Integer>> adjacencyList, boolean[] visited) {
        visited[currentNode] = true;
        for (int neighbor : adjacencyList.get(currentNode)) {
            if (!visited[neighbor]) {
                dfs(neighbor, adjacencyList, visited);
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextInt()) {
            sc.close();
            return;
        }

        int n = sc.nextInt();
        int m = sc.nextInt();

        int[][] edges = new int[m][2];
        for (int i = 0; i < m; i++) {
            edges[i][0] = sc.nextInt();
            edges[i][1] = sc.nextInt();
        }

        int components = countComponents(n, edges);
        System.out.println("Total Connected Components: " + components);

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
5 3
0 1
1 2
3 4
```
**Output:**
```text
Total Connected Components: 2
```

---

## Problem 13: Sum of Subarray Ranges (LC 2104)
- **Source File**: [2104-sum-of-subarray-ranges.java](file:///e:/PSB/javaCode/2104-sum-of-subarray-ranges/2104-sum-of-subarray-ranges.java)
- **Topic**: Arrays, Subarrays & Ranges

### Input Format
- Line 1: `n` (number of elements in the array).
- Line 2: `n` space-separated integers `nums`.

### Complete Executable Code
```java
import java.util.Scanner;

public class SubarrayRangesMain {

    public static long subArrayRanges(int[] nums) {
        int n = nums.length;
        long sum = 0;

        for (int i = 0; i < n; i++) {
            int min = nums[i];
            int max = nums[i];

            for (int j = i; j < n; j++) {
                min = Math.min(min, nums[j]);
                max = Math.max(max, nums[j]);

                sum += (long) max - min;
            }
        }

        return sum;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextInt()) {
            sc.close();
            return;
        }

        int n = sc.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        long result = subArrayRanges(nums);
        System.out.println("Sum of Subarray Ranges: " + result);

        sc.close();
    }
}
```

### Sample Input & Output
**Input:**
```text
3
1 2 3
```
**Output:**
```text
Sum of Subarray Ranges: 4
```

---

## 15. Quick Reference Input Mapping Table

| Data Structure / Pattern | Typical Input Format | Recommended Scanner Pattern |
| :--- | :--- | :--- |
| **1D Integer Array** | `N` followed by `A1 A2 ... AN` | `int n = sc.nextInt(); int[] a = new int[n]; for(int i=0; i<n; i++) a[i] = sc.nextInt();` |
| **1D String Array** | `N` followed by `S1 S2 ... SN` | `int n = sc.nextInt(); String[] s = new String[n]; for(int i=0; i<n; i++) s[i] = sc.next();` |
| **2D Numeric Grid** | `R C` followed by `R` rows of `C` ints | `int[][] g = new int[r][c]; for(int i=0; i<r; i++) for(int j=0; j<c; j++) g[i][j] = sc.nextInt();` |
| **2D Character Grid** | `R C` followed by `R` lines of strings | `char[][] g = new char[r][c]; for(int i=0; i<r; i++) g[i] = sc.next().toCharArray();` |
| **Graph Edges** | `N M` followed by `M` edge pairs `u v` | `for(int i=0; i<m; i++) { int u=sc.nextInt(), v=sc.nextInt(); adj.get(u).add(v); adj.get(v).add(u); }` |
| **Binary Tree** | Level-order tokens `3 9 20 null ...` | `String[] tokens = sc.nextLine().split("\\s+");` then BFS Queue build. |
| **Until EOF** | Arbitrary number of lines / test cases | `while(sc.hasNext()) { ... }` or `while(sc.hasNextInt()) { ... }` |
| **Number of Testcases** | `T` followed by `T` independent inputs | `int T = sc.nextInt(); while(T-- > 0) { solve(sc); }` |
