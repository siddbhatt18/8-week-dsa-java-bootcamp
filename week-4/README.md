Here’s your **Week 4 – Day 1 to Day 7 plan**, focused on:

- Sorting (concepts + when to use it)
- Binary Search (on arrays and on “answer space”)
- Classic LeetCode problems that use these patterns

Target: ~1.5–2 hours/day. Keep the structure: concept → implement → LeetCode → reflect.

---

## Week 4 Focus

- Sorting:
  - Big-picture understanding of O(n log n) sorts
  - When/why to sort before applying two pointers or greedy logic
- Binary Search:
  - Standard binary search
  - Boundary variants (first/last position)
  - Binary search on answer (min/max feasible value)
- Core problems you’ll keep seeing in interviews

---

## Day 1 – Sorting Fundamentals & Practice

**Goal:** Understand sorting basics, Java’s sort APIs, and when sorting helps.

### 1. Concept: Sorting & Complexity (30–40 min)

Review:

- Why sorting?
  - Enables two pointers
  - Simplifies merging, interval problems, greedy approaches
- Complexities:
  - Simple (not used in real code):  
    - Selection sort, insertion sort → O(n²)
  - Practical:
    - Merge sort, quicksort, heapsort → O(n log n) average
- Java:
  - `Arrays.sort(int[])` = O(n log n) (dual-pivot quicksort for primitives)
  - `Arrays.sort(Object[])` uses TimSort (O(n log n) worst-case)
  - `Collections.sort(List<T>)` uses same TimSort.

### 2. Implement Simple Sorts (45–60 min)

Just for understanding; in practice you use `Arrays.sort`.

1. **Selection Sort (int array)**
   ```java
   void selectionSort(int[] nums) { ... }
   ```

2. **Insertion Sort (int array)**
   ```java
   void insertionSort(int[] nums) { ... }
   ```

Write them from scratch and:
- Print array before/after.
- State time complexity O(n²) and space O(1).

### 3. Java Sort Usage (15–20 min)

Practice:

- Sorting primitives:
  ```java
  int[] nums = {3,1,4,1,5};
  Arrays.sort(nums);
  ```

- Sorting objects with comparator:
  ```java
  Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
  ```

### 4. LeetCode Practice (30–45 min)

1. **Squares of a Sorted Array** (`#977`, Easy)
   - Option A: square then sort using `Arrays.sort`.
   - Option B (better): two pointers from ends, fill result from back.

2. If time: any easy sort-related problem (e.g., `#905 Sort Array By Parity`).

**Reflection (10–15 min)**  
- When does sorting simplify problems?
- How do time complexities compare: selection/insertion vs `Arrays.sort`?

---

## Day 2 – Classic Binary Search on Sorted Arrays

**Goal:** Implement standard binary search and gain confidence with indices.

### 1. Concept: Binary Search Template (30–40 min)

On paper, derive binary search:

- For sorted array `nums`, find target.
- Invariant: answer (if exists) lies within `[left, right]`.
- Typical code pattern:

```java
int left = 0, right = nums.length - 1;
while (left <= right) {
    int mid = left + (right - left) / 2;
    if (nums[mid] == target) return mid;
    else if (nums[mid] < target) left = mid + 1;
    else right = mid - 1;
}
return -1;
```

Discuss briefly:
- Why `left + (right - left)/2` (avoid overflow).
- Condition `left <= right` vs `left < right` – be consistent.

### 2. Implement Binary Search Variants (45–60 min)

1. **Exact match**
   ```java
   int binarySearch(int[] nums, int target) { ... }
   ```

2. **Search Insert Position** (`#35` pattern)
   - If target found, return index; otherwise index where it would be.
   ```java
   int searchInsert(int[] nums, int target) { ... }
   ```

3. **Find first element ≥ target** (lower bound)
   ```java
   int lowerBound(int[] nums, int target) { ... } // returns index
   ```

Test on small arrays by hand.

### 3. LeetCode Practice (60–75 min)

1. **Binary Search** (`#704`, Easy)
   - Implement standard template.

2. **Search Insert Position** (`#35`, Easy)
   - Reuse variant.

3. **First Bad Version** (`#278`, Easy)
   - Binary search on a monotonic boolean function `isBadVersion(mid)`.

**Reflection (10–15 min)**  
- Where did you make most off-by-one mistakes, if any?
- Write down your “go-to” binary search skeleton.

---

## Day 3 – Boundary Binary Search & Rotated Arrays

**Goal:** Handle “first/last occurrence” and apply binary search to rotated arrays.

### 1. Binary Search for First/Last Occurrence (30–45 min)

Concept:
- Sorted array may have duplicates.
- Find first index of `target` (leftmost) or last (rightmost).

Outline:

```java
int findFirst(int[] nums, int target) {
    int left = 0, right = nums.length - 1, ans = -1;
    while (left <= right) {
        int mid = left + (right - left)/2;
        if (nums[mid] >= target) {
            if (nums[mid] == target) ans = mid;
            right = mid - 1; // go left
        } else {
            left = mid + 1;
        }
    }
    return ans;
}
```

Similarly for `findLast`.

### 2. LeetCode Practice – Boundaries (45–60 min)

1. **Find First and Last Position of Element in Sorted Array** (`#34`, Medium)
   - Use `findFirst` and `findLast`.
   - Return `[first, last]`.

2. If time, re-implement `searchInsert` using similar logic.

### 3. Rotated Sorted Array (45–60 min)

Concept:
- Array is rotated at some pivot but originally sorted.
- Example: `[4,5,6,7,0,1,2]`.
- Binary search by:
  - Identifying which half is sorted.
  - Deciding which side to go.

LeetCode:

1. **Search in Rotated Sorted Array** (`#33`, Medium)
   - Key logic:
     - If `nums[left] <= nums[mid]`, left half is sorted.
     - Check if target is in [left, mid]; else go right half.
     - Else right half is sorted; check [mid, right].

**Reflection (10–15 min)**  
- How did you reason about which half is sorted?
- Note any mistakes with conditions in `#34` or `#33`.

---

## Day 4 – Binary Search on “Answer Space”

**Goal:** Use binary search to find minimal/maximal feasible value (very important pattern).

### 1. Concept: Binary Search on Answer (30–40 min)

Pattern:
- You’re asked for **minimum** or **maximum** value `x` such that some condition is possible.
- The condition is **monotonic**:
  - If capacity `C` works, any `C' > C` works.
  - If time `T` is enough, any `T' > T` is enough.

Generic template:

```java
int left = minPossible, right = maxPossible;
while (left < right) {
    int mid = left + (right - left) / 2;
    if (can(mid)) {
        right = mid;     // mid is feasible, try smaller
    } else {
        left = mid + 1;  // mid not feasible, go larger
    }
}
return left; // or right; they converge
```

Key is implementing `can(mid)`.

### 2. LeetCode Practice – Answer Space (75–105 min)

1. **Koko Eating Bananas** (`#875`, Medium)
   - Given pile sizes and `h` hours, find minimum eating speed.
   - `can(speed)` = total hours at that speed ≤ `h`.

2. **Capacity To Ship Packages Within D Days** (`#1011`, Medium)
   - Given package weights and `D` days, find minimal capacity.
   - `can(cap)`:
     - Simulate days; sum weights until exceeding `cap`, then new day.
     - Return whether needed days ≤ `D`.

If time remains:
- Re-read/annotate your `can` functions to see the monotonic property.

**Reflection (10–15 min)**  
- Identify:
  - What is your search space’s `left` and `right`?
  - Why is `can(x)` monotonic in these problems?
- This thinking will generalize to many scheduling/partition problems.

---

## Day 5 – Sorting + Two Pointers: 3Sum & Intervals

**Goal:** Use sorting to enable two pointers and interval merging.

### 1. Concept: Sort + Two Pointers (30–40 min)

Patterns:

- After sorting:
  - Use two pointers (low/high) to find combinations (e.g., 2-sum, 3-sum).
  - Merge intervals by sorting by start time.

Walk through examples:

- `3Sum`:
  - Sort array.
  - For each index `i`, fix `nums[i]`, then use two pointers `left/right` to find complementary pair.
  - Skip duplicates to avoid repeated triplets.

- Merge intervals:
  - Sort intervals by start.
  - Iterate and merge overlaps.

### 2. LeetCode Practice – Sort + Two Pointers (75–105 min)

1. **3Sum** (`#15`, Medium)
   - Steps:
     - Sort `nums`.
     - Loop `i` from 0 to n-3.
     - Skip duplicates for `i`.
     - For each `i`, set `left = i+1`, `right = n-1`.
     - Move pointers based on `sum = nums[i] + nums[left] + nums[right]`.
   - Watch out for duplicate triplets.

2. **Merge Intervals** (`#56`, Medium)
   - Represent intervals as `int[][] intervals`.
   - `Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));`
   - Use a `List<int[]>` to store merged intervals.

**If time:**
3. **Insert Interval** (`#57`, Medium, stretch)
   - Similar idea; not mandatory this week.

**Reflection (10–15 min)**  
- How did sorting reduce the complexity of `3Sum` vs naive O(n³)?
- In intervals, how does sorting by start time guarantee a simple linear merge?

---

## Day 6 – Mixed Binary Search Practice

**Goal:** Solidify binary search in various flavors with repeated practice.

### 1. Quick Recap (20–30 min)

On paper:

- Write pseudocode for:
  - `binarySearch` (exact match).
  - `lowerBound` (first ≥ target).
  - Binary search on answer skeleton with `can(mid)`.

### 2. LeetCode Practice – Mixed Set (75–105 min)

Solve or re-solve:

1. **Binary Search** (`#704`, Easy) – quick warmup, aim for <10 min.
2. **Search Insert Position** (`#35`, Easy).
3. **First Bad Version** (`#278`, Easy).
4. **Find First and Last Position of Element in Sorted Array** (`#34`, Medium).
5. **Search in Rotated Sorted Array** (`#33`, Medium).

If you have extra time:
6. Re-implement **Koko Eating Bananas** (`#875`) or **Ship Packages** (`#1011`) quickly without looking.

**Reflection (10–15 min)**  
- Which binary search variant still confuses you? Boundaries? Rotated arrays? Answer space?
- Note 1–2 “gotchas” you want to watch for (e.g. wrong loop condition, off-by-one).

---

## Day 7 – Review, Integration & Light Stretch

**Goal:** Tie binary search and sorting together; prepare for trees next week.

### 1. Concept Review (30–40 min)

In your notebook, answer:

- When would you choose:
  - **Sorting + two pointers** vs **HashMap**?
  - **Binary search** vs **linear scan**?
- For each binary search flavor, write a one-line description:
  - Exact match (704).
  - First/last occurrence (34).
  - Rotated array (33).
  - Answer space (875/1011).

Also, quickly sketch:

- Pseudocode for `3Sum`.
- Pseudocode for merging intervals.

### 2. Timed Re-Solves (60–90 min)

Pick 4–5 problems (mix of easy & medium), and solve each in **≤25–30 min**:

Recommended set:
- `#704 Binary Search`
- `#35 Search Insert Position`
- `#33 Search in Rotated Sorted Array`
- `#875 Koko Eating Bananas` or `#1011 Ship Packages Within D Days`
- `#15 3Sum` or `#56 Merge Intervals`

Stick to the pattern:
1. 5–7 minutes: think / plan on paper.
2. Code.
3. Quick test, then submit.

### 3. Stretch (Optional, 30–45 min)

Choose one more challenging problem to *attempt* (even partial):

- `#4 Median of Two Sorted Arrays` (Hard – advanced, just to read/think).
- Or an extra binary-search-on-answer problem (e.g., `#410 Split Array Largest Sum`, Hard, just reading/partial thinking OK).

You don’t have to finish; pay attention to:
- Problem statement.
- How you might frame an answer-space search.

**Reflection (10–15 min)**  
- Which pattern (plain BS, rotated, boundary, answer search) do you feel most comfortable with now?
- Write one “personal template” for binary search that you’ll reuse in future problems.

---

## How Week 4 Fits the Bigger Picture

By the end of Week 4, you’ll:

- Understand and use **sorting** strategically (not just mechanically).
- Be comfortable with multiple flavors of **binary search**, including on answer space.
- Have solved some core interview classics (`3Sum`, `Merge Intervals`, rotated array search).

Next steps (Week 5):

- Move into **Trees & BSTs**:
  - Tree traversals (preorder, inorder, postorder, level-order).
  - Recursion patterns.
  - Common LeetCode tree/BST problems.

If you want, I can next generate a **Week 5 – Day 1–7 plan** fully focused on trees and BSTs.
