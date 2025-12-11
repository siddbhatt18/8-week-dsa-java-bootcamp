Below is your **Week 1: Day 1–7 plan**, with concrete tasks and time blocks. Adjust timings if you have more/less time, but keep the **order**: learn → write code → solve LeetCode → reflect.

---

## Day 1 – Big-O & Java Refresh

**Goal:** Understand time complexity and refresh Java basics you’ll use constantly.

### 1. Theory (45–60 min)
- Read / watch about:
  - What Big-O measures (worst-case growth with input size).
  - Common complexities:  
    - O(1), O(log n), O(n), O(n log n), O(n²)
  - How to read loops for complexity:
    - Single loop → usually O(n)  
    - Nested loops → usually O(n²)  
    - Halving input each step → O(log n)
- Learn how extra data structures affect **space complexity** (arrays, maps, etc.).

### 2. Java Basics Review (30–45 min)
Write small snippets (in your IDE) for each:

- Arrays:
  ```java
  int[] arr = {1, 2, 3};
  System.out.println(arr.length);
  ```
- 2D Arrays:
  ```java
  int[][] grid = {{1,2},{3,4}};
  ```
- Strings:
  ```java
  String s = "hello";
  System.out.println(s.charAt(1));
  System.out.println(s.substring(1, 3));
  System.out.println(s.length());
  ```
- `StringBuilder`:
  ```java
  StringBuilder sb = new StringBuilder();
  sb.append("hi");
  sb.append("!");
  System.out.println(sb.toString());
  ```

### 3. Complexity Estimation Exercises (30 min)
On paper or notes:

- For each pseudo-code, write time complexity:

  ```java
  // A
  for (int i = 0; i < n; i++) {
      System.out.println(i);
  }
  ```

  ```java
  // B
  for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
          System.out.println(i + j);
      }
  }
  ```

  ```java
  // C
  int i = 1;
  while (i < n) {
      i = i * 2;
  }
  ```

Compare with solutions from a Big-O reference afterwards.

---

## Day 2 – Arrays & Strings Fundamentals

**Goal:** Get comfortable iterating arrays and strings, and modifying them.

### 1. Array Operations (45–60 min)
Implement these as **separate methods** in Java. Don’t copy-paste code; type fully.

1. **Find max in array**
   ```java
   int findMax(int[] nums) { ... }
   ```
2. **Find min in array**
3. **Compute sum and average of array**
4. **Reverse an array in-place**
   - Using two pointers: `left` and `right`.

### 2. String Operations (45–60 min)
Implement:

1. **Reverse a string**
   - Using `char[]`:
     ```java
     String reverseString(String s) { ... }
     ```
   - And using `StringBuilder` (for comparison).

2. **Count vowels in a string**  
3. **Check if two strings are equal ignoring case, without using `equalsIgnoreCase`**
   - Compare lengths and lowercase versions (`toLowerCase()`).

### 3. Quick Self-Check (15–20 min)
For each function, ask:
- What’s the time complexity?
- Can I do it in-place or do I need extra memory?

---

## Day 3 – Two Pointers Basics + First LeetCode Problems

**Goal:** Learn the two-pointer pattern and apply it to simple problems.

### 1. Two Pointers Concept (30–45 min)
Study:
- When to use two pointers:
  - Checking palindrome.
  - Reversing arrays/strings.
  - Merging sorted arrays.
- Patterns:
  - Pointers at both ends moving inward.
  - Pointers moving in the same direction (will see more later).

### 2. Implement Classic Two-Pointer Functions (45–60 min)
In Java, implement:

1. **Check if a string is palindrome**
   ```java
   boolean isPalindrome(String s) { ... }
   ```
   - Use two indices `i = 0`, `j = s.length()-1`.

2. **Reverse char array in-place**
   ```java
   void reverse(char[] chars) { ... }
   ```

3. **Merge two sorted arrays into a new sorted array (not LeetCode 88 yet)**
   ```java
   int[] mergeSorted(int[] a, int[] b) { ... }
   ```
   - Two pointers `i` and `j` for `a` and `b`, merge into result.

### 3. LeetCode Practice (60–75 min)

Create a LeetCode account if you haven’t.

1. **Two Sum** (`#1`, Easy)
   - First: brute force (double loop).
   - Then: HashMap solution.
   - Focus: reading constraints, writing clean code.

2. **Best Time to Buy and Sell Stock** (`#121`, Easy)
   - Think:
     - Track minimum price so far.
     - For each price, compute potential profit.

If you have time:
3. **Valid Palindrome** (`#125`, Easy)
   - Reuse your palindrome idea but:
     - Skip non-alphanumeric characters.
     - Use `Character.isLetterOrDigit` and `Character.toLowerCase`.

---

## Day 4 – More Arrays + Strings & Two Pointers

**Goal:** Consolidate array/string skills and handle LeetCode-style input/output.

### 1. Refine Java Skills (30–45 min)
Practice:

- Enhanced for-loop:
  ```java
  for (int num : nums) { ... }
  ```
- Utility methods:
  - `Arrays.toString(nums)`
  - Creating arrays of given size: `new int[n];`
- Reading problem statements carefully and translating to method signature.

### 2. Implement:
1. **Remove all occurrences of a value from array and return new length**  
   (similar to LeetCode `#27 Remove Element`, but you can just create a new array or do in-place for practice).

2. **Rotate an array by k steps to the right (simple version)**  
   - Start with extra array:
     ```java
     int[] rotateRight(int[] nums, int k) { ... }
     ```
   - (In-place version can be done later.)

### 3. LeetCode Practice (60–90 min)

1. **Merge Sorted Array** (`#88`, Easy)
   - Read the problem carefully; merging is done **in-place** in `nums1`.
   - Use two pointers from the end:
     - `p1` at end of real data in `nums1`.
     - `p2` at end of `nums2`.
     - Fill from the end of `nums1`.

2. **Move Zeroes** (`#283`, Easy)
   - Two pointers:
     - `slow` for the position of the next non-zero.
     - `fast` to scan array.

If extra time / energy:
3. Re-solve **Two Sum** without looking at your old code.

---

## Day 5 – HashMap & HashSet Introduction

**Goal:** Learn hashing tools that you’ll use constantly.

### 1. HashMap & HashSet Basics (45–60 min)
Study / practice:

- HashMap:
  ```java
  Map<Integer, Integer> map = new HashMap<>();
  map.put(key, value);
  map.get(key);
  map.containsKey(key);
  map.remove(key);
  ```
- HashSet:
  ```java
  Set<Integer> set = new HashSet<>();
  set.add(val);
  set.contains(val);
  set.remove(val);
  ```

### 2. Implement Small Hash Problems (45–60 min)
1. **Frequency map of array elements**
   ```java
   Map<Integer, Integer> frequencyMap(int[] nums) { ... }
   ```

2. **First non-repeating character in a string**
   ```java
   int firstUniqChar(String s) { ... } // return index, or -1
   ```
   - Use HashMap to count characters, then scan string again.

3. **Check if two strings are anagrams (simple, assuming lowercase a–z)**  
   - Option A: HashMap for char counts.  
   - Option B: int[26] frequency array.

### 3. LeetCode Practice (60–90 min)

1. **Contains Duplicate** (`#217`, Easy)
   - Use HashSet; check if add operation reveals duplicates.

2. **Valid Anagram** (`#242`, Easy)
   - Use your own anagram check code.

If doing well:
3. **Two Sum** (`#1`, Easy, again)  
   - Now, try to code it from memory **quickly** (~10 minutes).

---

## Day 6 – Sliding Window Intro + Key Problem

**Goal:** Learn sliding window and apply it to an important string problem.

### 1. Sliding Window Concept (30–45 min)
Study:
- Fixed window vs variable window:
  - Fixed: window size is known (e.g., size k).
  - Variable: Expand/shrink until condition met.
- Pattern:
  ```java
  int left = 0;
  for (int right = 0; right < n; right++) {
      // include s[right] in window

      while (window is invalid) {
          // shrink from left
          left++;
      }

      // now window [left, right] is valid, maybe update result
  }
  ```

### 2. Simple Sliding Window Exercise (30–45 min)
Implement a fixed-size sliding window:

1. **Maximum sum of any subarray of size k**
   ```java
   int maxSumSubarrayOfSizeK(int[] nums, int k) { ... }
   ```
   - First compute sum of first k elements.
   - Then slide window: subtract `nums[left]`, add `nums[right]`.

### 3. LeetCode Practice – Sliding Window (60–90 min)

1. **Longest Substring Without Repeating Characters** (`#3`, Medium)
   - Treat this as your **main challenge** today.
   - Use:
     - `int left = 0;`
     - HashMap or array to store last index of each character.
   - Logic:
     - Expand right.
     - If character repeated and its last occurrence index ≥ `left`, move `left` to `lastIndex + 1`.
     - Update best length.

If time permits:
2. Review your solution, then:
   - Close it.
   - Re-implement from scratch once more.

---

## Day 7 – Review, Reinforce, and Light Challenge

**Goal:** Consolidate everything from week 1; re-solve and slightly push difficulty.

### 1. Quick Review (30–45 min)
Without coding, in your own words (notebook):

- What is Big-O and why do we care?
- When do you use:
  - Two pointers?
  - HashMap vs HashSet?
  - Sliding window?
- Write skeleton code for:
  - Binary search (you’ll use it next week).
  - A simple two-pointer loop to reverse an array.

### 2. Re-solve 2–3 Problems (60–90 min)
Pick from:

1. **Two Sum** (`#1`, Easy) – one final quick run (10–15 min).
2. **Best Time to Buy and Sell Stock** (`#121`, Easy).
3. **Valid Palindrome** (`#125`, Easy) or your own palindrome function.
4. **Move Zeroes** (`#283`, Easy).

Aim:  
- Solve **without looking at old code**.  
- Think: identify pattern first, then code.

### 3. Stretch Challenge (Optional, 30–45 min)
Try to start **Container With Most Water** (`#11`, Medium):

- Don’t worry if you don’t finish.
- Think in terms of two pointers at the ends of the array:
  - Move the pointer pointing to the **shorter** line inward.
- Even 30 minutes of struggling is useful; read solution afterward.

---

## How to Use This Week

- **Minimum viable day:** If busy, at least:
  - 1 theory section (or review notes).
  - 1 LeetCode problem fully solved.
- Keep a **log**:
  - Date
  - Problems attempted
  - What pattern / data structure was used
  - One mistake/lesson learned

If you’d like next, I can create a similar **Day 8–14 plan for Week 2**, focused on HashMap/HashSet and more sliding window.
