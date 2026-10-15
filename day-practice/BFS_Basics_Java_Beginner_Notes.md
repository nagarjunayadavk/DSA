# BFS Basics in Java --- Beginner Notes

## 1. What is BFS?

**BFS (Breadth-First Search)** visits nearby nodes first, then moves
farther away. It explores a graph level by level.

Example graph:

``` text
        0
       / \
      1   2
     / \
    3   4
```

Starting at node `0`, one possible BFS order is:

`0 → 1 → 2 → 3 → 4`

BFS is useful for: - Traversing a graph level by level. - Finding
shortest paths in an unweighted graph. - Exploring a maze/grid. -
Finding connected components when started from every unvisited node. -
Problems where something spreads step by step.

### Understand these 3 concepts
- Queue: Processes cells in FIFO order.
- Visited: Prevents visiting the same cell repeatedly.
- Direction array: Moves up, down, left, and right.

## 2. The two key tools

### Queue --- FIFO

FIFO means **First In, First Out**. The first node added is the first
node removed.

``` java
Queue<Integer> queue = new ArrayDeque<>();
queue.offer(0);       // add 0
int node = queue.poll(); // remove the front node
```

### Visited array

A visited array prevents processing the same node repeatedly, especially
when a graph contains cycles.

``` java
boolean[] visited = new boolean[n];
```

### Direction Array
``` java
int[][] directions = {
    {-1, 0}, {1, 0},
    {0, -1}, {0, 1}
};
// or
// int[][] directions = {-1, 0, 1, 0, -1};
```

**Important:** In standard BFS, mark a node visited when you add it to
the queue.

## 3. Basic BFS Java example

This graph has edges `0–1`, `0–2`, `1–3`, and `1–4`.

``` java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        int n = 5;

        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        graph.get(0).add(1);
        graph.get(0).add(2);
        graph.get(1).add(0);
        graph.get(1).add(3);
        graph.get(1).add(4);
        graph.get(2).add(0);
        graph.get(3).add(1);
        graph.get(4).add(1);

        boolean[] visited = new boolean[n];
        Queue<Integer> queue = new ArrayDeque<>();

        queue.offer(0);
        visited[0] = true;

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");

            for (int neighbor : graph.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.offer(neighbor);
                }
            }
        }
    }
}
```

Output:

``` text
0 1 2 3 4
```

## 4. How do the `while` and `for` loops work together?

Remember:

-   The **`while` loop** takes the next node from the queue.
-   The **`for` loop** checks all neighbors of that one node.
-   After the `for` loop finishes, execution returns to the `while`
    condition.
-   The `while` loop stops when the queue becomes empty.

Execution order:

1.  Check `!queue.isEmpty()`.
2.  Remove one node with `queue.poll()`.
3.  Check every neighbor using the `for` loop.
4.  Mark unvisited neighbors and add them to the queue.
5.  Finish the `for` loop.
6.  Return to the `while` condition and process the next queued node.
7.  Stop when the queue is empty.

**Adding a node to the queue does not immediately process that node's
neighbors.** Its neighbors are processed later, when the `while` loop
removes that node.

### Queue walkthrough

  Stage         Action                                   Queue after action
  ------------- ---------------------------------------- --------------------
  Start         Add `0`                                  `[0]`
  Process `0`   Remove `0`; add `1, 2`                   `[1, 2]`
  Process `1`   Remove `1`; `0` is visited; add `3, 4`   `[2, 3, 4]`
  Process `2`   Remove `2`; no new unvisited neighbors   `[3, 4]`
  Process `3`   Remove `3`; its neighbor is visited      `[4]`
  Process `4`   Remove `4`; its neighbor is visited      `[]`
  Finish        Queue is empty                           BFS stops

### 1.Understand the two loops

- `while` loop: Picks the next node from the queue to process.
- `for` loop: Checks all neighbors of that one node.

The `for` loop does not restart the `while` loop itself. It finishes checking the current node's neighbors, and then the `while` loop checks the queue again.


### 2. Your main doubt: when does each loop run?

Imagine this sequence:

``` java
while (!queue.isEmpty()) {        // 1. Check queue
    int node = queue.poll();      // 2. Remove one node

    for (int neighbor : graph.get(node)) {  // 3. Check its neighbors
        if (!visited[neighbor]) {
            visited[neighbor] = true;
            queue.offer(neighbor);          // 4. Add neighbors
        }
    }

    // 5. The for loop is finished.
    //    Go back to the while condition.
}
```

The execution order is:

1. `while` checks the queue.
2. `poll()` removes one node.
3. `for` checks every neighbor of that node.
4. New neighbors are added to the queue.
5. The `for` loop finishes.
6. `while` checks the queue again and removes the next node.
7. Repeat until the queue is empty.

Important: Adding nodes to the queue does not immediately execute the `for` loop for those nodes. Their neighbors are processed only when the `while` loop removes them later.

## 5. BFS template to remember

``` java
Queue<Integer> queue = new ArrayDeque<>();
boolean[] visited = new boolean[n];

queue.offer(start);
visited[start] = true;

while (!queue.isEmpty()) {
    int node = queue.poll();

    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            visited[neighbor] = true;
            queue.offer(neighbor);
        }
    }
}
```

For a disconnected graph, start BFS from every unvisited node:

``` java
for (int i = 0; i < n; i++) {
    if (!visited[i]) {
        // Start BFS from i
    }
}
```


## 6. Beginner LeetCode / NeetCode practice order

Try these in order. Focus on understanding the pattern, not solving
quickly.

### Level 1 --- First understand traversal

1.  **BFS traversal of a graph** --- practise implementing the basic
    queue pattern.
    -   [NeetCode Roadmap](https://neetcode.io/roadmap)
    -   [LeetCode problems](https://leetcode.com/problemset/)
2.  **Number of Islands --- LeetCode 200**\
    Practise grid BFS/DFS and counting connected groups.
    -   [LeetCode](https://leetcode.com/problems/number-of-islands/)
    -   [NeetCode
        solution](https://neetcode.io/solutions/number-of-islands)
3.  **Max Area of Island --- LeetCode 695**\
    Practise counting the size of each connected group.
    -   [LeetCode](https://leetcode.com/problems/max-area-of-island/)
    -   [NeetCode
        solution](https://neetcode.io/solutions/max-area-of-island)

### Level 2 --- BFS for shortest paths

4.  **Shortest Path in Binary Matrix --- LeetCode 1091**\
    Practise distance tracking and shortest paths in a grid.
    -   [LeetCode](https://leetcode.com/problems/shortest-path-in-binary-matrix/)
    -   [NeetCode
        solution](https://neetcode.io/solutions/shortest-path-in-binary-matrix)
5.  **Nearest Exit from Entrance in Maze --- LeetCode 1926**\
    Practise boundary checks and shortest distance.
    -   [LeetCode](https://leetcode.com/problems/nearest-exit-from-entrance-in-maze/)
6.  **Rotting Oranges --- LeetCode 994**\
    Practise **multi-source BFS**: put every initially rotten orange
    into the queue, then process the spread level by level.
    -   [LeetCode](https://leetcode.com/problems/rotting-oranges/)
    -   [NeetCode
        solution](https://neetcode.io/solutions/rotting-oranges)

Note: Rotting Oranges uses **multi-source BFS**, not multi-source DFS.

## 7. Hidden-test checklist

Before submitting, check:

-   Minimum input size.
-   A one-cell grid, when applicable.
-   Blocked start or destination, when applicable.
-   Destination cannot be reached.
-   Disconnected graph.
-   Cycles or repeated edges, if allowed by the problem.
-   Maximum constraints and time complexity.
-   Correctly mark nodes visited when enqueuing them.

## 8. Complexity

-   BFS with an adjacency list: `O(V + E)` time and `O(V)` auxiliary
    space.
-   BFS on a grid with `R` rows and `C` columns: `O(R × C)` time in the
    worst case.

## 9. Today's assignment

1.  Read the basic BFS code and explain each line out loud.
2.  Trace the queue by hand for the example graph.
3.  Solve **Number of Islands** in Java.
4.  Test one normal case, one small case, and one tricky case.
5.  Only then move to **Max Area of Island**.

**Remember:** `while` chooses the next node; `for` checks that node's
neighbors.
