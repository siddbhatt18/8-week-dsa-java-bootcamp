**Week 8 Focus:**  
- Backtracking (subsets, combinations, permutations)  
- Systematic search + pruning  
- Combining recursion with earlier patterns  
- A few mixed/harder problems to stretch your thinking

Assume ~2–3 hours/day. Keep the loop: think on paper → code → test → reflect.

---

## Mental Model for Backtracking (for the Whole Week)

Write this at the top of your Week 8 notes:

```java
void backtrack(STATE state) {
    if (reached a complete solution) {
        record it;
        return;
    }

    for (each valid choice at this step) {
        make the choice;           // modify state
        backtrack(updated state);  // recurse
        undo the choice;           // restore state (backtrack)
    }
}
```

Key responsibilities:
- Define what a **“state”** is (current path, index, remaining target, etc.).
- Define **when a solution is complete**.
- Define **choices** you can make at each step.
- Implement **undo step** cleanly (backtracking).

---

## Day 1 – Backtracking Basics + Subsets

### 1. Concept: What Is Backtracking? (30–40 min)

On paper:

- It’s **depth-first search** on the space of choices.
- Used when:
  - You need to **generate all** combinations, permutations, subsets, etc.
  - You want to **search** for valid configurations (e.g., Sudoku, N‑Queens).
- Core ingredients:
  - Partial solution (`path`)
  - Choices left to explore
  - Base condition (when the path is “complete”)

Draw a small example for subsets of `[1,2]`:

- Decision tree like:
  - Start: `[]`
    - Include 1 → `[1]`
      - Include 2 → `[1,2]`
      - Exclude 2 → `[1]`
    - Exclude 1 → `[]`
      - Include 2 → `[2]`
      - Exclude 2 → `[]`

### 2. Problem: Subsets (Medium) – LC 78 (40–60 min)

Paraphrase:
- Given an array of distinct integers `nums`, return all possible subsets (the power set).

Think on paper (15–20 min):

Option A – index-based recursion:
- `backtrack(startIndex, path)`:
  - Add current `path` to result (every node is a valid subset).
  - For `i` from `startIndex` to end:
    - Add `nums[i]` to path.
    - Recurse with `startIndex = i + 1`.
    - Remove `nums[i]` from path (backtrack).

Identify:
- State: `startIndex` and `path`.
- Complete solution: Actually, **every** path is a valid subset.
- Choices: which index to pick next.

Coding (in `Week8Day1.java`):

```java
List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    backtrack(0, nums, new ArrayList<>(), res);
    return res;
}

void backtrack(int start, int[] nums, List<Integer> path, List<List<Integer>> res) {
    res.add(new ArrayList<>(path)); // add current subset

    for (int i = start; i < nums.length; i++) {
        path.add(nums[i]);
        backtrack(i + 1, nums, path, res);
        path.remove(path.size() - 1); // undo
    }
}
```

Test with `nums = [1,2,3]`.

### 3. Reflection (10–15 min)

Write:
- In your own words:
  - What does `start` represent?
  - Why do we copy `path` when adding to `res`?
- Trace through a small example manually to see recursion & undo steps.

---

## Day 2 – Combinations (Fixed Length) + Template Reinforcement

### 1. Quick Review (10–15 min)

- Without looking, rewrite the method signature and key idea for `subsets`.
- On paper, draw the recursion tree for `nums = [1,2]`.

### 2. Problem: Combinations – LC 77 (40–60 min)

Paraphrase:
- Given two integers `n` and `k`, return all possible combinations of `k` numbers out of `[1..n]`.

Think on paper (15–20 min):

- Representation:
  - `backtrack(start, path)`:
    - If `path.size() == k`, record it and return.
    - For `i` from `start` to `n`:
      - Add `i` to path.
      - `backtrack(i + 1, path)`
      - Remove last element.

Identify:
- State: `start` integer, `path` list.
- Base case: `path.size() == k`.
- Choices: pick each next number from the range.

Coding (`Week8Day2.java`):

```java
List<List<Integer>> combine(int n, int k) {
    List<List<Integer>> res = new ArrayList<>();
    backtrack(1, n, k, new ArrayList<>(), res);
    return res;
}

void backtrack(int start, int n, int k, List<Integer> path, List<List<Integer>> res) {
    if (path.size() == k) {
        res.add(new ArrayList<>(path));
        return;
    }
    for (int i = start; i <= n; i++) {
        path.add(i);
        backtrack(i + 1, n, k, path, res);
        path.remove(path.size() - 1);
    }
}
```

Test with `n = 4, k = 2`.

### 3. (Optional) Pruning Idea (10–15 min)

On paper:
- You can prune when it’s impossible to reach size `k`:
  - If remaining numbers `< (k - path.size())`, break the loop.
- Roughly: `for (int i = start; i <= n - (k - path.size()) + 1; i++)`

You don’t have to code it now, but understand that pruning narrows search.

### 4. Reflection (10–15 min)

Write:
- Compare `subsets` and `combine`:
  - What changed in base condition?
  - What changed in how we treat `path`?

---

## Day 3 – Permutations (Order Matters)

### 1. Quick Review (10–15 min)

- State & base case for `combine(n, k)` in one paragraph.
- How do you make a choice and then undo it?

### 2. Concept: Permutations vs Combinations (20–30 min)

On paper:

- Combination:
  - Order does not matter (`[1,2]` same as `[2,1]`).
- Permutation:
  - Order matters (`[1,2]` different from `[2,1]`).

In permutations, you usually:
- Keep track of *used* elements (e.g., `boolean[] used`).
- When building `path` of length `n`, at each step you can choose any unused element.

### 3. Problem: Permutations – LC 46 (45–60 min)

Paraphrase:
- Given an array `nums` of distinct integers, return all possible permutations.

Think on paper (15–20 min):

- `backtrack(path, used[])`:
  - If `path.size() == nums.length`, record path (copy) and return.
  - For each index `i`:
    - If `used[i]` is false:
      - Mark `used[i] = true`.
      - Add `nums[i]` to path.
      - Recurse.
      - Undo: remove last from path, set `used[i] = false`.

Coding (`Week8Day3.java`):

```java
List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    boolean[] used = new boolean[nums.length];
    backtrack(nums, used, new ArrayList<>(), res);
    return res;
}

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

Test with `nums = [1,2,3]`.

### 4. Reflection (10–15 min)

Write:
- How is this different from `subsets` and `combine`?
- What role does `used[]` play?
- Why can’t you just use `start` like in combinations for permutations?

---

## Day 4 – Combination Sum (Unbounded Choices)

### 1. Quick Review (10–15 min)

- Describe, in words, how the permutation algorithm works:
  - When do you stop?
  - How do you enforce “no reuse” of the same index at the same level?

### 2. Concept: Combination Sum – LC 39 (35–45 min)

Paraphrase:
- Given an array `candidates` (distinct positive ints) and a `target`:
  - Find all unique combinations where chosen numbers sum to `target`.
  - You may use each number **unlimited** times.
  - Order of numbers in a combination doesn’t matter (`[2,3,2]` is same as `[2,2,3]`, so treat it as one).

Think on paper (20–25 min):

- Sort candidates optionally (helps reasoning but not required).
- Use `backtrack(startIndex, remainingTarget, path)`:
  - If `remainingTarget == 0`: record `path`.
  - If `remainingTarget < 0`: return (invalid).
  - For `i` from `startIndex` to `candidates.length - 1`:
    - Choose `candidates[i]`:
      - Add to path.
      - Recurse with:
        - `startIndex = i` (since unlimited reuse of this candidate).
        - `remainingTarget - candidates[i]`.
      - Undo (remove last element).

Identify:
- State: `startIndex`, `remainingTarget`, `path`.
- Choices: each candidate index from `startIndex` onward.

### 3. Coding: Combination Sum (45–60 min)

In `Week8Day4.java`:

```java
List<List<Integer>> combinationSum(int[] candidates, int target) {
    List<List<Integer>> res = new ArrayList<>();
    Arrays.sort(candidates); // not strictly necessary, but nice
    backtrack(0, target, candidates, new ArrayList<>(), res);
    return res;
}

void backtrack(int start, int remain, int[] candidates, List<Integer> path, List<List<Integer>> res) {
    if (remain == 0) {
        res.add(new ArrayList<>(path));
        return;
    }
    if (remain < 0) {
        return; // overshoot
    }
    for (int i = start; i < candidates.length; i++) {
        path.add(candidates[i]);
        backtrack(i, remain - candidates[i], candidates, path, res);
        path.remove(path.size() - 1);
    }
}
```

Test with:
- `candidates = [2,3,6,7], target = 7` → `[ [2,2,3], [7] ]`.

### 4. Reflection (10–15 min)

Write:
- Why do we pass `i` (not `i+1`) when recursing?
- What changes conceptually if reuse is not allowed?

---

## Day 5 – Handling Duplicates: Subsets II / Combination Sum II

### 1. Quick Review (10–15 min)

- Re‑explain why `combinationSum` uses `i` instead of `i + 1` in recursion.
- What does that allow?

### 2. Concept: Duplicates & Avoiding Duplicate Results (25–35 min)

On paper:

When the input has duplicates and **order doesn’t matter**, you must avoid:
- Generating `[1,2]` and `[2,1]` as separate solutions.
- Generating combinations that are the same due to repeated equal values at different indices.

Key pattern:
- **Sort the array**.
- In loop `for (int i = start; i < n; i++)`:
  - Skip duplicates at same level:
    ```java
    if (i > start && nums[i] == nums[i - 1]) continue;
    ```

This prevents exploring branches that differ only by choosing a duplicate candidate index in a different order at the same recursion depth.

### 3. Problem: Subsets II – LC 90 (40–60 min)

Paraphrase:
- Like Subsets, but `nums` may contain duplicates.
- Return all possible subsets without duplicate subsets.

Think:

- Sort `nums` first.
- Use similar pattern as Subsets:
  - `backtrack(start, path)`:
    - Record path each time.
    - For `i` from `start` to `n`:
      - If `i > start && nums[i] == nums[i - 1]` → `continue` (skip duplicate at this level).
      - Add `nums[i]`.
      - Recurse with `i + 1`.
      - Undo.

Coding (`Week8Day5.java`):

```java
List<List<Integer>> subsetsWithDup(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(0, nums, new ArrayList<>(), res);
    return res;
}

void backtrack(int start, int[] nums, List<Integer> path, List<List<Integer>> res) {
    res.add(new ArrayList<>(path));
    for (int i = start; i < nums.length; i++) {
        if (i > start && nums[i] == nums[i - 1]) continue;
        path.add(nums[i]);
        backtrack(i + 1, nums, path, res);
        path.remove(path.size() - 1);
    }
}
```

Test with `nums = [1,2,2]`.

### 4. (Optional) Problem: Combination Sum II – LC 40 (Harder) (30–40 min)

Paraphrase:
- Like Combination Sum, but:
  - Each candidate may be used **at most once**.
  - There can be duplicates in `candidates`.
  - Need unique combinations.

Idea:
- Sort array.
- Backtracking similar to `CombinationSum`, but:
  - Recurse with `i+1` (not `i`) because you cannot reuse the same index.
  - Skip duplicates with `if (i > start && candidates[i] == candidates[i-1]) continue;`.

Even if you don’t fully code it, outline on paper:
- State, base cases, and the `i > start && ...` condition.

### 5. Reflection (10–15 min)

Write:
- Why do you have the condition `i > start && nums[i] == nums[i - 1]`?
- What would happen without it in `subsetsWithDup`?

---

## Day 6 – Mixed: Word Search (Grid + Backtracking)

### 1. Quick Review (10–15 min)

- List the problems you’ve solved so far with backtracking:
  - Subsets, Combinations, Permutations, Combination Sum, etc.
- Note for each whether order matters and whether duplicates exist.

### 2. Concept: Backtracking on a Grid – Word Search – LC 79 (35–45 min)

Paraphrase:
- Given a 2D board and a word, determine if the word exists in the grid.
- Word can be constructed from letters of sequentially adjacent cells (up, down, left, right).
- The same cell may not be used more than once in a path.

Think on paper:

- Grid search + backtracking:
  - For each cell `(r,c)`:
    - If `board[r][c] == word[0]`, start DFS/backtracking from here.
  - `search(r, c, index)`:
    - If `index == word.length` → found word, return true.
    - Check boundaries, check `board[r][c] == word[index]`.
    - Mark cell as visited (temporarily, e.g., set to `'#'` or track in `boolean[][] visited`).
    - Recurse in 4 directions with `index + 1`.
    - Undo visited mark (backtrack).
    - If any direction returns true → propagate true.

### 3. Coding: Word Search (45–60 min)

In `Week8Day6.java`:

1. Implement:

```java
boolean exist(char[][] board, String word) {
    int rows = board.length, cols = board[0].length;
    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {
            if (dfs(board, word, r, c, 0)) {
                return true;
            }
        }
    }
    return false;
}

boolean dfs(char[][] board, String word, int r, int c, int index) {
    if (index == word.length()) return true;
    if (r < 0 || r >= board.length || c < 0 || c >= board[0].length) return false;
    if (board[r][c] != word.charAt(index)) return false;

    char temp = board[r][c];
    board[r][c] = '#'; // mark visited

    int[][] dirs = {{1,0}, {-1,0}, {0,1}, {0,-1}};
    for (int[] d : dirs) {
        if (dfs(board, word, r + d[0], c + d[1], index + 1)) {
            board[r][c] = temp; // undo before returning
            return true;
        }
    }
    board[r][c] = temp; // undo
    return false;
}
```

2. Test on small boards.

3. Then solve LC **79. Word Search** on LeetCode.

### 4. Reflection (10–15 min)

Write:
- How is this similar to your grid DFS from “Number of Islands”?
- What’s new / trickier here (e.g., tracking the word index, revisiting cells)?

---

## Day 7 – Consolidation & Mixed Backtracking Practice

### 1. Concept Review (30–40 min)

On paper, for each of these problems:

- Subsets (78)
- Combinations (77)
- Permutations (46)
- Combination Sum (39)
- Subsets II (90)
- Word Search (79)

Write:

1. What is the **state**?
2. What is the **base case** / completion condition?
3. What are the **choices** at each step?
4. How do you **undo** your choice?

This step is crucial – it builds your pattern recognition.

### 2. Re‑implement from Memory (60–75 min)

In `Week8Review.java`, re‑implement:

1. `List<List<Integer>> subsets(int[] nums)`
2. `List<List<Integer>> combine(int n, int k)`
3. `List<List<Integer>> permute(int[] nums)`
4. `List<List<Integer>> combinationSum(int[] candidates, int target)`
5. `List<List<Integer>> subsetsWithDup(int[] nums)`
6. `boolean exist(char[][] board, String word)` (Word Search)

For each, add comments:
- 1–2 lines describing the idea.
- Time complexity (roughly exponential, but write the intuitive form, e.g., O(2^n), O(n!), etc.).
- Space complexity (recursion depth + path storage).

### 3. LeetCode Mini‑Session (60–75 min)

On LeetCode (fresh editor, no code copy):

1. **78. Subsets (Medium)**
2. **77. Combinations (Medium)**
3. **46. Permutations (Medium)**
4. **39. Combination Sum (Medium)**
5. **90. Subsets II (Medium)** – if time
6. **79. Word Search (Medium)** – if time

Approach:
- Spend at least ~15 minutes on each before peeking at hints.
- If you get stuck:
  - Write the backtracking template.
  - Identify state, base case, and choices.

### 4. End‑of‑Program Reflection (15–30 min)

You’ve now done 8 structured weeks. Take time to write:

1. **Pattern Inventory**  
   Across 8 weeks, list the major patterns you know now:
   - Arrays & Strings (two pointers, sliding window, prefix sums)
   - Hashing (`HashMap`, `HashSet`)
   - Linked lists (reverse, merge, fast/slow)
   - Stacks & Queues (parentheses, MinStack, monotonic stack)
   - Binary search (standard, boundaries, on answer)
   - Sorting + two pointers, interval merging
   - Trees (DFS/BFS)
   - Heaps / PriorityQueue (top‑K, merge K lists)
   - 1D & 2D DP
   - Backtracking (subsets, permutations, combinations, grid search)

2. **Self‑Assessment (1–5)**  
   Rate your comfort level with each pattern.

3. **Next Steps**  
   Based on your ratings:
   - Choose 2–3 weak areas to *intensively* practice over the next 2–3 weeks.
   - Plan: e.g., “2 tree problems, 2 DP problems, 2 backtracking problems per week.”

4. **Goal Setting**  
   - Decide a concrete next goal:
     - “Solve 100 LeetCode problems in the next 2 months.”
     - Or “Finish one company’s curated list (e.g., Blind 75).”

---

If you’d like, I can help you turn this into a **post‑bootcamp routine**: e.g., a 4‑week plan to solidify patterns by category (Tree/Graph week, DP week, etc.), plus a suggested list of representative LeetCode problems at each level.
