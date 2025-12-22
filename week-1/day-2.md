### Day 2 – Arrays Review + Intro to Problem‑Solving & First HashMap Pattern (Two Sum)

**Main outcomes for today**

By the end of Day 2, you should be able to:

1. Re‑implement core array functions from Day 1 quickly and correctly.
2. Follow a **clear, repeatable problem‑solving process** for DSA questions.
3. Solve **Two Sum** using both brute force and an optimized `HashMap` solution.
4. Apply arrays + loops + simple logic to a few new problems of rising difficulty.

Plan for ~2–3 hours. If you have less time, keep the order but cut some practice questions.

---

## Part 1 – Short Review: Solidify Day 1 (20–30 min)

Goal: Refresh core array operations and warm up your brain.

### 1.1 Re‑implement Key Functions (from memory)

In a new file `Day2Warmup.java`, **without looking** at yesterday’s code, implement:

1. `sumArray(int[] nums)`
2. `maxInArray(int[] nums)`
3. `reverseInPlace(int[] nums)`

Skeleton:

```java
public class Day2Warmup {

    public static int sumArray(int[] nums) {
        // TODO
    }

    public static int maxInArray(int[] nums) {
        // TODO
    }

    public static void reverseInPlace(int[] nums) {
        // TODO
    }

    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4};
        System.out.println(sumArray(a));       // expected 10
        System.out.println(maxInArray(a));     // expected 4
        reverseInPlace(a);                     // expected [4, 3, 2, 1]
        for (int x : a) System.out.print(x + " ");
    }
}
```

After coding:

- Add time/space complexity comments above each method.
- If you had to think hard or got stuck:
  - Note which parts were fuzzy (loop boundaries? initial values?).

This quickly tells you what to reinforce later.

---

## Part 2 – A Simple, Repeatable Problem‑Solving Process (20–30 min)

You’ll use this for almost every DSA problem.

### 2.1 The 6‑Step Process

For any new problem:

1. **Restate the problem** in your own words.
   - “Given X, return Y such that condition Z holds.”

2. **Identify inputs and outputs**
   - Types (int[], String, int, etc.)
   - Constraints (size of input? range of values? duplicates allowed?)

3. **Design a brute‑force solution first**
   - Even if it’s O(n²) or worse.
   - Ask: “If I ignore performance, how can I guarantee correctness?”

4. **Analyze the brute‑force complexity**
   - Time: loops, nested loops.
   - Space: extra data structures.

5. **Search for patterns / optimizations**
   - Can I use a HashMap/HashSet?
   - Two pointers? Sorting? Prefix sums?
   - Can I avoid repeated work?

6. **Only then write code**
   - After you’re clear on the approach.
   - Then test with the sample cases and your own edge cases.

### 2.2 Tiny Exercise: Apply the Process (5–10 min)

Take this very simple problem (don’t code yet, just think):

> Given an array of integers, return the **index** of the first occurrence of a target, or -1 if it doesn’t exist.

On paper or in a doc, write:

1. Your restatement in your own words.
2. Input/output types (e.g., `int[] nums`, `int target`, return `int` index).
3. Brute force in plain language (1–3 bullet points).
4. Time & space complexity of brute force (it’s already optimal here, but still analyze).

You’ll repeat this thinking style for real interview‑style problems.

---

## Part 3 – LeetCode‑Style Problem: Two Sum (70–90 min)

Now we apply the process to a classic problem and introduce `HashMap`.

### 3.1 Understand the Problem (10–15 min, **no coding yet**)

LeetCode: **Two Sum** (Easy)

> Given an array of integers `nums` and an integer `target`, return *indices* of the two numbers such that they add up to target.  
> You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

On paper:

1. Restate:
   - “Given an int array and a target sum, find two different indices i, j such that `nums[i] + nums[j] == target`. Return `[i, j]` in any order.”

2. Inputs/Outputs:
   - Input: `int[] nums`, `int target`
   - Output: `int[]` of length 2 (indices)

3. Constraints (read from LeetCode):
   - `2 <= nums.length <= ...`
   - Values might be negative/positive, duplicates allowed.
   - Exactly one solution.

4. Brute force idea:
   - Use nested loops: for each i, try all j > i, check `nums[i] + nums[j] == target`.

5. Complexity of brute force:
   - Time: O(n²)
   - Space: O(1)

Only after this, move to coding.

---

### 3.2 Implement Brute Force First (15–20 min)

In `Day2TwoSum.java`:

```java
import java.util.Arrays;

public class Day2TwoSum {

    // Brute force O(n^2)
    public static int[] twoSumBrute(int[] nums, int target) {
        // TODO: nested loops
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        System.out.println(Arrays.toString(twoSumBrute(nums, target))); // [0, 1] or [1, 0]
    }
}
```

Plan:

- For i from 0 to n-1:
  - For j from i+1 to n-1:
    - If `nums[i] + nums[j] == target`, return `{i, j}`.

If no pair found (though problem guarantees one), you can return something like `{-1, -1}` by convention.

After coding:

- Confirm O(n²) time and O(1) extra space in comments.

---

### 3.3 Optimize Using HashMap (Core Learning Moment) (30–40 min)

Now improve time from O(n²) → O(n).

#### Concept: Using a Map to Remember What You’ve Seen

Idea:

- As you scan the array, for each number `nums[i]`, you need `target - nums[i]`.
- If you’ve seen that complement before (at some index j), then `nums[i] + nums[j] == target`.
- Use a `HashMap<Integer, Integer>` to map `value → index` of seen elements.

Pseudocode (write this before Java):

- Create empty map `valToIndex`.
- For each index `i`:
  - Let `curr = nums[i]`.
  - Let `need = target - curr`.
  - If `need` is in map: return `{map.get(need), i}`.
  - Else: put `curr → i` in map.

#### Implementation

Add to `Day2TwoSum.java`:

```java
import java.util.HashMap;
import java.util.Map;

public class Day2TwoSum {

    // Optimized O(n) using HashMap
    public static int[] twoSumHashMap(int[] nums, int target) {
        // TODO: implement
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;

        System.out.println(Arrays.toString(twoSumBrute(nums, target)));
        System.out.println(Arrays.toString(twoSumHashMap(nums, target)));
    }
}
```

Explain to yourself:

- Why is time O(n)?
  - Single pass, each HashMap operation is average O(1).
- Why extra space is O(n)?
  - In worst case, we store every element in the map.

Run with a few tests:

- `{2, 7, 11, 15}, 9` → `[0, 1]`
- `{3, 2, 4}, 6` → indices of 2 and 4
- `{3, 3}, 6` → `[0, 1]`

#### Mental checkpoint

Write in your notebook:

- “For Two Sum, brute force is nested loops (O(n²)). With HashMap, we scan once, storing value → index and checking complement in O(1), so total O(n).”

This is your **first major “pattern”**:
> Array + HashMap to find pair with given sum.

You’ll see this pattern repeatedly with small variations.

---

## Part 4 – Additional Practice Questions (Arrays + Logic) of Increasing Difficulty

Use these to reinforce arrays, loops, and problem‑solving. Do as many as your time/energy allows.

### Level 1 – Direct Array Manipulation (Accuracy First)

#### Q1. Index of First Occurrence (Linear Search)

**Task**

```java
// Return the index of the first occurrence of target in nums, or -1 if not found.
public static int indexOf(int[] nums, int target) { ... }
```

Approach:

- Loop i from 0 to n-1.
- If `nums[i] == target`, return i.
- If end of loop reached, return -1.

---

#### Q2. Last Occurrence

**Task**

```java
// Return the index of the last occurrence of target in nums, or -1 if not found.
public static int lastIndexOf(int[] nums, int target) { ... }
```

Options:

- Loop from end to start and return first match.
- Or loop from start, updating an `answer` variable whenever you see target.

---

#### Q3. Count Greater Than X

**Task**

```java
// Return how many elements in nums are strictly greater than x.
public static int countGreaterThan(int[] nums, int x) { ... }
```

Simple linear scan; good for building speed and confidence.

---

### Level 2 – Slightly More Logic/Edge Cases

#### Q4. Remove All Occurrences of a Value (Return New Array)

**Task**

```java
// Return a new array that has all elements of nums except those equal to val.
public static int[] removeElementNewArray(int[] nums, int val) { ... }
```

Plan:

1. First pass: count how many elements are NOT equal to `val`.
2. Second pass: create new array of that size and fill it with those elements.

This introduces:
- Two‑pass algorithms.
- Thinking about size first, then constructing result.

---

#### Q5. Merge Two Sorted Arrays (Simple Version)

Given two **individually sorted** arrays `a` and `b`, merge them into a new sorted array.

```java
// Given 2 sorted arrays a and b, return a new sorted array containing all their elements.
public static int[] mergeSorted(int[] a, int[] b) { ... }
```

Approach:

- Use two pointers `i` for `a`, `j` for `b`.
- Compare `a[i]` and `b[j]`, take the smaller into result.
- Move the pointer of the array from which you took the element.
- When one array ends, copy the remaining of the other.

This prepares you for merging in **Merge Two Sorted Lists** later.

---

### Level 3 – Early Pattern Recognition (Stretch, Optional)

#### Q6. Two Sum (Brute Only, from Memory)

After doing the guided Two Sum once, **later in the day or tomorrow**:

- Close all code.
- Re‑implement `twoSumBrute` **from scratch** in a new file in under 10 minutes.
- Then optionally also re‑implement `twoSumHashMap`.

This measures retention.

---

#### Q7. Pair Exists With Given Sum (Boolean Version)

Similar to Two Sum, but **only return true/false**, not indices.

```java
// Return true if there exists a pair (i != j) such that nums[i] + nums[j] == target.
// Use the best approach you can think of.
public static boolean hasPairWithSum(int[] nums, int target) { ... }
```

Try to:

- First write brute force.
- Then write a HashSet/HashMap version (conceptually similar to Two Sum).

---

## Part 5 – Speed & Accuracy Drill (15–20 min)

Pick 3–4 of the easier functions from today and yesterday:

- `indexOf`
- `lastIndexOf`
- `countGreaterThan`
- `sumArray`
- `maxInArray`

For each function:

1. Set a **4–5 minute timer**.
2. Write it from scratch in a clean file or at bottom of current file.
3. Add 1–2 quick test cases in `main`.
4. Check correctness quickly.

Focus on:

- No off‑by‑one errors.
- Clean, consistent loop structure.
- Getting faster each time you repeat.

You are building **muscle memory** for array iteration.

---

## Part 6 – Reflection & What to Watch for Tomorrow (10–15 min)

In your notebook:

1. **Today I applied:**
   - Arrays + loops.
   - Brute force + optimization thinking.
   - First use of a `HashMap` (`value → index` mapping).

2. **What I found tricky:**
   - e.g., Remembering when to put into the map for Two Sum,
   - Handling edge cases in merge,
   - Off‑by‑one in lastIndexOf.

3. **Patterns I recognize now:**
   - “Find two numbers that do something” → maybe HashMap or two pointers if sorted.
   - “Search for a value/condition” → simple linear scan with return or boolean flag.

4. **Tomorrow’s focus (preview):**
   - Strings + `StringBuilder`.
   - A two‑pointer string problem (**Valid Palindrome**).
   - More array/string practice with increasing difficulty.

---

### Summary of Day 2 Practice Questions (DSA + Difficulty Ladder)

**Core guided problem**  
- LeetCode: Two Sum  
  - Brute force (O(n²))  
  - Optimized with HashMap (O(n))

**Level 1 (Fundamentals)**  
1. `indexOf(int[] nums, int target)`  
2. `lastIndexOf(int[] nums, int target)`  
3. `countGreaterThan(int[] nums, int x)`

**Level 2 (More Logic)**  
4. `removeElementNewArray(int[] nums, int val)`  
5. `mergeSorted(int[] a, int[] b)`

**Level 3 (Pattern Reinforcement / Stretch)**  
6. Re‑implement `twoSumBrute` (later in the day)  
7. `hasPairWithSum(int[] nums, int target)` (boolean version of Two Sum)

If you’d like, next I can create:

- A detailed **Day 3 guide** (Strings + StringBuilder + Valid Palindrome), or  
- A “daily warm‑up” list that you repeat every morning in 20 minutes to cement arrays and HashMap basics.
