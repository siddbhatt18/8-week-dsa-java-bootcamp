Here’s your **Week 7 – Day 1 to Day 7 plan**, focused on **Dynamic Programming (DP)**:

- Recognize when DP applies (overlapping subproblems, optimal substructure)
- Start with simple 1D DP → move to 2D (grids, subsequences)
- Practice core LeetCode DP problems

Aim for ~1.5–2 hours/day. Keep the pattern: concept → small implementations → LeetCode → brief reflection.

---

## Week 7 Focus

- DP fundamentals:
  - Top‑down (recursion + memoization)
  - Bottom‑up (tabulation)
- 1D DP:
  - Climbing stairs
  - House Robber
  - Simple linear recurrences
- 2D DP:
  - Grid paths
  - Longest Common Subsequence (LCS)
- Intro to sequence DP:
  - Longest Increasing Subsequence (LIS)
  - Simple string DP

---

## Day 1 – What Is DP? Climbing Stairs

**Goal:** Understand the core idea of DP and solve your first classic DP problem.

### 1. Concept: When to Use DP (30–40 min)

In your notes:

- DP fits when:
  - You can break problem into **subproblems**.
  - Subproblems **reuse** results (overlapping).
  - There is an **optimal substructure** (best solution built from best solutions of subproblems).

Contrast three styles with a simple example:

- Plain recursion (exponential).
- Recursion + memo (top‑down DP).
- Iterative array (bottom‑up DP).

Explain classical Fibonacci:

```java
// naive recursion: exponential
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```

Memoized version:

```java
int fibMemo(int n, int[] memo) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];
    memo[n] = fibMemo(n-1, memo) + fibMemo(n-2, memo);
    return memo[n];
}
```

Bottom‑up:

```java
int fibBottomUp(int n) {
    if (n <= 1) return n;
    int[] dp = new int[n+1];
    dp[0] = 0; dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n];
}
```

### 2. LeetCode – Climbing Stairs (`#70`, Easy) (45–60 min)

Think first:

- You can climb 1 or 2 steps.
- Let `dp[i]` = number of ways to reach step `i`.
- Recurrence:
  - `dp[i] = dp[i-1] + dp[i-2]`
- Base:
  - `dp[0] = 1` (1 way to stand at ground)
  - `dp[1] = 1`

Implement:

1. Bottom‑up `dp[]` array.
2. Optimize to O(1) space using two variables (`prev1`, `prev2`).

### 3. Optional: Practice with Fibonacci (20–30 min)

- Write a bottom‑up Fibonacci.
- Then re‑express climbing stairs as “like Fibonacci”.

**Reflection (10–15 min)**  
Answer briefly:

- What is the **state** in `Climbing Stairs`?
- What is the **transition/recurrence**?
- Which feels clearer to you now: top‑down with memo or bottom‑up?

---

## Day 2 – 1D DP: House Robber & Variants

**Goal:** Get comfortable with 1D DP on arrays (choose/skip decisions).

### 1. Concept: “Take or Skip” DP (25–30 min)

Pattern:

- You’re at index `i`.
- You can either:
  - Take current item and skip some next index.
  - Or skip current item.
- `dp[i]` = best value considering prefix up to index `i`.

### 2. LeetCode – House Robber (`#198`, Medium) (45–60 min)

Problem:

- `nums[i]` = money.
- Cannot rob adjacent houses.
- `dp[i]` = max money up to index `i`.

Recurrence:

```java
dp[0] = nums[0];
dp[1] = max(nums[0], nums[1]);
dp[i] = max(dp[i-1], dp[i-2] + nums[i]);
```

Steps:

1. First write bottom‑up with `dp[]`.
2. Then compress to two variables.

### 3. Optional: House Robber II (`#213`, Medium) (45–60 min)

- Houses in a **circle**.
- either rob from 0..n-2 or 1..n-1 (two linear subproblems).
- Use your `robLinear(int[] nums, int start, int end)` helper.

If this feels too much, skip and just re‑solve `#70`.

**Reflection (10–15 min)**  
- Identify `dp` definition and recurrence in your own words.
- Notice similarity to Climbing Stairs: local relation to previous states.

---

## Day 3 – 1D DP: Longest Increasing Subsequence (LIS)

**Goal:** Learn a slightly more complex 1D DP over array indices.

### 1. Concept: DP over “ending at i” (20–30 min)

For LIS:

- Let `dp[i]` = length of **longest increasing subsequence ending at index i**.
- Then:

```java
dp[i] = 1 + max(dp[j]) for all j < i where nums[j] < nums[i]
if no such j, dp[i] = 1
answer = max(dp[i]) over all i
```

### 2. LeetCode – Longest Increasing Subsequence (`#300`, Medium) (60–75 min)

Implement O(n²) DP:

```java
int lengthOfLIS(int[] nums) {
    int n = nums.length;
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

Don’t worry about the O(n log n) optimized version yet; focus on understanding the DP.

### 3. Optional: Practice Another “ending at i” DP (30–45 min)

If you have time, read/think about:

- **Maximum Subarray** (`#53`, Easy/Medium, Kadane’s algorithm)
  - `dp[i]` = max subarray sum **ending at i**.

Try implementing:

```java
int maxSubArray(int[] nums) {
    int current = nums[0];
    int best = nums[0];
    for (int i = 1; i < nums.length; i++) {
        current = Math.max(nums[i], current + nums[i]);
        best = Math.max(best, current);
    }
    return best;
}
```

**Reflection (10–15 min)**  
- For LIS: why define `dp[i]` as “ending at i” instead of something else?
- What’s the pattern like: nested loops where `j < i` influences `dp[i]`.

---

## Day 4 – 2D DP on Grids: Unique Paths & Min Path Sum

**Goal:** Move from 1D to 2D DP with grid problems.

### 1. Concept: Grid DP (30–40 min)

Typical setup:

- `dp[r][c]` stores some best/number-of-ways for cell `(r,c)`.
- Transitions usually from top and left neighbors:
  - `dp[r][c] = dp[r-1][c] + dp[r][c-1]` or variations.
- Need base cases for first row/column.

### 2. LeetCode – Unique Paths (`#62`, Medium) (45–60 min)

Robot from top‑left to bottom‑right, only moves right/down.

- Let `dp[r][c]` = number of ways to reach `(r,c)`.
- Base:
  - First row and first column all 1 (only one way along edge).
- Transition:
  - `dp[r][c] = dp[r-1][c] + dp[r][c-1]`.

Implement bottom‑up `dp[rows][cols]`.

### 3. LeetCode – Minimum Path Sum (`#64`, Medium) (45–60 min)

Similar to `#62`, but minimize cost:

- `grid[r][c]` = cost of cell.
- `dp[r][c]` = min path sum to reach `(r,c)`.

Recurrence:

```java
dp[0][0] = grid[0][0];
dp[r][c] = grid[r][c] + min(dp[r-1][c], dp[r][c-1]);
```

Handle first row/column separately.

**Reflection (10–15 min)**  
- Compare `#62` and `#64`: same structure, “+” vs “min +”.
- Clearly identify state `dp[r][c]` and transition.

---

## Day 5 – 2D DP on Strings: Longest Common Subsequence (LCS)

**Goal:** Learn DP on two strings (2D DP), a very common pattern.

### 1. Concept: DP over Two Strings (30–40 min)

For LCS between `text1` and `text2`:

- Let `dp[i][j]` = length of LCS of:
  - `text1[0..i-1]` (first i chars)
  - `text2[0..j-1]` (first j chars)

Recurrence:

- If `text1[i-1] == text2[j-1]`:

  ```java
  dp[i][j] = dp[i-1][j-1] + 1;
  ```

- Else:

  ```java
  dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
  ```

Initialize `dp[0][*] = 0`, `dp[*][0] = 0`.

### 2. LeetCode – Longest Common Subsequence (`#1143`, Medium) (60–75 min)

Implement exactly as above:

```java
int longestCommonSubsequence(String text1, String text2) {
    int m = text1.length(), n = text2.length();
    int[][] dp = new int[m+1][n+1];
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1.charAt(i-1) == text2.charAt(j-1)) {
                dp[i][j] = dp[i-1][j-1] + 1;
            } else {
                dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
            }
        }
    }
    return dp[m][n];
}
```

### 3. Optional: Read/Edit Another String DP (30–45 min)

If you can, at least **read and understand** another string DP:

- **Edit Distance** (`#72`, Hard – just high-level reading is fine), or
- A simpler one: **Distinct Subsequences** (`#115`, Hard, reading only).

Don’t worry about fully solving; just see similar `dp[i][j]` patterns.

**Reflection (10–15 min)**  
- What do `i` and `j` represent in LCS?
- How is DP table fill order chosen (why `i` from 1..m, `j` from 1..n)?

---

## Day 6 – Coin Change & Mixed DP Review

**Goal:** Solidify DP skills with a classic “unbounded knapsack”-style problem and review.

### 1. Concept: Coin Change as DP on Amount (25–30 min)

For **Coin Change**:

- Given coins and amount.
- Let `dp[amount]` = minimum coins to make that amount (or impossible).

Recurrence:

```java
dp[0] = 0;
for a from 1..amount:
    dp[a] = INF initially
    for each coin c:
        if a - c >= 0 and dp[a-c] not INF:
            dp[a] = min(dp[a], dp[a-c] + 1)
```

Answer is `dp[amount]` or -1 if INF.

### 2. LeetCode – Coin Change (`#322`, Medium) (60–75 min)

Implement bottom‑up:

```java
int coinChange(int[] coins, int amount) {
    int max = amount + 1;
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, max);
    dp[0] = 0;
    for (int a = 1; a <= amount; a++) {
        for (int c : coins) {
            if (a - c >= 0) {
                dp[a] = Math.min(dp[a], dp[a - c] + 1);
            }
        }
    }
    return dp[amount] > amount ? -1 : dp[amount];
}
```

### 3. Quick Review Problems (45–60 min)

Re‑solve 2–3 of these (pick ones you found tricky):

- `#70 Climbing Stairs`
- `#198 House Robber`
- `#62 Unique Paths`
- `#64 Minimum Path Sum`
- `#300 Longest Increasing Subsequence`

Try to do each in **≤25 minutes**.

**Reflection (10–15 min)**  
- For Coin Change, clearly state:
  - `dp[a]` meaning.
  - Transition formula.
- Compare it to `Climbing Stairs` and `House Robber` patterns.

---

## Day 7 – DP Pattern Review & Timed Practice

**Goal:** Connect DP patterns across problems and practice under time constraints.

### 1. Pattern Summary (30–40 min)

In your notebook, for each category, write 2–3 lines:

1. **Linear 1D DP**
   - Examples: `#70`, `#198`, `#53`, `#300`, `#322`
   - Typical form: `dp[i]` depends on some earlier `dp[j]` (j ≤ i).

2. **2D Grid DP**
   - Examples: `#62`, `#64`
   - `dp[r][c]` from neighbors, base row/col.

3. **2D String DP**
   - Example: `#1143`
   - `dp[i][j]` from `dp[i-1][j-1]`, `dp[i-1][j]`, `dp[i][j-1]`.

For each, write:

- Definition of state.
- Typical transition shape.

### 2. Timed Mixed DP Set (60–90 min)

Pick 4–5 DP problems across categories. Suggested set:

- `#70 Climbing Stairs`
- `#198 House Robber`
- `#62 Unique Paths`
- `#64 Minimum Path Sum`
- `#300 Longest Increasing Subsequence`
- `#322 Coin Change`
- `#1143 Longest Common Subsequence`

For each:

1. Spend 5–7 minutes thinking on paper:
   - Define `dp` state explicitly.
   - Write the recurrence.
2. Then code and test.

Aim for:

- Easies: ≤20 minutes.
- Mediums: ≤30 minutes.

### 3. Optional Stretch (30–45 min)

If you’re up for a challenge, attempt or at least **carefully read**:

- **House Robber II** (`#213`) – apply your `House Robber` logic twice.
- Or another sequence DP you haven’t tried yet:
  - **Delete and Earn** (`#740`, Medium)
  - **Longest Palindromic Subsequence** (`#516`, Medium – 2D DP over one string).

Even if you don’t finish, focus on:

- How `dp` is defined.
- Relationship to problems you already know.

**Reflection (10–15 min)**  
- Which DP pattern feels most natural to you now?
- Which specific problem felt hardest this week, and why?  
  Write its `dp` definition and recurrence one more time cleanly.

---

## How Week 7 Fits the Bigger Picture

By the end of Week 7, you should:

- Recognize when a problem is a good fit for DP.
- Be able to define **states** and **recurrences** for:
  - 1D linear DP (climbing stairs, robber, LIS, coin change).
  - 2D grid DP (paths, minimal sums).
  - 2D string DP (LCS).
- Convert recursive ideas into bottom‑up implementations in Java.

Week 8 will then focus on:

- Integrating everything: arrays, hashes, two pointers, trees, graphs, backtracking, DP.
- Pattern recognition and timed LeetCode sessions to simulate interview conditions.

If you’d like, I can next create a **Week 8 – consolidation & mock‑interview week** daily plan.
