Here is your **Day 1–Day 7 plan for Week 3**, focusing on:

- Sorting in Java (practical use + where it shows up in LeetCode)
- Binary Search (classic and variants)

Assume ~2–3 hours per day and adjust as needed.

---

## Day 1 – Sorting in Java: Essentials

**Goals:**
- Learn how to sort primitives and objects in Java.
- Understand when to use sorting as a first step in problem-solving.

### 1. Concept Primer (20–30 min)

Review/learn:
- Time complexity of common comparison-based sorts: **O(n log n)**.
- In Java you usually use:
  - `Arrays.sort()` for arrays.
  - `Collections.sort()` for lists.
- Sorting is often used before:
  - Two pointers (e.g., pair sum problems).
  - Binary search.
  - Grouping similar items.

### 2. Sorting Primitives (45–60 min)

Create class: `week3.day1.SortPrimitives`.

**Exercises:**

1. Sort an array of ints:
   ```java
   int[] nums = {5, 2, 9, 1, 5, 6};
   Arrays.sort(nums);
   // print sorted array
   ```

2. Sort array in **descending** order:
   - Option 1: sort ascending then reverse in-place.
   - Option 2: use `Integer[]` + custom comparator:
     ```java
     Integer[] numsObj = {5, 2, 9, 1, 5, 6};
     Arrays.sort(numsObj, (a, b) -> b - a);
     ```

3. Write a helper method:
   ```java
   public static void printArray(int[] arr) {
       for (int x : arr) System.out.print(x + " ");
       System.out.println();
   }
   ```

### 3. Sorting Objects (45–60 min)

Create class: `week3.day1.SortObjects`.

**Exercises:**

1. Define a simple `Person`:
   ```java
   class Person {
       String name;
       int age;
       Person(String name, int age) {
           this.name = name;
           this.age = age;
       }
   }
   ```

2. Create a `Person[]` array and sort by `age`:
   ```java
   Arrays.sort(people, Comparator.comparingInt(p -> p.age));
   ```

3. Practice:
   - Sort by name (alphabetical).
   - Sort by age descending.

**Concepts reinforced:**
- Difference between primitive and object arrays.
- Basic use of `Comparator`.

---

## Day 2 – Binary Search: Fundamentals

**Goals:**
- Implement classic binary search from scratch.
- Understand the idea of “searching in a sorted array in O(log n)”.

### 1. Concept Primer (20–30 min)

Key ideas:
- You can **only** apply binary search when there is some sorted / monotonic structure.
- Each step halves the search space.
- Basic pattern:
  ```java
  int left = 0, right = n - 1;
  while (left <= right) {
      int mid = left + (right - left) / 2;
      if (nums[mid] == target) { ... }
      else if (nums[mid] < target) left = mid + 1;
      else right = mid - 1;
  }
  ```

### 2. Implement Basic Binary Search (60–75 min)

Create class: `week3.day2.BinarySearchBasics`.

**Exercises:**

1. Implement:
   ```java
   public static int binarySearch(int[] nums, int target) {
       int left = 0, right = nums.length - 1;
       while (left <= right) {
           int mid = left + (right - left) / 2;
           if (nums[mid] == target) return mid;
           else if (nums[mid] < target) left = mid + 1;
           else right = mid - 1;
       }
       return -1;
   }
   ```
2. Test with:
   - `nums = {1, 3, 5, 7, 9}`, targets: `1, 5, 9, 2`.
3. Write a small main method to print results.

### 3. LeetCode: Binary Search (704, Easy) (30–45 min)

Create `week3.day2.LC704BinarySearch`.

- Implement using your own template (do not copy).
- Edge cases:
  - Single-element array.
  - Empty array (LeetCode might not use it, but think about it).

**Concepts reinforced:**
- Template memorization.
- Getting mid/index boundaries correct.

---

## Day 3 – Binary Search Variants (Boundaries)

**Goals:**
- Learn leftmost and rightmost occurrence binary search.
- Understand the idea of `lower_bound` / `upper_bound`-style logic.

### 1. Leftmost / Rightmost Binary Search (60–75 min)

Create class: `week3.day3.BoundaryBinarySearch`.

**Exercises:**

1. Leftmost index of target (`first >= target`):
   ```java
   public static int lowerBound(int[] nums, int target) {
       int left = 0, right = nums.length; // note: right = n (half-open interval)
       while (left < right) {
           int mid = left + (right - left) / 2;
           if (nums[mid] < target) {
               left = mid + 1;
           } else {
               right = mid;
           }
       }
       return left; // first position where nums[pos] >= target
   }
   ```

2. Rightmost index where `nums[pos] <= target` (or first > target):
   - Implement a similar function `upperBound(int[] nums, int target)`.

3. Test with arrays that contain duplicates:
   - `int[] nums = {1,2,2,2,3,4}; target = 2;`
   - Understand what `lowerBound` and `upperBound` should return.

### 2. LeetCode: Search Insert Position (35, Easy) (30–45 min)

Create `week3.day3.LC35SearchInsert`.

**Idea:**
- Use a variant of binary search:
  - If not found, `left` will be at the correct insert index.
- Return `left` after the loop.

### 3. LeetCode: First Bad Version (278, Easy) (30–45 min)

Create `week3.day3.LC278FirstBadVersion`.

**Idea:**
- You’re given `boolean isBadVersion(int version)`.
- Use binary search to find the minimum `version` such that `isBadVersion(version)` is true.

Template:
- `left = 1`, `right = n`
- While `left < right`:
  - If `isBadVersion(mid)` → search left half (`right = mid`)
  - Else → search right half (`left = mid + 1`)

**Concepts reinforced:**
- Binary search over *condition*, not exact value.
- Minimizing index that satisfies a predicate.

---

## Day 4 – Sorting + Binary Search on LeetCode

**Goals:**
- Combine sorting and binary search in solving problems.
- Practice slightly more complex binary search conditions.

### 1. Review Sorting + Two Pointers Combo (20–30 min)

Think through:
- When we sort first and then use:
  - Two pointers to find pairs/triplets.
  - Binary search to check existence.

You won’t fully dive into all pair-sum problems now, but just get the idea: sort → enable efficient searching.

### 2. LeetCode: Find Smallest Letter Greater Than Target (744, Easy) (30–45 min)

Create `week3.day4.LC744SmallestLetter`.

**Idea:**
- Sorted array of characters.
- Need the smallest letter > target (wrap around).
- Binary search to find first element > target.
  - If not found, answer is first element (wrap).

### 3. LeetCode: Peak Index in a Mountain Array (852, Easy) (45–60 min)

Create `week3.day4.LC852PeakIndex`.

**Idea:**
- Array increases then decreases (mountain).
- Use binary search on shape:
  - If `arr[mid] < arr[mid+1]`, peak is to the right.
  - Else, peak is to the left or at mid.

**Concepts reinforced:**
- Binary search with comparisons, not equality.
- Reasoning about array “shape”.

---

## Day 5 – Search in Rotated / Special Arrays

**Goals:**
- Apply binary search to non-trivially sorted arrays.
- Understand logic for rotated arrays.

### 1. Concept Primer: Rotated Sorted Array (20–30 min)

Given an array sorted in ascending order, then rotated at some pivot:
- Example: `[0,1,2,4,5,6,7]` → `[4,5,6,7,0,1,2]`
- Properties:
  - At least one half (left or right) is still sorted.
  - Use that to decide where to search.

### 2. LeetCode: Search in Rotated Sorted Array (33, Medium) (60–90 min)

Create `week3.day5.LC33SearchInRotated`.

**Approach:**
- Use binary search:
  - Let `mid` be middle.
  - If `nums[mid] == target` → done.
  - Determine which half is sorted:
    - If `nums[left] <= nums[mid]` → left half sorted.
      - If `target` is between `nums[left]` and `nums[mid]` → search left.
      - Else → search right.
    - Else → right half sorted.
      - If `target` is between `nums[mid]` and `nums[right]` → search right.
      - Else → search left.

**Concepts reinforced:**
- Using structure beyond simple sorted array.
- Condition-based binary search.

### 3. LeetCode: Find Peak Element (162, Medium) (45–60 min)

Create `week3.day5.LC162FindPeak`.

**Idea:**
- A peak is index `i` where `nums[i] >= neighbors`.
- Binary search:
  - If `nums[mid] < nums[mid + 1]`, go right.
  - Else, go left (including mid).

**Concepts reinforced:**
- Binary search for local optimum.
- Avoiding out-of-bounds (careful with indices).

---

## Day 6 – Practice & Integration: Sorting + Binary Search + Previous Patterns

**Goals:**
- Mix binary search with arrays, hashing, and two pointers.
- Strengthen understanding with more LeetCode.

### 1. LeetCode: Valid Triangle Number (611, Medium) – Optional if time (60–90 min)

Create `week3.day6.LC611ValidTriangle`.

**High-level idea:**
- Sort array.
- Use two pointers + binary search (or just two pointers) to count valid triangles.
- Even just reading this solution helps you see how sorting often comes first.

If this feels too advanced right now, you may skip or just read editorials/solutions without implementing fully.

### 2. Revisit Earlier Problems Using Binary Search Ideas (45–60 min)

Pick at least 2:

1. Re-implement:
   - **Binary Search (704)** from scratch, not looking at code.
2. Modify binary search to:
   - Return **leftmost index** of target in a sorted array with duplicates.
3. Write a helper:
   ```java
   public static boolean exists(int[] nums, int target) {
       return binarySearch(nums, target) != -1;
   }
   ```

### 3. Concept Drill (20–30 min)

On paper / in notes, write:

1. Binary search template with:
   - Return index if found, else -1.
2. Boundary-search template (`left < right` with half-open interval).
3. When to choose:
   - `while (left <= right)` vs `while (left < right)`.

---

## Day 7 – Review, Self-Test & Reflection

**Goals:**
- Solidify sorting and binary search knowledge.
- Make sure you can use these patterns without handholding.

### 1. Quick Written Quiz (20–30 min)

Without looking at code, write:

1. Code snippet to sort `int[] nums` ascending and then descending.
2. Binary search method header and body (for sorted `int[]`).
3. Short explanation:
   - Why does binary search run in O(log n)?
   - Why must the search space be sorted / monotonic?

### 2. Re-solve a Set of Problems (60–90 min)

In **new files**, solve from scratch:

(Choose at least 3; aim for 4 if time.)

1. **LC 704 – Binary Search (Easy)**  
2. **LC 35 – Search Insert Position (Easy)**  
3. **LC 278 – First Bad Version (Easy)**  
4. **LC 744 – Find Smallest Letter Greater Than Target (Easy)**  
5. **LC 162 – Find Peak Element (Medium)**  
6. **LC 33 – Search in Rotated Sorted Array (Medium)** (stretch if you feel ready)

For each:
- Before coding, write 3–5 lines of pseudocode.
- After solving, note:
  - Pattern: classic search / boundary search / condition search.
  - Time / space complexity.

### 3. Reflection & Prep for Week 4 (15–30 min)

Answer for yourself:

1. Can I implement binary search from memory without errors?
2. Do I understand how to tweak it for:
   - Left/right boundaries.
   - Searching conditions instead of exact targets.
3. Does sorting feel natural in Java (primitives vs objects)?

Note 1–2 problems/concepts to quickly revisit at the start of Week 4.

Week 4 will build on all of this with:
- Stacks & Queues
- Linked Lists
…so you’ll start combining patterns (e.g., binary search + linked lists later in your journey).

If you’d like, next I can:
- Generate the same Day 1–7 plan for **Week 4 (Stacks, Queues, Linked Lists)**, or
- Make a compact **Binary Search + Sorting cheat sheet** summarizing the core patterns and templates.
