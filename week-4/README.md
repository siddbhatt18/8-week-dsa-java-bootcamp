**Week 4 Focus:**  
- Binary search patterns (classic + boundary search)  
- Binary search on “answer” / condition  
- Sorting & custom comparators  
- Two pointers on sorted arrays  
- Intro to monotonic stack via a classic problem  

Assume ~2–3 hours/day. Keep the habit: **think on paper first, then code, then reflect.**

---

## Day 1 – Binary Search Fundamentals

### 1. Concept Study: Binary Search Basics (30–40 min)

On paper:

1. **Core idea:**
   - Works on **sorted** (or monotonic) data.
   - Repeatedly halve the search space.
   - Typical components:
     - `int left = 0;`
     - `int right = n - 1;`
     - `while (left <= right)`:
       - `int mid = left + (right - left) / 2;`
       - Compare `nums[mid]` with target.
       - Adjust `left` or `right`.

2. **Pitfalls:**
   - Off‑by‑one errors (`<` vs `<=`).
   - Infinite loops if you don’t move pointers.
   - `mid` overflow if using `(left + right)/2` with large ints (use `left + (right - left) / 2`).

3. **Time complexity:** O(log n)  
   - Each step halves the range.

Write a generic template in your notebook.

### 2. Coding: Basic Binary Search (45–60 min)

Create `Week4Day1.java`:

1. **Implement: `int binarySearch(int[] nums, int target)`**
   - Return index if found, `-1` otherwise.
   - Use the **exact template** you wrote on paper.
   - Carefully handle:
     - `left <= right`
     - future bug: forgetting to update `left`/`right`.

2. **Test cases:**
   - `nums = [1,3,5,7,9], target = 7` → 3
   - Target at first index, last index, not present at all.
   - Empty array.

3. **Comment:**
   - Time and space complexity.
   - One line explaining why it’s O(log n).

### 3. LeetCode: Binary Search (Easy) (30–45 min)

- Solve LC **704. Binary Search**.
- Try first with your own implementation (copy from your file if needed).
- Ensure you pass all tests.

### 4. Reflection (10–15 min)

On paper:
- Explain in your own words:
  - Why binary search needs sorted data.
  - What changes if array is not sorted.

---

## Day 2 – Boundary Binary Search (First/Last Occurrence)

### 1. Quick Review (10–15 min)

Without looking:
- Sketch the binary search pseudo‑code.
- Explain in words: left, right, mid, and how they move.

### 2. Concept: Finding First or Last Occurrence (30–40 min)

On paper, clarify:

- Sometimes you need:
  - **First position** of target in a sorted array with duplicates.
  - **Last position** of target.

Pattern for **first** occurrence:
- Perform binary search, but when `nums[mid] == target`:
  - Record `mid` as a candidate answer.
  - Move `right = mid - 1` to keep searching **left side**.

Pattern for **last** occurrence:
- When `nums[mid] == target`:
  - Record `mid`.
  - Move `left = mid + 1` to keep searching **right side**.

### 3. Coding: First and Last Position (45–60 min)

In `Week4Day2.java`:

1. **Method: `int findFirst(int[] nums, int target)`**
   - Use binary search:
     - When `nums[mid] >= target`, move `right = mid - 1`.
     - When `nums[mid] < target`, move `left = mid + 1`.
   - After loop, check if `left` is within bounds and `nums[left] == target`; if so, `left`, else `-1`.
   - Alternatively, use a variable `ans = -1` and update when found.

2. **Method: `int findLast(int[] nums, int target)`**
   - Similar, but:
     - When `nums[mid] <= target`, move `left = mid + 1`.
     - When `nums[mid] > target`, move `right = mid - 1`.

3. **Combine:**
   - `int[] searchRange(int[] nums, int target)`  
     Return `{first, last}`.

### 4. LeetCode: Find First and Last Position of Element in Sorted Array (Medium) (30–45 min)

- LC **34. Find First and Last Position of Element in Sorted Array**.
- You already have the logic; adapt and submit.
- Double‑check edge cases:
  - Empty array.
  - Target not found.
  - All elements equal to target.

### 5. Reflection (10–15 min)

On paper:
- Describe the difference between:
  - “standard” binary search that returns any occurrence.
  - boundary search for first/last occurrence.

---

## Day 3 – Binary Search on Rotated Sorted Arrays (Logic Heavy)

### 1. Quick Review (10–15 min)

- Re‑state from memory:
  - How to find first occurrence with binary search in one paragraph.

### 2. Concept: Rotated Sorted Array (30–40 min)

On paper:

- Example of rotated sorted array:
  - Original sorted: `[1,2,3,4,5,6,7]`
  - Rotated: `[4,5,6,7,1,2,3]`

Goal:
- Search for target in O(log n).

Key observation:
- At any `mid`, **one half is always sorted**:
  - If `nums[left] <= nums[mid]`: left half is sorted.
  - Else: right half is sorted.

Within sorted half:
- Check if target lies within that half’s range.
- If yes, discard other half.
- If no, discard this half.

### 3. LeetCode: Search in Rotated Sorted Array (Medium) (60–75 min)

1. **Think on paper (20 min):**
   - Write the above logic as pseudo code.
   - Consider:
     ```java
     int left = 0, right = n - 1;
     while (left <= right) {
         int mid = left + (right - left) / 2;
         if (nums[mid] == target) return mid;

         if (nums[left] <= nums[mid]) {
             // left half sorted
             if (target >= nums[left] && target < nums[mid]) {
                 right = mid - 1;
             } else {
                 left = mid + 1;
             }
         } else {
             // right half sorted
             if (target > nums[mid] && target <= nums[right]) {
                 left = mid + 1;
             } else {
                 right = mid - 1;
             }
         }
     }
     return -1;
     ```

2. **Implement on LeetCode (LC 33).**
3. Test with multiple examples, including:
   - No rotation (normal sorted).
   - Target not present.

### 4. Optional: Find Minimum in Rotated Sorted Array (Medium, stretch) (20–30 min)

If you have time:

- LC **153. Find Minimum in Rotated Sorted Array**:
  - Find smallest element in O(log n).
  - Sketch idea:
    - If array is not rotated (`nums[left] < nums[right]`), min is `nums[left]`.
    - Otherwise, use binary search to find rotation point.

Even if you don’t code it fully, reason about it for practice.

### 5. Reflection (10–15 min)

Write:
- Why does the property “one half is sorted” hold in a rotated sorted array?
- How did you use that fact to limit your search?

---

## Day 4 – Binary Search on Answer (Search Space of Solutions)

### 1. Concept: Binary Search on Answer (30–40 min)

On paper:

- Sometimes you don’t binary search **in the array**, but over the **range of possible answers**.
- We need:
  - A monotonic boolean function `check(x)`:
    - As `x` increases, result goes from false→true or true→false.
  - Then, find the smallest `x` that makes `check(x)` true, or largest that makes it false, etc.

Common pattern:
```java
int left = minPossible, right = maxPossible;
while (left < right) {
    int mid = left + (right - left) / 2;
    if (check(mid)) {
        right = mid;      // mid could be answer, search left half
    } else {
        left = mid + 1;   // mid too small, go right
    }
}
return left; // or right
```

### 2. Example Problem (Custom): Minimum Capacity to Ship Packages (Think Only) (25–35 min)

Paraphrase a classic (similar to LC 1011):

- You have an array of package weights and days `D`.
- You must ship packages in order.
- Each day you can ship packages with total weight ≤ `capacity`.
- What is the **minimum capacity** required to ship them all within `D` days?

Think:

- Search space:
  - `left = max(weights)` (must at least carry the heaviest package).
  - `right = sum(weights)` (can carry all in one day at most).

- `check(capacity)`:
  - Simulate:
    - Start day 1, running sum.
    - Add packages until sum + weight[i] > capacity → new day.
    - Count days used; if `daysUsed <= D`, capacity is enough.

Even if you don’t code fully now, understand this pattern deeply.

### 3. LeetCode: First Bad Version (Easy) (30–45 min)

This is simpler but introduces **boundary search on condition**:
- LC **278. First Bad Version**.

You have `isBadVersion(version)` API and need the **first** bad version.

1. **Think:**
   - Version is like `[1,2,3,...,n]`, with pattern:  
     `F F F F T T T ... T`
   - Want smallest index where `isBadVersion` is true.
- Binary search on `1..n`:
  - If `isBadVersion(mid)` is true:
    - Move `right = mid` (mid might still be first bad).
  - Else:
    - Move `left = mid + 1`.

2. Implement using `while (left < right)` pattern.

### 4. (Optional) Start: Koko Eating Bananas (Medium, challenging) (20–30 min)

If you have time:

- LC **875. Koko Eating Bananas**.
- Very similar to “search on answer”:
  - Search Koko’s eating speed.
- Even if you don’t solve completely, read the description and try to outline:
  - Possible `left` and `right`.
  - `check(speed)` function.

### 5. Reflection (10–15 min)

Write:
- What is the key difference between “binary search in array” and “binary search on answer”?
- Why is a monotonic condition essential?

---

## Day 5 – Sorting Basics + Two Pointers & Intervals

### 1. Concept: Sorting in Java (20–30 min)

On paper:

- `Arrays.sort(int[])` → sorts in ascending order, O(n log n).
- Sorting objects or arrays of objects:
  ```java
  Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
  ```
- `Collections.sort(list)` for lists.

Think:
- Sorting often simplifies problems:
  - Group anagrams.
  - Merge intervals.
  - Two pointers on sorted arrays for sums.

### 2. Coding: Sorting and Two Pointers Refresher (30–40 min)

In `Week4Day5.java`:

1. **Sort and Two Sum with Sorting**
   - Method: `boolean hasPairWithSumSorted(int[] nums, int target)`
   - Steps:
     - `Arrays.sort(nums)`;
     - Two pointers:
       ```java
       int left = 0, right = nums.length - 1;
       while (left < right) {
           int sum = nums[left] + nums[right];
           if (sum == target) return true;
           else if (sum < target) left++;
           else right--;
       }
       return false;
       ```

2. Comment on the complexity: O(n log n).

### 3. Concept: Intervals & Merge Pattern (25–35 min)

On paper:

- Given intervals like `[[1,3],[2,6],[8,10],[15,18]]`, want to merge overlapping ones.
- Approach:
  1. Sort intervals by start time.
  2. Keep a `current` interval.
  3. For each interval:
     - If `interval.start` <= `current.end`, they overlap → merge by updating `current.end = max(current.end, interval.end)`.
     - Else, add `current` to result, and set `current = interval`.

Draw a simple example and walk through step‑by‑step.

### 4. LeetCode: Merge Intervals (Medium) (45–60 min)

- LC **56. Merge Intervals**.

1. **Think First:**
   - Convert the above concept into steps.
2. **Implement:**
   - Remember to handle corner cases: 0 or 1 interval.
   - Use `Arrays.sort(intervals, (a,b) -> Integer.compare(a[0], b[0]));`
3. Complexity: O(n log n) due to sorting.

### 5. Reflection (10–15 min)

Write:
- How did sorting make merging intervals easier?
- Could you do it in O(n²) without sorting? Why is that worse?

---

## Day 6 – Monotonic Stack Introduction (Daily Temperatures)

### 1. Concept: Monotonic Stack (30–40 min)

On paper:

- Monotonic stack: a stack that is always **increasing** or **decreasing** by some criterion (e.g., values or indices).

Classic use:
- **Next greater element**:
  - While current value is greater than stack’s top value:
    - Pop from stack.
    - The current index is the “next greater” for that popped index.

Key pattern:
- Stack holds **indices**, not values.
- The stack is maintained in a way (e.g., decreasing values stack) so that when a larger value appears, you solve for multiple previous indices.

### 2. Problem Setup: Daily Temperatures (Thinking) (20–30 min)

LC **739. Daily Temperatures** (Medium):

- Given temperatures `T[i]`, find for each day how many days until a warmer temperature.
- If none, answer is 0.

On paper:

- Brute force: for each day, scan future days → O(n²).
- Monotonic stack idea:
  - Keep a stack of **indices** with temperatures in a **decreasing** order.
  - As you go from left to right:
    - For current index `i`:
      - While stack not empty and `T[i] > T[stack.peek()]`:
        - `prevIndex = stack.pop()`
        - Answer for `prevIndex` = `i - prevIndex`
      - Push `i` onto stack.

### 3. Implement: Daily Temperatures (60–75 min)

In `Week4Day6.java`:

1. Implement method:
   ```java
   int[] dailyTemperatures(int[] T)
   ```
2. Follow the algorithm you wrote.
3. Test with:
   - `T = [73,74,75,71,69,72,76,73]`  
     Expected: `[1,1,4,2,1,1,0,0]`.

### 4. Reflection (10–15 min)

Write:
- In your own words, what is a monotonic stack?
- Why does it help avoid O(n²) for this problem?

If you have time, consider:
- Where else might you want “next greater element” or “next smaller element”?

---

## Day 7 – Consolidation: Binary Search + Sorting + Monotonic Stack

### 1. Concept Review (30–40 min)

Without looking at previous notes, on paper:

- Write definitions for:
  - Binary search (standard).
  - Boundary search (first/last).
  - Binary search on answer (and what `check(x)` is).
  - Sorting + how it enables two pointers & interval merging.
  - Monotonic stack.

- For each, give **one example problem** where you’d use it.

Then open your notes and correct/fill any gaps.

### 2. Re‑implement from Memory (60–75 min)

In `Week4Review.java`, re‑implement:

1. `int binarySearch(int[] nums, int target)`
2. `int[] searchRange(int[] nums, int target)` (first & last)
3. `int searchInRotatedSortedArray(int[] nums, int target)` (or just `search`)
4. `void mergeIntervals(int[][] intervals)` (or return merged list)
5. `int[] dailyTemperatures(int[] T)`

For each:
- Add comments:
  - Time complexity.
  - Space complexity.
  - 1–2 line intuition.

### 3. LeetCode Mini‑Session (60–75 min)

On LeetCode, solve or re‑solve:

1. **704. Binary Search (Easy)**  
2. **34. Find First and Last Position of Element in Sorted Array (Medium)**  
3. **33. Search in Rotated Sorted Array (Medium)**  
4. **56. Merge Intervals (Medium)**  
5. **739. Daily Temperatures (Medium)** – if time.

Approach:
- Start each from a blank editor.
- Spend at least 10–15 minutes reasoning if stuck before peeking at hints.

### 4. End‑of‑Week Reflection (15–20 min)

In your notebook:

1. **Pattern Cheat Sheet (update from previous weeks):**
   - Arrays + hash set/map
   - Sliding window
   - Linked list pointer tricks
   - Stack (parentheses, MinStack, monotonic stack)
   - Binary search (standard + rotated + answer)
   - Sorting (two pointers, interval merging)

2. **Comfort Ratings (1–5):**
   - Binary search basics
   - Binary search on rotated arrays
   - Binary search on answer (even conceptual)
   - Sorting + two pointers
   - Monotonic stack

3. **Questions for Next Week:**
   - e.g., “When should I think about DP vs binary search?”  
   - “How can I better detect when monotonic stack is useful?”  
   - “What’s the best way to debug binary search bugs?”

You’ll use these to start Week 5 (trees + BFS/DFS) more focused and aware of your current strengths and weaknesses.

---

If you’d like, I can next build **Week 5 (Trees & basic graph traversals)** into the same daily structure so you keep progressing with clear steps.
