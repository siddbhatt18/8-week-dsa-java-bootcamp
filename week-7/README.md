Here is your **Day 1–Day 7 plan for Week 7**, focused on:

- Graphs and grids with **DFS/BFS**
- Graph representations (adjacency list, visited sets)
- Intro **Dynamic Programming (DP)** with classic 1D patterns

Assume ~2–3 hours per day; adjust as needed.

---

## Day 1 – Graph Basics & Adjacency Lists

**Goals:**
- Understand what graphs are.
- Learn adjacency list representation.
- Write simple DFS and BFS on an unweighted graph.

### 1. Concept Primer (20–30 min)

Key terms:
- **Graph**: nodes (vertices) + edges.
- Directed vs undirected.
- Weighted vs unweighted.
- Typical representations:
  - **Adjacency list**: `List<List<Integer>>` or `Map<Integer, List<Integer>>`
  - **Adjacency matrix**: `int[][]` (less common in coding interviews; use for dense graphs).

Use adjacency list by default.

### 2. Build Adjacency Lists (45–60 min)

Create: `week7.day1.GraphBasics`.

**Tasks:**

1. Given number of nodes `n` and an edge list `int[][] edges` for an undirected graph:
   ```java
   public static List<List<Integer>> buildGraph(int n, int[][] edges) {
       List<List<Integer>> graph = new ArrayList<>();
       for (int i = 0; i < n; i++) {
           graph.add(new ArrayList<>());
       }
       for (int[] e : edges) {
           int u = e[0], v = e[1];
           graph.get(u).add(v);
           graph.get(v).add(u); // remove for directed
       }
       return graph;
   }
   ```

2. Test with:
   - `n = 4`, edges: `[[0,1],[1,2],[2,3],[3,0]]` (a cycle).
   - Print adjacency list.

### 3. Simple DFS & BFS on Graph (45–60 min)

In the same class:

1. **DFS (recursive)**:
   ```java
   public static void dfs(int node, List<List<Integer>> graph, boolean[] visited) {
       visited[node] = true;
       System.out.print(node + " ");
       for (int nei : graph.get(node)) {
           if (!visited[nei]) {
               dfs(nei, graph, visited);
           }
       }
   }
   ```

2. **BFS (iterative with queue)**:
   ```java
   public static void bfs(int start, List<List<Integer>> graph) {
       boolean[] visited = new boolean[graph.size()];
       Queue<Integer> queue = new ArrayDeque<>();
       visited[start] = true;
       queue.offer(start);
       while (!queue.isEmpty()) {
           int node = queue.poll();
           System.out.print(node + " ");
           for (int nei : graph.get(node)) {
               if (!visited[nei]) {
                   visited[nei] = true;
                   queue.offer(nei);
               }
           }
       }
   }
   ```

Run DFS and BFS starting from node 0 and compare orders.

---

## Day 2 – Graph Connected Components & Grids as Graphs

**Goals:**
- Count connected components in a graph using DFS.
- See how **2D grids** can be treated as graphs.

### 1. Connected Components in an Undirected Graph (45–60 min)

Create: `week7.day2.ConnectedComponents`.

**Task:**

Implement:
```java
public static int countComponents(int n, int[][] edges) {
    List<List<Integer>> graph = buildGraph(n, edges);
    boolean[] visited = new boolean[n];
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            count++;
            dfs(i, graph, visited);
        }
    }
    return count;
}
```

- Reuse `buildGraph` and `dfs` from Day 1 or copy them.

Concepts reinforced:
- “Start DFS/BFS from every unvisited node” to count components.

### 2. Grids as Graphs: Concept (20–30 min)

Think of a 2D grid `char[][] grid`:

- Each cell `(r, c)` is a node.
- Edges between adjacent cells (up/down/left/right) if valid.
- Use `visited[r][c]` or modify grid in-place (e.g., marking as '0').

You’ll use this for “Number of Islands” and similar problems.

### 3. Helper: DFS on a Grid (30–45 min)

Create: `week7.day2.GridDFS`.

Implement a generic flood-fill method:
```java
int rows = grid.length, cols = grid[0].length;

private void dfsGrid(char[][] grid, int r, int c) {
    if (r < 0 || c < 0 || r >= rows || c >= cols) return;
    if (grid[r][c] != '1') return; // or any target char

    grid[r][c] = '0'; // mark visited

    dfsGrid(grid, r + 1, c);
    dfsGrid(grid, r - 1, c);
    dfsGrid(grid, r, c + 1);
    dfsGrid(grid, r, c - 1);
}
```

Just test with a small toy grid to ensure it doesn’t crash.

---

## Day 3 – LeetCode Grids: Number of Islands & Max Area of Island

**Goals:**
- Apply DFS/BFS on grids.
- Solve two core grid/graph problems.

### 1. LeetCode: Number of Islands (200, Medium) (60–90 min)

Create: `week7.day3.LC200NumberOfIslands`.

**Problem:** Count connected components of '1's (land) in a 2D grid.

**Approach (DFS):**
- Iterate over all cells.
- When you see '1':
  - Increment count.
  - Call DFS to sink/flood all connected '1's to '0'.

Pattern:
```java
public int numIslands(char[][] grid) {
    int rows = grid.length, cols = grid[0].length;
    int count = 0;
    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {
            if (grid[r][c] == '1') {
                count++;
                dfs(grid, r, c);
            }
        }
    }
    return count;
}
```

Concepts reinforced:
- Grids as graphs.
- DFS flood-fill.

### 2. LeetCode: Max Area of Island (695, Medium) (45–60 min)

Create: `week7.day3.LC695MaxAreaOfIsland`.

**Problem:** Similar to Number of Islands, but return the largest area (count of cells) in any island.

**Approach:**
- Almost same DFS, but have DFS return area:
  ```java
  private int dfs(int[][] grid, int r, int c) {
      if (out of bounds or grid[r][c] == 0) return 0;
      grid[r][c] = 0;
      int area = 1;
      area += dfs(grid, r+1, c);
      area += dfs(grid, r-1, c);
      area += dfs(grid, r, c+1);
      area += dfs(grid, r, c-1);
      return area;
  }
  ```

- Track `maxArea = max(maxArea, dfs(...))`.

Concepts reinforced:
- DFS returning aggregated values.
- Very similar pattern to previous problem.

---

## Day 4 – Graph Traversal: Clone Graph & Intro to DP

**Goals:**
- Practice DFS/BFS in a general graph with a HashMap.
- Start basic DP thinking.

### 1. LeetCode: Clone Graph (133, Medium) (60–90 min)

Create: `week7.day4.LC133CloneGraph`.

LeetCode provides `Node { int val; List<Node> neighbors; }`.

**Idea:**
- Use a `Map<Node, Node>` to map original → clone.
- DFS or BFS:
  - If node already cloned (in map), return it.
  - Else:
    - Clone current node.
    - Recursively/iteratively clone neighbors.

DFS version sketch:
```java
private Map<Node, Node> map = new HashMap<>();

public Node cloneGraph(Node node) {
    if (node == null) return null;
    if (map.containsKey(node)) return map.get(node);

    Node clone = new Node(node.val);
    map.put(node, clone);
    for (Node nei : node.neighbors) {
        clone.neighbors.add(cloneGraph(nei));
    }
    return clone;
}
```

Concepts reinforced:
- Graph traversal with adjacency lists.
- Handling cycles via visited/map.

### 2. Intro DP Concept (20–30 min)

Key DP ideas:
- **Overlapping subproblems**: same subcomputations appear multiple times.
- **Optimal substructure**: optimal solution can be built from optimal subsolutions.
- Common approaches:
  - **Top-down (memoization)**: recursion + caching.
  - **Bottom-up (tabulation)**: iteratively fill DP array.

You’ll start with very simple 1D DP.

### 3. Classic DP Warm-Up: Fibonacci with Memoization & Tabulation (30–45 min)

Create: `week7.day4.DPBasics`.

Implement:

1. **Top-down Fibonacci**:
   ```java
   public int fibMemo(int n, int[] memo) {
       if (n <= 1) return n;
       if (memo[n] != -1) return memo[n];
       memo[n] = fibMemo(n-1, memo) + fibMemo(n-2, memo);
       return memo[n];
   }
   ```

2. **Bottom-up Fibonacci**:
   ```java
   public int fibTab(int n) {
       if (n <= 1) return n;
       int[] dp = new int[n+1];
       dp[0] = 0;
       dp[1] = 1;
       for (int i = 2; i <= n; i++) {
           dp[i] = dp[i-1] + dp[i-2];
       }
       return dp[n];
   }
   ```

Concepts reinforced:
- Storing results to avoid recomputation.
- 1D DP array.

---

## Day 5 – DP: Climbing Stairs & House Robber

**Goals:**
- Learn 1D DP for simple recurrence problems.
- Recognize DP patterns in LeetCode.

### 1. LeetCode: Climbing Stairs (70, Easy) (45–60 min)

Create: `week7.day5.LC70ClimbingStairs`.

**Problem:** Ways to climb `n` stairs, steps of 1 or 2.

**DP approach:**
- `dp[i] = dp[i-1] + dp[i-2]`
- Base: `dp[0] = 1` (1 way to stay at bottom), `dp[1] = 1`.

Space-optimized version:
```java
public int climbStairs(int n) {
    if (n <= 2) return n;
    int a = 1, b = 2; // ways to reach step 1 and 2
    for (int i = 3; i <= n; i++) {
        int c = a + b;
        a = b;
        b = c;
    }
    return b;
}
```

Concepts reinforced:
- Recognizing Fibonacci-like DP.
- Simple space optimization.

### 2. LeetCode: House Robber (198, Medium) (60–75 min)

Create: `week7.day5.LC198HouseRobber`.

**Problem:** Max sum of non-adjacent houses.

**DP approach:**
- `dp[i]` = max money you can rob from first `i+1` houses.
- Recurrence:
  - `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`
- Base:
  - `dp[0] = nums[0]`
  - `dp[1] = max(nums[0], nums[1])`

Space-optimized approach:
```java
public int rob(int[] nums) {
    if (nums.length == 1) return nums[0];
    int prev2 = nums[0];                // dp[i-2]
    int prev1 = Math.max(nums[0], nums[1]); // dp[i-1]
    for (int i = 2; i < nums.length; i++) {
        int curr = Math.max(prev1, prev2 + nums[i]);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

Concepts reinforced:
- “Take or skip” DP pattern.
- Translating problem text into recurrence.

### 3. Quick Check: Maximum Subarray (53, Easy/Medium) (30–45 min)

Create: `week7.day5.LC53MaximumSubarray`.

Use Kadane’s algorithm (DP-ish):

```java
public int maxSubArray(int[] nums) {
    int curr = nums[0];
    int best = nums[0];
    for (int i = 1; i < nums.length; i++) {
        curr = Math.max(nums[i], curr + nums[i]);
        best = Math.max(best, curr);
    }
    return best;
}
```

Concepts reinforced:
- Local vs global optimum.
- 1D running DP.

---

## Day 6 – Mixed Graph & DP Practice

**Goals:**
- Combine your new skills in graph DFS/BFS and basic DP.
- Reinforce patterns with more problems or re-solve.

### 1. Re-solve or Revisit Graph Problems (60–75 min)

Pick at least **2** of:

1. **Number of Islands (200)** – DFS on grid  
2. **Max Area of Island (695)** – DFS with return value  
3. **Clone Graph (133)** – DFS/BFS with HashMap  

For each:
- Try solving in a **new file** from scratch.
- Avoid looking at previous code; rely on your understanding of the pattern.

After solving:
- Write in comments:
  - Pattern used: DFS grid / DFS general graph / BFS.
  - Time complexity and space complexity.

### 2. Practice DP Problems Again (45–60 min)

Re-solve from scratch (new files):

1. **Climbing Stairs (70)**  
2. **House Robber (198)**  
3. **Maximum Subarray (53)**

Focus on:
- Writing recurrence in comments first.
- Then coding the DP/optimized version.

---

## Day 7 – Integration, Review & Self-Test

**Goals:**
- Ensure graph and DP fundamentals are solid.
- Practice recognizing which pattern to use.

### 1. Written Concept Check (20–30 min)

Without code, answer:

1. Graphs:
   - What is an adjacency list?
   - Differences between DFS and BFS in terms of:
     - Data structure used
     - Typical use cases
2. Grids:
   - How do you treat a 2D grid as a graph?
   - Typical DFS base conditions for grid flood-fill.
3. DP:
   - What is overlapping subproblems?
   - Difference between memoization and tabulation.
   - Write the recurrence for:
     - Climbing Stairs
     - House Robber

### 2. Self-Test: Solve 4–6 Problems from Scratch (60–90 min)

In new files, attempt at least **4** of these:

**Graphs / Grids:**
1. **Number of Islands (200, Medium)**  
2. **Max Area of Island (695, Medium)**  
3. **Clone Graph (133, Medium)**  

**DP:**
4. **Climbing Stairs (70, Easy)**  
5. **House Robber (198, Medium)**  
6. **Maximum Subarray (53, Easy/Medium)**  

For each:
- Spend up to 20–25 minutes thinking before checking hints.
- After coding, add a brief summary:
  - “Pattern: DFS on grid” / “Pattern: 1D DP”
  - Complexity.

### 3. Reflection & Prep for Week 8 (15–30 min)

Reflect:

1. Do graphs feel less intimidating now?
   - Can I implement DFS/BFS from scratch?
   - Can I convert between problem description and a graph/grid model?
2. Does DP make basic sense?
   - Can I derive simple 1D recurrences?
   - Do you feel the difference between greedy vs DP vs brute force?

Note down:
- Any graph or DP problems that felt weak.
- Specific patterns to reinforce (e.g., grid DFS, adjacency list, 1D DP).

In **Week 8**, you’ll:
- Push DP a bit further (2D/grid DP, coin change, unique paths).
- Do more mixed practice combining arrays, trees, graphs, and DP.

If you want next, I can:
- Generate the **Week 8 (Day 1–7) plan focusing on 2D DP & mixed review**, or  
- Provide a concise **Graph + Basic DP cheat sheet** (patterns, templates, and common pitfalls).
