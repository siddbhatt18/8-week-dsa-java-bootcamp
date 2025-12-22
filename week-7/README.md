**Week 7 Focus:**  
- Core dynamic programming (DP) mindset  
- 1D DP (climbing stairs, house robber, coin change)  
- Simple 2D/grid DP (unique paths, min path sum)  
- Learn to recognize “overlapping subproblems” and “optimal substructure”  

Assume ~2–3 hours/day. As before: think on paper → code → reflect.

---

## Day 1 – DP Mindset + Climbing Stairs

### 1. Concept: What Is Dynamic Programming? (30–40 min)

On paper, in your own words:

- DP is about:
  - **Overlapping subproblems:** the same smaller problems are solved repeatedly.
  - **Optimal substructure:** optimal solution to a problem can be built from optimal solutions of its subproblems.

Typical workflows:
1. Start with **a recursive definition** (top‑down).
2. Notice repeated work.
3. Convert to a **memoized recursion** or **bottom‑up table**.

Key questions to ask for any DP problem:
- What is the **state**? (`dp[i]` or `dp[i][j]` … what does it mean?)
- What are the **transitions**? (how to compute `dp[i]` from previous states)
- What are the **base cases**?
- What is the **answer**? (`dp[n-1]`? max over dp? dp[m][n]? etc.)

Write this “checklist” in your notebook.

### 2. Intro Example: Climbing Stairs (Discussion) (20–30 min)

LeetCode **70. Climbing Stairs (Easy)**.

Paraphrase problem:
- You can climb 1 or 2 steps at a time.
- In how many distinct ways can you reach step `n`?

On paper:

- Let `dp[i]` = number of ways to reach step `i`.
- Base cases:
  - `dp[0] = 1` (1 way to stay at ground).
  - `dp[1] = 1` (only 1 step).
- Transition:
  - To get to step `i`, you either:
    - come from `i-1` (1 step) or
    - come from `i-2` (2 steps).
  - So: `dp[i] = dp[i-1] + dp[i-2]`.

Time complexity: O(n), space O(n) or O(1) if you just keep last two.

### 3. Coding: Climbing Stairs (45–60 min)

In `Week7Day1.java`:

1. Implement:

   ```java
   int climbStairs(int n) {
       if (n <= 2) return n;
       int[] dp = new int[n + 1];
       dp[0] = 1;
       dp[1] = 1;
       for (int i = 2; i <= n; i++) {
           dp[i] = dp[i - 1] + dp[i - 2];
       }
       return dp[n];
   }
   ```

2. Then implement a **space-optimized** version using just two variables:

   ```java
   int climbStairsOptimized(int n) {
       if (n <= 2) return n;
       int prev2 = 1; // dp[0]
       int prev1 = 1; // dp[1]
       for (int i = 2; i <= n; i++) {
           int curr = prev1 + prev2;
           prev2 = prev1;
           prev1 = curr;
       }
       return prev1;
   }
   ```

3. Test with small `n` values: 1–7, and compare.

### 4. LeetCode: Climbing Stairs (Easy) (20–30 min)

- Solve LC **70. Climbing Stairs** using your DP solution.

### 5. Reflection (10–15 min)

On paper:
- Write your **state definition** and **transition** for climbing stairs in your own words.
- How can you tell this is DP and not just simple math?

---

## Day 2 – House Robber (Classic 1D DP)

### 1. Quick Review (10–15 min)

From memory (no code):

- Write the recurrence for Climbing Stairs:
  - `dp[i] = ?`
- Mention base cases.

### 2. Concept: House Robber (30–40 min)

LeetCode **198. House Robber (Medium)**.

Paraphrase:
- You have `nums[]`, each element is money at a house.
- If you rob a house, you **cannot** rob its immediate neighbors.
- Maximize total amount.

On paper:

- Let `dp[i]` = max money you can rob from first `i` houses (`0..i-1`) or from index `i` onward (pick one convention and stick with it).

Common convention:
- `dp[i]` = max money you can rob **up to index i** (0‑based).

Then:
- For house `i`, you have two choices:
  - **Skip** it → `dp[i] = dp[i-1]`
  - **Rob** it → `dp[i] = nums[i] + (i >= 2 ? dp[i-2] : 0)`

Thus:
- `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`.

Base cases:
- `dp[0] = nums[0]`
- `dp[1] = max(nums[0], nums[1])` (if `n >= 2`)

### 3. Coding: House Robber (45–60 min)

In `Week7Day2.java`:

1. Implement:

   ```java
   int rob(int[] nums) {
       int n = nums.length;
       if (n == 0) return 0;
       if (n == 1) return nums[0];
       int[] dp = new int[n];
       dp[0] = nums[0];
       dp[1] = Math.max(nums[0], nums[1]);
       for (int i = 2; i < n; i++) {
           dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
       }
       return dp[n - 1];
   }
   ```

2. Try a **space-optimized** version using only two variables (similar to Climbing Stairs).

### 4. LeetCode: House Robber (Medium) (20–30 min)

- Solve LC **198. House Robber**.
- Then read discussion/solutions and match to your recurrence.

### 5. Compare Problems (10–15 min)

On paper:
- What are the similarities between Climbing Stairs and House Robber?
  - Both 1D DP.
  - Both use `dp[i]` depending on `dp[i-1]` and `dp[i-2]`.
- What’s different (interpretation of `dp[i]`)?

---

## Day 3 – Coin Change (Unbounded 1D DP)

### 1. Quick Review (10–15 min)

- Briefly re‑write `dp[i]` recurrence for House Robber (high-level).
- Note the idea of “choose to take or skip current index.”

### 2. Concept: Coin Change – Minimum Coins (40–50 min)

LeetCode **322. Coin Change (Medium)**.

Paraphrase problem:
- Coins of given denominations.
- Infinite number of each coin.
- Want **minimum number of coins** to make up `amount`. If impossible, return -1.

On paper:

- Let `dp[x]` = minimum coins needed to make up amount `x`.
- Base:
  - `dp[0] = 0` (0 coins to make sum 0)
  - `dp[x] = INF` initially for x > 0.

Transition:
- For each amount `x` from 1 to `amount`:
  - For each coin `c`:
    - If `x - c >= 0` and `dp[x - c]` is not INF:
      - `dp[x] = min(dp[x], dp[x - c] + 1)`

Time complexity: O(amount * number_of_coins).

### 3. Coding: Coin Change (60–75 min)

In `Week7Day3.java`:

1. Implement:

   ```java
   int coinChange(int[] coins, int amount) {
       int max = amount + 1; // sentinel for impossible
       int[] dp = new int[amount + 1];
       Arrays.fill(dp, max);
       dp[0] = 0;

       for (int x = 1; x <= amount; x++) {
           for (int coin : coins) {
               if (x - coin >= 0) {
                   dp[x] = Math.min(dp[x], dp[x - coin] + 1);
               }
           }
       }

       return dp[amount] > amount ? -1 : dp[amount];
   }
   ```

2. Test with:
   - `coins = [1,2,5], amount = 11` → 3 (5+5+1)
   - `coins = [2], amount = 3` → -1

3. Then solve LC **322. Coin Change** with same logic.

### 4. Reflection (10–15 min)

Write:
- What does `dp[x]` represent here?
- Why is it important to initialize `dp[x]` with a large value (INF)?

Optional thought:
- How is this different from a greedy solution (always take largest coin) that might fail?

---

## Day 4 – 2D DP: Unique Paths

### 1. Quick Review (10–15 min)

From memory or quickly scanning:

- State & transition of `coinChange`.
- General 1D DP pattern: loop over state (i) and consider transitions from previous states.

### 2. Concept: Unique Paths (30–40 min)

LeetCode **62. Unique Paths (Medium)**.

Paraphrase:
- A robot moves **only right or down** in an `m x n` grid, starting at top-left, ending at bottom-right.
- How many unique paths are there?

On paper:

- Let `dp[r][c]` = number of ways to reach cell `(r, c)` from start.
- Base cases:
  - First row: can only move right, so `dp[0][c] = 1` for all c.
  - First column: can only move down, so `dp[r][0] = 1` for all r.
- Transition:
  - For general cell (r > 0 and c > 0):
    - `dp[r][c] = dp[r-1][c] + dp[r][c-1]`.

Answer:
- `dp[m-1][n-1]`

### 3. Coding: Unique Paths (45–60 min)

In `Week7Day4.java`:

1. Implement:

   ```java
   int uniquePaths(int m, int n) {
       int[][] dp = new int[m][n];
       for (int r = 0; r < m; r++) {
           dp[r][0] = 1;
       }
       for (int c = 0; c < n; c++) {
           dp[0][c] = 1;
       }
       for (int r = 1; r < m; r++) {
           for (int c = 1; c < n; c++) {
               dp[r][c] = dp[r - 1][c] + dp[r][c - 1];
           }
       }
       return dp[m - 1][n - 1];
   }
   ```

2. Solve LC **62. Unique Paths** using this.

### 4. Variant: Unique Paths with Obstacles (Thinking) (20–30 min)

LeetCode **63. Unique Paths II (Medium)**.

- There is a grid with 1 as obstacle, 0 as free cell.
- You can’t go through obstacles.

On paper only for now (or code if you have time):

- Modify `dp[r][c]` logic:
  - If cell is obstacle → `dp[r][c] = 0`.
  - Else:
    - If first row/column: handle carefully (if an obstacle appears, all cells after it in that row/col are unreachable).
    - Else: `dp[r][c] = dp[r-1][c] + dp[r][c-1]`.

### 5. Reflection (10–15 min)

Write:
- Compare 1D vs 2D DP:
  - How do states and transitions differ?
- Why is thinking in terms of “ways to reach here” more natural than “ways to go from here”?

---

## Day 5 – 2D DP: Minimum Path Sum

### 1. Quick Review (10–15 min)

- Re‑explain `uniquePaths` in words:
  - What `dp[r][c]` means.
  - Where base cases are.
  - Recurrence relation.

### 2. Concept: Minimum Path Sum (30–40 min)

LeetCode **64. Minimum Path Sum (Medium)**.

Paraphrase:
- Grid of non-negative numbers.
- Move only right and down.
- Find a path from top-left to bottom-right with minimum sum of values along the path.

On paper:

- Let `dp[r][c]` = **minimum path sum** to reach `(r, c)` from `(0,0)`.

Base:
- `dp[0][0] = grid[0][0]`
- First row: can only come from left:
  - `dp[0][c] = dp[0][c-1] + grid[0][c]`
- First column: can only come from top:
  - `dp[r][0] = dp[r-1][0] + grid[r][0]`

Transition:
- `dp[r][c] = grid[r][c] + min(dp[r-1][c], dp[r][c-1])`

Answer:
- `dp[m-1][n-1]`.

### 3. Coding: Minimum Path Sum (45–60 min)

In `Week7Day5.java`:

1. Implement:

   ```java
   int minPathSum(int[][] grid) {
       int m = grid.length, n = grid[0].length;
       int[][] dp = new int[m][n];
       dp[0][0] = grid[0][0];

       for (int c = 1; c < n; c++) {
           dp[0][c] = dp[0][c - 1] + grid[0][c];
       }
       for (int r = 1; r < m; r++) {
           dp[r][0] = dp[r - 1][0] + grid[r][0];
       }
       for (int r = 1; r < m; r++) {
           for (int c = 1; c < n; c++) {
               dp[r][c] = grid[r][c] + Math.min(dp[r - 1][c], dp[r][c - 1]);
           }
       }
       return dp[m - 1][n - 1];
   }
   ```

2. Then solve LC **64. Minimum Path Sum**.

### 4. Optional: Space Optimization on 2D DP (15–20 min)

Think on paper:

- Notice that to compute row `r`, you only need row `r` and row `r-1`.
- So you can use a 1D array `dp[c]` that you update row by row.
- Don’t rush to implement if confusing; it’s a nice stretch goal.

### 5. Reflection (10–15 min)

Write:
- How are `uniquePaths` and `minPathSum` similar?
- What changed when the problem switched from “count paths” to “minimize sum”?

---

## Day 6 – Longest Increasing Subsequence (O(n²) DP)

### 1. Quick Review (10–15 min)

- Summarize the main differences between:
  - Counting‑based DP (e.g., Climbing Stairs, Unique Paths).
  - Min‑cost DP (e.g., Coin Change, Minimum Path Sum).

### 2. Concept: Longest Increasing Subsequence (LIS) – DP Version (40–50 min)

LeetCode **300. Longest Increasing Subsequence (Medium)**.

Paraphrase:
- Given an unsorted array, find the length of the longest strictly increasing subsequence (not necessarily contiguous).

On paper:

- Classic O(n²) DP:

Let `dp[i]` = length of LIS **ending at index i**.

Then:
- Initialize `dp[i] = 1` for all i.
- For each `i` from 0 to n-1:
  - For each `j` from 0 to i-1:
    - If `nums[j] < nums[i]`, you can extend LIS ending at j:
      - `dp[i] = max(dp[i], dp[j] + 1)`
- Answer is `max(dp[i])` over all i.

### 3. Coding: LIS O(n²) DP (45–60 min)

In `Week7Day6.java`:

1. Implement:

   ```java
   int lengthOfLIS(int[] nums) {
       int n = nums.length;
       if (n == 0) return 0;
       int[] dp = new int[n];
       Arrays.fill(dp, 1);
       int ans = 1;
       for (int i = 0; i < n; i++) {
           for (int j = 0; j < i; j++) {
               if (nums[j] < nums[i]) {
                   dp[i] = Math.max(dp[i], dp[j] + 1);
               }
           }
           ans = Math.max(ans, dp[i]);
       }
       return ans;
   }
   ```

2. Test with:
   - `[10,9,2,5,3,7,101,18]` → 4 (2,3,7,101 or 2,5,7,101)
   - `[0,1,0,3,2,3]` → 4

3. Then solve LC **300. Longest Increasing Subsequence** using same approach.

Optional:
- Be aware there is an O(n log n) solution using binary search, but for now focus on DP intuition.

### 4. Reflection (10–15 min)

Write:
- What does `dp[i]` represent exactly?
- Why do we need a nested loop (O(n²)) here, unlike some earlier 1D DPs?

---

## Day 7 – Consolidation: 1D & 2D DP

### 1. Concept Review (30–40 min)

Without looking at previous code, on paper:

For each of these problems, write:

1. What your **dp state** is (what `dp[...]` means).
2. The **recurrence/transition**.
3. The **base cases**.
4. Where the **final answer** is read from.

Do this for:

- Climbing Stairs (70)
- House Robber (198)
- Coin Change (322)
- Unique Paths (62)
- Minimum Path Sum (64)
- Longest Increasing Subsequence (300)

Then compare with your notes and fix any inaccuracies.

### 2. Re‑implement from Memory (60–75 min)

In `Week7Review.java`, re‑implement:

1. `int climbStairs(int n)`
2. `int rob(int[] nums)`
3. `int coinChange(int[] coins, int amount)`
4. `int uniquePaths(int m, int n)`
5. `int minPathSum(int[][] grid)`
6. `int lengthOfLIS(int[] nums)`

For each:
- Add a comment block above:

  ```java
  // State: dp[i] = ...
  // Transition: ...
  // Base: ...
  // Answer: ...
  ```

- Add time and space complexity as comments.

### 3. LeetCode Mini‑Session (60–75 min)

On LeetCode, solve or re‑solve (from scratch):

1. **70. Climbing Stairs (Easy)**  
2. **198. House Robber (Medium)**  
3. **322. Coin Change (Medium)**  
4. **62. Unique Paths (Medium)**  
5. **64. Minimum Path Sum (Medium)**  
6. (If time) **300. Longest Increasing Subsequence (Medium)**  

Give each at least 15 minutes before peeking at any hints.

### 4. End‑of‑Week Reflection (15–20 min)

In your notebook:

1. **DP Pattern Summary**
   - 1D DP:
     - “dp[i] is optimal result up to i or for amount i.”
   - 2D DP:
     - “dp[r][c] is optimal result to reach cell (r,c).”
   - Multi-choice transitions:
     - “dp[x] = min/max/combine over possible previous states.”

2. **Comfort Ratings (1–5):**
   - Identifying when a problem is DP.
   - Designing states and transitions.
   - Implementing 1D vs 2D DP.
   - Explaining your DP logic to someone else.

3. **Questions to Guide Next Steps:**
   - e.g., “How to approach more complex DP like knapsack, edit distance, or palindromic subsequences?”
   - “How to spot DP when it is hidden beneath recursion/backtracking?”

---

If you’d like, I can next build a Week 8 day‑by‑day plan around **backtracking (subsets, permutations, combinations)** and some mixed/harder LeetCode problems that combine patterns you’ve learned.
