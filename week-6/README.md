Here’s your **Week 6 – Day 1 to Day 7 plan**, focused on:

- Graph fundamentals (BFS & DFS)
- “Grid as graph” patterns (islands, flood fill)
- Backtracking (subsets, permutations, combinations)

Plan on ~1.5–2 hours/day. Keep the loop: concept → implement small pieces → LeetCode → short reflection.

---

## Week 6 Focus

- Graphs:
  - Adjacency list representations
  - DFS (recursive/stack) & BFS (queue)
  - Visited sets to avoid infinite loops
- Grids as implicit graphs
- Backtracking:
  - Subsets, permutations, combination sums

---

## Day 1 – Graph Basics & DFS/BFS Templates

**Goal:** Understand graph representation and generic DFS/BFS patterns in Java.

### 1. Concept: Graphs & Representation (25–30 min)

In your notes, capture:

- Graph types:
  - Directed vs undirected
  - Weighted vs unweighted (we’ll ignore weights for now)
- Representation (focus on adjacency list):
  - `List<List<Integer>>`
  - or `Map<Integer, List<Integer>>`

Example adjacency list:

```java
int n = 5;
List<List<Integer>> graph = new ArrayList<>();
for (int i = 0; i < n; i++) graph.add(new ArrayList<>());
graph.get(0).add(1);
graph.get(1).add(0);
// etc.
```

### 2. Implement DFS & BFS Templates (45–60 min)

Create a small demo graph (e.g. 0–1–2, 1–3, 3–4) and implement:

1. **DFS (recursive)**

```java
void dfs(int node, List<List<Integer>> graph, boolean[] visited) {
    if (visited[node]) return;
    visited[node] = true;
    System.out.println("Visited " + node);
    for (int nei : graph.get(node)) {
        dfs(nei, graph, visited);
    }
}
```

2. **BFS (queue)**

```java
void bfs(int start, List<List<Integer>> graph) {
    boolean[] visited = new boolean[graph.size()];
    Queue<Integer> q = new ArrayDeque<>();
    q.offer(start);
    visited[start] = true;

    while (!q.isEmpty()) {
        int node = q.poll();
        System.out.println("Visited " + node);
        for (int nei : graph.get(node)) {
            if (!visited[nei]) {
                visited[nei] = true;
                q.offer(nei);
            }
        }
    }
}
```

Test by running DFS and BFS starting from node `0`.

### 3. Simple Practice: Connected Components (20–30 min)

Implement:

```java
int countComponents(List<List<Integer>> graph) {
    int n = graph.size();
    boolean[] visited = new boolean[n];
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            count++;
            dfs(i, graph, visited); // reuse your DFS
        }
    }
    return count;
}
```

Test with a graph that has 2 separate components.

**Reflection (10–15 min)**  
- Differences in how DFS and BFS traverse.
- Importance of `visited` to avoid infinite loops.

---

## Day 2 – Grids as Graphs: Number of Islands, Flood Fill

**Goal:** See 2D grids as graphs and apply DFS/BFS to them.

### 1. Concept: Treating Grids as Graphs (25–30 min)

Key ideas:

- Each cell `(r, c)` is a node.
- Edges to neighbors: usually up, down, left, right (4-dir).
- Use `visited[r][c]` to avoid revisiting.
- DFS/BFS structure is similar; you just check bounds and cell values.

Directions array:

```java
int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
```

### 2. LeetCode – Number of Islands (`#200`, Medium) (60–75 min)

Implement using DFS (or BFS if you prefer):

- For each cell:
  - If `grid[r][c] == '1'` and not visited:
    - Increment island count.
    - DFS/BFS from this cell, marking all connected land as visited.

Skeleton:

```java
void dfs(char[][] grid, int r, int c) {
    int rows = grid.length, cols = grid[0].length;
    if (r < 0 || r >= rows || c < 0 || c >= cols) return;
    if (grid[r][c] != '1') return;

    grid[r][c] = '0'; // mark visited
    dfs(grid, r+1, c);
    dfs(grid, r-1, c);
    dfs(grid, r, c+1);
    dfs(grid, r, c-1);
}
```

Count islands by scanning the grid and calling `dfs` when you see a '1'.

### 3. LeetCode – Flood Fill (`#733`, Easy/Medium) (30–45 min)

- Given image matrix, starting point `(sr, sc)`, and new color, fill connected region.
- Similar DFS/BFS with boundary and color checks.

**Reflection (10–15 min)**  
- Notice how `Number of Islands` and `Flood Fill` are essentially the same DFS/BFS pattern with different interpretations.

---

## Day 3 – More Grid Graphs: Max Area, Enclaves (Optional), and Practice

**Goal:** Reinforce grid DFS/BFS patterns and get comfortable altering what you compute.

### 1. Concept: Varying What You Track (20–30 min)

In these problems, DFS/BFS is the same; only **what you compute** changes:

- Count components (islands).
- Area/size of component.
- Perimeter, boundary touching, etc.

Think about:

- Using DFS/BFS to accumulate a count/area.
- Returning values from recursion or using a mutable holder (e.g., class field, or local array).

### 2. LeetCode – Max Area of Island (`#695`, Medium) (45–60 min)

Similar to `#200`, but instead of just counting islands:

- For each island, compute its area (number of cells).
- Track a global max.

Pseudo-DFS:

```java
int dfs(int[][] grid, int r, int c) {
    int rows = grid.length, cols = grid[0].length;
    if (r < 0 || r >= rows || c < 0 || c >= cols) return 0;
    if (grid[r][c] != 1) return 0;

    grid[r][c] = 0; // mark visited
    int area = 1;
    area += dfs(grid, r+1, c);
    area += dfs(grid, r-1, c);
    area += dfs(grid, r, c+1);
    area += dfs(grid, r, c-1);
    return area;
}
```

### 3. Optional / Extra Grid Problem (30–45 min)

Pick one (optional but good reinforcement):

- **Island Perimeter** (`#463`, Easy)
- **Number of Enclaves** (`#1020`, Medium – similar to islands but edges matter)

Focus on reusing the same DFS/BFS shape.

### 4. Quick Re-solve / Review (15–20 min)

- Re-scan your code for `#200` and `#733`.
- Identify common template pieces you can reuse.

**Reflection (10–15 min)**  
- How similar did `#200`, `#695`, `#733` feel?
- Write a generic “DFS on grid” template you can adapt later.

---

## Day 4 – Backtracking Basics: Subsets & Permutations

**Goal:** Learn the core backtracking pattern and apply it to simple combinatorial problems.

### 1. Concept: Backtracking Template (25–30 min)

General pattern:

```java
void backtrack(STATE current, CHOICES choices, RESULT result) {
    if (reachedEndCondition) {
        result.add(copyOfCurrentState);
        return;
    }

    for (choice in choices) {
        if (invalidChoice) continue;
        makeChoice(choice);
        backtrack(updatedState);
        undoChoice(choice); // backtrack
    }
}
```

Key ideas:

- Represent current partial solution (e.g., `List<Integer> path`).
- At each step:
  - Make a choice → recurse → undo choice.

### 2. LeetCode – Subsets (`#78`, Medium) (45–60 min)

Goal: all subsets (power set) of `nums`.

Skeleton:

```java
void backtrack(int[] nums, int start, List<Integer> path, List<List<Integer>> res) {
    res.add(new ArrayList<>(path)); // record current subset
    for (int i = start; i < nums.length; i++) {
        path.add(nums[i]);
        backtrack(nums, i + 1, path, res);
        path.remove(path.size() - 1); // undo
    }
}
```

Call with `start = 0` and empty `path`.

### 3. LeetCode – Permutations (`#46`, Medium) (45–60 min)

Goal: all permutations of array `nums`.

Approaches:

- Use `visited[]` or
- Swap in place.

Using visited array:

```java
void backtrack(int[] nums, boolean[] used, List<Integer> path, List<List<Integer>> res) {
    if (path.size() == nums.length) {
        res.add(new ArrayList<>(path));
        return;
    }
    for (int i = 0; i < nums.length; i++) {
        if (used[i]) continue;
        used[i] = true;
        path.add(nums[i]);
        backtrack(nums, used, path, res);
        path.remove(path.size() - 1);
        used[i] = false;
    }
}
```

**Reflection (10–15 min)**  
- Compare Subsets vs Permutations backtracking structure.
- What changes? (start index vs used[], stopping condition.)

---

## Day 5 – Backtracking: Combination Sum & Variants

**Goal:** Practice backtracking with sum constraints and repeated numbers.

### 1. Concept: Combinations with Target Sum (20–30 min)

Key ideas:

- Sort inputs if needed (for pruning or deduplication).
- Track:
  - current list
  - current sum or remaining sum
  - index from which to consider choices

### 2. LeetCode – Combination Sum (`#39`, Medium) (60–75 min)

- Candidates: can be reused multiple times.
- Required: unique combinations (order doesn’t matter).

Skeleton:

```java
void backtrack(int[] candidates, int start, int target, 
               List<Integer> path, List<List<Integer>> res) {
    if (target == 0) {
        res.add(new ArrayList<>(path));
        return;
    }
    if (target < 0) return;

    for (int i = start; i < candidates.length; i++) {
        path.add(candidates[i]);
        backtrack(candidates, i, target - candidates[i], path, res); // i, not i+1, reuse allowed
        path.remove(path.size() - 1);
    }
}
```

### 3. Optional: Combination Sum II or Subsets II (45–60 min)

If you feel comfortable:

- **Combination Sum II** (`#40`, Medium, optional)
  - Each candidate can be used at most once.
  - Handle duplicates (sort array, skip same values at same recursion level).
- Or **Subsets II** (`#90`, Medium – subsets with duplicates).

Even if you only partially implement, focus on the idea of skipping duplicates:

```java
if (i > start && nums[i] == nums[i-1]) continue;
```

**Reflection (10–15 min)**  
- How is Combination Sum different from Subsets?
- How does the `start` index control reuse vs non-reuse of elements?

---

## Day 6 – Mixed Practice: Graph (Grid) + Backtracking

**Goal:** Consolidate Week 6 topics with a mix of problems.

### 1. Quick Recap (20–30 min)

In your notebook, summarize:

- DFS/BFS template on adjacency list.
- DFS template on grid.
- Backtracking template (state, choices, backtrack step).

### 2. LeetCode – Graph/Grid Re-solve (45–60 min)

Choose 2–3 to solve (again if needed):

- `#200 Number of Islands`
- `#695 Max Area of Island`
- `#733 Flood Fill`

Try to implement without looking at old code.

### 3. LeetCode – Backtracking Re-solve (45–60 min)

Choose 2–3:

- `#78 Subsets`
- `#46 Permutations`
- `#39 Combination Sum`

Aim to improve:

- Speed.
- Clarity of your backtracking structure.

**Reflection (10–15 min)**  
- Which pattern feels more natural: grid DFS/BFS or backtracking?
- For any confusion, write down a specific example where you got stuck.

---

## Day 7 – Review, Integration, and Light Stretch

**Goal:** Tie together graph and backtracking skills; preview slightly harder problems.

### 1. Concept Review (30–40 min)

Write short explanations:

- What is a **visited** structure, and why is it crucial in graph problems?
- When to use:
  - DFS vs BFS in graphs.
  - Backtracking vs DP vs greedy (high-level intuition).
- For backtracking:
  - What does “state” consist of?
  - How do you undo a choice?

### 2. Timed Problem Set (60–90 min)

Pick 4–5 problems across graphs and backtracking. Give yourself **≤25–30 min** per problem.

Suggested set:

- From graphs/grids:
  - `#200 Number of Islands`
  - `#695 Max Area of Island`
  - `#733 Flood Fill`
- From backtracking:
  - `#78 Subsets`
  - `#46 Permutations`
  - `#39 Combination Sum`

For each:
1. 5–7 min: think on paper (pattern, outline).
2. Code and test.

### 3. Stretch Problems (Optional, 30–45 min)

Pick one or two to at least *attempt*:

- **Clone Graph** (`#133`, Medium) – graph DFS/BFS + HashMap cloning
- **Word Search** (`#79`, Medium) – backtracking on a grid
- **Letter Combinations of a Phone Number** (`#17`, Medium) – backtracking with characters

Even partial progress is useful. Focus on identifying:

- Graph/backtracking pattern.
- State, choices, constraints.

**Reflection (10–15 min)**  
- Which new pattern this week do you feel most confident in (grids, subsets, permutations, combos)?
- Which one needs another round of practice? Note it for later review weeks.

---

## How Week 6 Fits the Bigger Picture

By the end of Week 6, you should:

- Be comfortable with:
  - Representing and traversing **graphs** (especially grids) via DFS/BFS.
  - Common grid problems like islands and flood fill.
  - **Backtracking** on arrays and grids for subsets, permutations, and combination sums.
- Recognize when problems ask you to explore **all possibilities** (backtracking) vs searching in a **graph-like structure** (DFS/BFS).

Next (Week 7), you’ll:

- Learn **Dynamic Programming** basics:
  - 1D DP (Climbing Stairs, House Robber)
  - 2D DP (grid paths, subsequences)
  - Turning recursion into DP states and transitions.

If you’d like, I can next generate a **Week 7 – Day 1–7 plan** focused entirely on DP.
