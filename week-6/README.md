Here is your **Day 1–Day 7 plan for Week 6**, focused on:

- Deepening your **recursion** skills
- Learning general **backtracking patterns**
- Applying them on classic LeetCode problems (subsets, permutations, combinations)
- Combining recursion with trees (path-based problems)

Assume ~2–3 hours per day; adjust as needed.

---

## Shared Mental Model for Week 6

**Recursion:** A function that calls itself with a smaller subproblem until a **base case** is reached.

**Backtracking:** Systematically exploring all configurations (paths, subsets, permutations) by:
1. Choosing an option
2. Recursing further
3. Undoing (backtracking) the choice

General backtracking template:

```java
void backtrack(State state) {
    if (foundSolutionOrReachedEnd(state)) {
        recordOrUseResult(state);
        return;
    }

    for (choice in possibleChoices(state)) {
        makeChoice(state, choice);
        backtrack(state);
        undoChoice(state, choice); // backtrack
    }
}
```

Keep this template in mind all week.

---

## Day 1 – Recursion Fundamentals (Non-Backtracking)

**Goals:**
- Get comfortable reading and writing simple recursive methods.
- Understand base case vs recursive case clearly.

### 1. Concept Primer (20–30 min)

Key ideas:
- Every recursive method needs:
  - **Base case**: condition to stop recursion.
  - **Recursive case**: call itself on a simpler input.
- Missteps:
  - No base case → infinite recursion.
  - Base case not reached → stack overflow.

### 2. Simple Recursion Exercises (60–75 min)

Create: `week6.day1.RecursionBasics`.

Implement the following recursively:

1. Factorial:
   ```java
   public static int factorial(int n) {
       if (n == 0) return 1;        // base case
       return n * factorial(n - 1); // recursive case
   }
   ```

2. Sum of first n natural numbers:
   ```java
   public static int sumToN(int n) {
       if (n == 0) return 0;
       return n + sumToN(n - 1);
   }
   ```

3. Reverse a string:
   ```java
   public static String reverse(String s) {
       if (s == null || s.length() <= 1) return s;
       return reverse(s.substring(1)) + s.charAt(0);
   }
   ```

4. Check if an array is sorted (strictly increasing) using recursion:
   ```java
   public static boolean isSorted(int[] arr, int index) {
       if (index == arr.length - 1) return true;
       if (arr[index] >= arr[index + 1]) return false;
       return isSorted(arr, index + 1);
   }
   ```

### 3. Recursive Tree DFS Revisit (30–45 min)

Create: `week6.day1.TreeRecap` (reuse your `TreeNode` from Week 5).

Re-implement from memory:

- `maxDepth(TreeNode root)`
- `sumNodes(TreeNode root)`

Focus on:
- Seeing each call as handling “current node + its subtrees.”
- How recursion naturally matches tree structure.

---

## Day 2 – Backtracking Concept & First Problem: Subsets

**Goals:**
- Understand backtracking as “explore + undo”.
- Implement a simple subsets generator.

### 1. Backtracking Concept (20–30 min)

Think of backtracking as exploring a **decision tree**:

At each step:
- Either you **include** an element or you **exclude** it.
- Or you choose one of many candidates and move forward.

Key ideas:
- Maintain a **current path** (e.g., `List<Integer> path`).
- On each recursion:
  - Add something to `path`.
  - Recurse.
  - Remove it (backtrack).

### 2. LeetCode: Subsets (78, Medium) (60–90 min)

Create: `week6.day2.LC78Subsets`.

**Problem:** Given `int[] nums`, return all possible subsets (the power set).

**Approach 1 – Backtracking with index:**

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums, int start, List<Integer> path, List<List<Integer>> result) {
    // Record current subset
    result.add(new ArrayList<>(path));

    for (int i = start; i < nums.length; i++) {
        path.add(nums[i]);                 // choose
        backtrack(nums, i + 1, path, result); // explore
        path.remove(path.size() - 1);      // undo (backtrack)
    }
}
```

Concepts reinforced:
- Using `start` to avoid reusing elements before index.
- Copying `path` into `result` (not reusing the same list).
- “Include current, recurse, then backtrack.”

### 3. Variation Exercise (30–45 min)

In the same or new class `SubsetsSizeK`:

- Generate all subsets of size exactly `k`.

Modify backtracking:
- Add a condition:
  - When `path.size() == k`, add copy to result and return.
- Prune when `path.size() > k`.

---

## Day 3 – Backtracking: Combinations (C(n, k))

**Goals:**
- Practice backtracking with index ranges.
- Learn to control combinations with start indices and pruning.

### 1. LeetCode: Combinations (77, Medium) (60–90 min)

Create: `week6.day3.LC77Combinations`.

**Problem:** Return all combinations of `k` numbers out of the range [1..n].

**Approach:**

```java
public List<List<Integer>> combine(int n, int k) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(1, n, k, new ArrayList<>(), result);
    return result;
}

private void backtrack(int start, int n, int k, List<Integer> path, List<List<Integer>> result) {
    if (path.size() == k) {
        result.add(new ArrayList<>(path));
        return;
    }

    for (int i = start; i <= n; i++) {
        path.add(i);
        backtrack(i + 1, n, k, path, result);
        path.remove(path.size() - 1);
    }
}
```

Optional enhancement: pruning
- When remaining numbers are not enough to fill the combination, break early.

Concepts reinforced:
- Using `start` to avoid duplicates and enforce increasing order.
- Recognizing combination vs permutation (order does not matter here).

### 2. Practice Variation (30–45 min)

Modify problem:
- Input: `int[] nums` (may be unsorted, distinct).
- Generate all combinations of length `k` using backtracking (similar to SubsetsSizeK).
- Sort `nums` first if needed.

### 3. Quick Written Reflection (15–20 min)

On paper, write:
- The backtracking template for combinations:
  - Parameters: `start`, `path`, `result`.
- How is this different from subsets?
  - Subsets: include path of any size.
  - Combinations: stop at size `k`.

---

## Day 4 – Backtracking: Permutations

**Goals:**
- Learn to generate all permutations of an array.
- Understand the difference between permutations and combinations.

### 1. Concept Primer: Permutations vs Combinations (15–20 min)

- **Combinations**: order does NOT matter. `{1,2}` == `{2,1}`.
- **Permutations**: order DOES matter. `[1,2]` and `[2,1]` are different.
- In permutations, you often:
  - Track which elements have been used with a `boolean[] used`.
  - Or you swap elements in place.

### 2. LeetCode: Permutations (46, Medium) (60–90 min)

Create: `week6.day4.LC46Permutations`.

**Approach 1 – Using `boolean[] used`:**

```java
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    boolean[] used = new boolean[nums.length];
    backtrack(nums, used, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums, boolean[] used, List<Integer> path, List<List<Integer>> result) {
    if (path.size() == nums.length) {
        result.add(new ArrayList<>(path));
        return;
    }

    for (int i = 0; i < nums.length; i++) {
        if (used[i]) continue;
        used[i] = true;
        path.add(nums[i]);
        backtrack(nums, used, path, result);
        path.remove(path.size() - 1);
        used[i] = false;
    }
}
```

Concepts reinforced:
- Tracking used elements.
- Full-length path as base case.

### 3. LeetCode: Permutations II (47, Medium) – Optional (60–75 min)

Create: `week6.day4.LC47PermutationsII`.

- `nums` may have duplicates; need unique permutations.
- Common pattern:
  - Sort array first.
  - In the loop:
    - Skip duplicates when `nums[i] == nums[i-1] && !used[i-1]`.

This is great for seeing how backtracking handles duplicates via ordering.

---

## Day 5 – Tree Paths & Backtracking

**Goals:**
- Combine your tree knowledge with recursion/backtracking.
- Practice path-based tree problems.

### 1. LeetCode: Path Sum II (113, Medium) (60–90 min)

Create: `week6.day5.LC113PathSumII`.

**Problem:** Return all root-to-leaf paths where sum of values equals targetSum.

**Approach:**
- Similar to Path Sum I, but store paths with backtracking.

```java
public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(root, targetSum, new ArrayList<>(), result);
    return result;
}

private void backtrack(TreeNode node, int remaining, List<Integer> path, List<List<Integer>> result) {
    if (node == null) return;

    path.add(node.val);

    if (node.left == null && node.right == null && remaining == node.val) {
        result.add(new ArrayList<>(path));
    } else {
        backtrack(node.left, remaining - node.val, path, result);
        backtrack(node.right, remaining - node.val, path, result);
    }

    path.remove(path.size() - 1); // backtrack
}
```

Concepts reinforced:
- Combining recursion with path tracking.
- Backtracking (adding/removing node values).

### 2. LeetCode: Binary Tree Paths (257, Easy) (45–60 min)

Create: `week6.day5.LC257BinaryTreePaths`.

**Problem:** Return all root-to-leaf paths as strings `"1->2->5"`.

**Approach:**
- Similar to Path Sum II.
- Track current path either as `List<Integer>` or as `StringBuilder` passed down recursively.
- More convenient is building string:

```java
private void dfs(TreeNode node, String path, List<String> result) {
    if (node == null) return;

    if (path.isEmpty()) path = Integer.toString(node.val);
    else path = path + "->" + node.val;

    if (node.left == null && node.right == null) {
        result.add(path);
    } else {
        dfs(node.left, path, result);
        dfs(node.right, path, result);
    }
}
```

Concepts reinforced:
- Path-building in recursion.
- Slight variation in state (string vs list).

### 3. Quick Reflection (15–20 min)

Write down:
- How backtracking in trees compares to backtracking on arrays:
  - In trees, choices are usually “go left / go right”.
  - In arrays, choices are selecting elements or indices.

---

## Day 6 – More Backtracking Practice & Variations

**Goals:**
- Practice another core backtracking problem.
- Solidify patterns of choices, recursion, and undoing choices.

### 1. LeetCode: Combination Sum (39, Medium) (60–90 min)

Create: `week6.day6.LC39CombinationSum`.

**Problem:** Given `candidates` and `target`, find all unique combinations where the candidate numbers sum to target. You may reuse same number multiple times.

**Approach:**

- Sort `candidates` (optional but helps pruning).
- Backtracking with index:

```java
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(candidates, target, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] candidates, int remaining, int start,
                       List<Integer> path, List<List<Integer>> result) {
    if (remaining == 0) {
        result.add(new ArrayList<>(path));
        return;
    }
    if (remaining < 0) return;

    for (int i = start; i < candidates.length; i++) {
        path.add(candidates[i]);
        backtrack(candidates, remaining - candidates[i], i, path, result); // i (not i+1) because reuse allowed
        path.remove(path.size() - 1);
    }
}
```

Concepts reinforced:
- When to pass `i` vs `i+1` as `start` (reuse vs no reuse).
- Using `remaining` as a constraint.

### 2. Optional: Combination Sum II (40, Medium) (45–60 min)

Create: `week6.day6.LC40CombinationSumII`.

- Each number may be used at most once.
- `candidates` may contain duplicates → avoid duplicate combinations.
- Pattern:
  - Sort `candidates`.
  - In loop, skip duplicates:
    ```java
    if (i > start && candidates[i] == candidates[i-1]) continue;
    ```

Concepts reinforced:
- Controlling duplicate combinations via sorted order and skipping.

### 3. Pattern Summary (20–30 min)

In your notes, summarize backtracking patterns:

- **Subsets:**  
  - Parameters: `start`, `path`  
  - Always record `path` at each node.
- **Combinations (fixed size k):**  
  - Stop when `path.size() == k`.
- **Permutations:**  
  - Use `used[]` or in-place swaps.
- **Combination Sum:**  
  - Use `remaining` target, prune when negative.

---

## Day 7 – Integration, Review, and Self-Test

**Goals:**
- Ensure you can recognize when recursion/backtracking is needed.
- Re-solve key problems from scratch.
- Consolidate patterns.

### 1. Written Concept Check (20–30 min)

Without code, write:

1. General backtracking template with:
   - `path`, `start`, and `result`.
2. Differences between:
   - Subsets vs Combinations vs Permutations.
3. Typical signs that a problem is suitable for backtracking:
   - “Return all subsets/paths/permutations/combinations…”
   - “Find all possible ways…”
   - “Generate all configurations…”

### 2. Re-solve Key Problems (60–90 min)

In **new files**, from scratch, solve at least **5**:

1. **Subsets (78, Medium)**  
2. **Combinations (77, Medium)**  
3. **Permutations (46, Medium)**  
4. **Path Sum II (113, Medium)**  
5. **Binary Tree Paths (257, Easy)**  
6. **Combination Sum (39, Medium)**  

For each:
- Write 3–5 lines of pseudocode before coding.
- After coding:
  - Identify pattern: subset/combination/permutation/path.
  - Time complexity (usually exponential, e.g., O(2^n) or O(n·n!)).
  - Space complexity (recursion stack + result).

### 3. Reflection & Prep for Week 7 (15–30 min)

Ask yourself:

1. Do I feel comfortable writing backtracking from a blank file?
2. Can I:
   - Track “used” elements correctly?
   - Understand why we add to path then remove (backtrack)?
   - Use `start` index to prevent duplicates/reuse?
3. Which backtracking problem type is hardest for me?  
   - Practice that one more time.

Week 7 will move into:

- Graphs (DFS/BFS on general graphs and grids)
- Introduction to Dynamic Programming (1D DP)

Both will reuse your recursion / DFS intuition and pattern-recognition skills from this week.

If you’d like, next I can:
- Generate a Day 1–7 plan for **Week 7 (Graphs + Intro DP)**, or
- Provide a **backtracking cheat sheet** summarizing common templates and pitfalls.
