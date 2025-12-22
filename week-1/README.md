**Week 1 Focus:**  
- Big‑O basics  
- Arrays & Strings in Java  
- Two pointers  
- Intro Sliding Window  
- Start LeetCode (with strong emphasis on thinking before seeing solutions)

Assume ~2–3 hours/day. Adjust times if needed; the order and “spirit” matter more than exact minutes.

---

## Day 1 – Big‑O + Java Arrays Basics

### 1. Concept Study (45–60 min)

**a) Big‑O (Practical View)**  
Read/watch about:
- Time complexity: O(1), O(log n), O(n), O(n log n), O(n²)
- Space complexity: additional memory used by your algorithm
- Examples:
  - Single loop over `n` items → O(n)
  - Nested loops over `n` items → O(n²)
  - Sorting an array with `Arrays.sort` → O(n log n)

**Your tasks (on paper):**
1. For each piece of code below, write its time complexity:

   ```java
   // A
   int sum = 0;
   for (int i = 0; i < n; i++) {
       sum += i;
   }

   // B
   for (int i = 0; i < n; i++) {
       for (int j = 0; j < n; j++) {
           System.out.println(i + " " + j);
       }
   }

   // C
   for (int i = 1; i < n; i *= 2) {
       System.out.println(i);
   }
   ```

2. Explain in one sentence why each one has that complexity.

**b) Java Arrays Basics**
- Syntax: declaration, initialization, access
  ```java
  int[] arr = new int[5];
  int[] arr2 = {1, 2, 3, 4};
  int x = arr2[0];
  ```
- Length: `arr.length`
- Looping:
  ```java
  for (int i = 0; i < arr.length; i++) {}
  for (int num : arr) {}
  ```

### 2. Coding Practice (45–60 min)

In your IDE, create a simple class `Day1Arrays`.

**Exercises (write your own, not copy/paste):**
1. **Sum of Array**
   - Method: `int sumArray(int[] nums)`
   - Return the sum of all elements.
   - In `main`, test with different arrays.

2. **Maximum in Array**
   - Method: `int maxInArray(int[] nums)`
   - Return the maximum element (assume `nums.length > 0`).
   - Think: what if all numbers are negative?

3. **Reverse Array (Create New Array)**
   - Method: `int[] reverseArray(int[] nums)`
   - Return a *new* array with elements reversed.

**Think Through (before coding):**
- What are the inputs/outputs?
- What’s the most straightforward way (brute force)?
- What’s the time complexity (Big‑O)?

Write a comment above each method with your complexity guess.

### 3. Reflection (10–15 min)

In a notebook:
- Write “Today I learned…” and list:
  - Big‑O types you saw
  - How to declare and loop an array
- Note one thing that was confusing to revisit tomorrow.

---

## Day 2 – Arrays Practice + Intro to LeetCode

### 1. Quick Review (15–20 min)
- Skim your Day 1 notes.
- Re‑implement **sumArray** and **maxInArray** from memory (without looking).
- Confirm they compile and run.

### 2. Concept Study: Problem‑Solving Steps (20–30 min)

Internalize a simple process for any problem:
1. Restate the problem in your own words.
2. Identify:
   - Input types and constraints (size of array? values range?)
   - Output required
3. Think of a **brute force** approach first.
4. Evaluate its complexity. Is it acceptable?
5. Think of optimizations (if needed).
6. Only then start coding.

### 3. LeetCode Setup (10–15 min)

- Create a LeetCode account.
- Configure it to use **Java** as default language.
- Learn how to:
  - Read constraints
  - Run code with “Run Code”
  - Submit solution

### 4. LeetCode Problem 1 – Two Sum (Easy) (60–75 min)

**Goal:** Learn how to approach and iterate on a problem.

1. **Read the problem carefully.**
   - Write out, in your own words, what it’s asking.
   - Note constraints: size of `nums`, value range, duplicates allowed?

2. **Think without coding (10–15 min).**
   - Brute force idea: nested loops, check all pairs:
     - Time complexity?
   - Any way to do better than O(n²)?
     - Hint to yourself: Can I store what I’ve seen so far?

3. **Approach 1 – Brute Force (nested loops).**
   - Implement O(n²) solution first.
   - Test with examples given and add a few of your own.

4. **Approach 2 – Optimized with HashMap.**
   - Idea: while iterating, store `value → index`. For each `nums[i]`, 
     - check if `target - nums[i]` is in the map.
   - Implement carefully.

5. **After Coding:**
   - Write in your notebook:
     - Brute force complexity.
     - Optimized complexity.
     - Why HashMap helps.

### 5. Light Practice (Optional, 20–30 min)

Implement:
- `boolean contains(int[] nums, int target)` – returns true if `target` exists in `nums`.  
  Estimate its complexity.

---

## Day 3 – Strings & StringBuilder

### 1. Concept Study (30–45 min)

**a) Strings in Java**
- `String` is immutable.
- Common methods: `length()`, `charAt(i)`, `substring`, `toCharArray()`.
- Building strings with concatenation in loops is inefficient.

**b) StringBuilder**
- Mutable sequence of characters.
- Useful for building/transforming strings in loops.
  ```java
  StringBuilder sb = new StringBuilder();
  sb.append('a');
  sb.append("hello");
  String result = sb.toString();
  ```

### 2. Coding Exercises (45–60 min)

Create class `Day3Strings`.

1. **Reverse String (using char array)**
   - Method: `String reverseString(String s)`
   - Idea:
     - Convert to `char[]`.
     - Swap from ends towards center.
   - Complexity?

2. **Count Vowels**
   - Method: `int countVowels(String s)`
   - Count how many of `a,e,i,o,u` (both uppercase/lowercase) in the string.

3. **Remove Vowels (use StringBuilder)**
   - Method: `String removeVowels(String s)`
   - Build a new string without vowels.

### 3. LeetCode Problem 2 – Valid Palindrome (Easy) (45–60 min)

**Think first (10–15 min):**
- You need to check if a string is the same forward and backward **ignoring non‑alphanumeric and case**.
- Ideas:
  - Clean string to only letters/digits, convert to same case, then check palindrome.
  - Or use two pointers moving inward, skipping invalid characters.

**Plan:**
1. Try to design a two‑pointer solution on paper:
   - `left = 0`, `right = s.length() - 1`.
   - While `left < right`:
     - Move `left` forward while `!Character.isLetterOrDigit(s.charAt(left))`.
     - Move `right` backward similarly.
     - Compare lowercase chars at left and right.

2. Implement in Java.
3. Add test cases in a local `main` before pasting into LeetCode (e.g., `"A man, a plan, a canal: Panama"`).

### 4. Reflection (10–15 min)

Write:
- What is the **two‑pointer** idea in your own words?
- Where else do you think two pointers might be useful?

---

## Day 4 – Two Pointers & In‑Place Array Manipulation

### 1. Quick Review (15–20 min)

- From memory, write the **two‑pointer** idea:
  - When we move from both ends?
  - When we move fast vs slow?
- Re‑implement `reverseString` quickly.

### 2. Concept Study: Two Pointers on Arrays (30–45 min)

Patterns:
- **Opposite ends:** start from `0` and `n-1` (e.g., palindrome, reverse in place).
- **Same direction:** one pointer lags behind another (we’ll see in linked lists later, but keep in mind).

### 3. Coding Practice (45–60 min)

Create `Day4TwoPointers`.

1. **Reverse Array In‑Place**
   - Method: `void reverseInPlace(int[] nums)`
   - Use `left` and `right`, swap elements.
   - Complexity?

2. **Move Zeros (Like LeetCode 283)** – but implement independently first.
   - Method: `void moveZeroes(int[] nums)`
   - Goal: move all zeros to the end while keeping non‑zero order.
   - First idea: create new array and copy non‑zeros. Complexity & extra space?
   - Try to improve to **in‑place**:
     - Use an index `pos` for where next non‑zero should go.

### 4. LeetCode Problem 3 – Move Zeroes (Easy) (45–60 min)

You’ve already thought about it:
- Step 1: Think and implement your own local version without looking.
- Step 2: Compare your approach to LeetCode after submitting.
- Step 3: Note if you used extra space or did it in‑place and why in‑place is better.

**Key concept reinforced:**  
- Two pointers (or a write pointer) to compact or reorganize arrays in‑place.

### 5. Short Written Exercise (10–15 min)

Answer on paper:
- Describe an array problem (that you invent) where two pointers starting from both ends is helpful.
- Describe another where one pointer writes and one reads (like move zeros).

---

## Day 5 – Intro to Sliding Window + Prefix Sums (Light)

### 1. Concept Study: Sliding Window (30–45 min)

Idea:
- You look at *continuous subarrays/substrings* and maintain some property (sum, length, distinct chars, etc.)
- Two main types:
  1. **Fixed size window** (e.g., “max sum of subarray of size k”)
  2. **Variable size window** (grow and shrink to satisfy constraints)

Walk through a simple example on paper:
- Array: `[1, 2, 3, 4, 5]`, window size `k = 3`.
  - Windows: `[1,2,3]`, `[2,3,4]`, `[3,4,5]`
  - Show how to compute each window sum by adding new element and subtracting old one.

### 2. Coding: Fixed Sliding Window (45–60 min)

Create `Day5SlidingWindow`.

1. **Max Sum of Subarray of Size K**
   - Method: `int maxSumSubarrayOfSizeK(int[] nums, int k)`
   - Steps:
     - Compute sum of first `k` elements.
     - Slide window: for i from k to n-1:
       - Add `nums[i]`, subtract `nums[i - k]`.
       - Track max sum.
   - Complexity?

2. **Simple Prefix Sum (Intro only)**
   - Method: `int[] prefixSums(int[] nums)`
     - `prefix[i]` = sum of nums[0..i-1] (length `n+1`).
   - Show how to get sum of any subarray `[l, r]` using `prefix[r+1] - prefix[l]`.

### 3. LeetCode Problem 4 – Maximum Subarray (Kadane’s) (Medium label, conceptually manageable) (60–75 min)

**Think first (15–20 min):**
- Problem: Find contiguous subarray with largest sum.
- Brute force: check all subarrays (O(n²) or O(n³)).
- Try to find a rule as you scan:
  - If current running sum becomes negative, does it help to keep it?

**Hint to push you:**
- Maintain `currentSum`. For each element `x`:
  - Either start a new subarray at `x`, or extend previous one:
    - `currentSum = max(x, currentSum + x)`
  - Track `maxSum`.

Implement Kadane’s algorithm after you’ve reasoned through at least one example array by hand (e.g. `[-2,1,-3,4,-1,2,1,-5,4]`).

### 4. Reflection (10–15 min)

On paper:
- Explain Kadane’s in your own words (no code, just concept).
- Describe how sliding window is different from prefix sums.

---

## Day 6 – Strings + Another Two‑Pointer Problem

### 1. Quick Review (15–20 min)

- Re‑implement fixed window sum problem quickly.
- Skim Kadane’s solution and make sure you still understand the idea.

### 2. Concept: More String Handling (20–30 min)

Review:
- `Character.isLetterOrDigit(c)`
- `Character.toLowerCase(c)`
- `String.trim()`, `split()` (for general familiarity)

### 3. LeetCode Problem 5 – Implement strStr() / Find Substring (Easy) (60–75 min)

**Goal:** Practice brute force and think about complexity.

1. **Understand the problem:**
   - Given `haystack` and `needle`, return first index of `needle` in `haystack`, or -1.
   - If `needle` is empty → return 0.

2. **Think (15–20 min) without coding:**
   - Brute force:
     - For each possible starting index `i` in `haystack`, compare characters `haystack[i + j]` vs `needle[j]`.
     - When mismatch, break and move to next `i`.

3. **Implement brute force.**
   - Carefully handle edge cases:
     - `needle.length() > haystack.length()`
     - `needle` empty

4. **Complexity:**
   - Worst case about O(n * m) where n is length of `haystack`, m of `needle`.

### 4. Optional Practice: Manual Two Pointer on Strings (20–30 min)

Write:
- Method `boolean isPrefix(String s, String prefix)`
  - Return true if `prefix` is a prefix of `s` (similar to `s.startsWith(prefix)`).
  - Use a simple loop, no library method.

### 5. Short Written Exercise (10–15 min)

Answer:
- For `strStr`, when is complexity O(n * m), and when closer to O(n)?
- What might be a “more advanced” algorithm for pattern searching (just names, no details)?  
  (e.g., KMP, Rabin‑Karp — just to plant a seed.)

---

## Day 7 – Consolidation & Mixed Practice

Today is review + tying concepts together. Focus on **doing from memory** and **explaining to yourself**.

### 1. Concept Review (30–45 min)

Without looking at notes initially, write on paper:

- Define these in 1–2 sentences each:
  - O(1), O(n), O(n²)
  - Two pointers
  - Sliding window
  - Prefix sum
- List at least 3 array problems and which pattern might help for each.

Then check your notes and fill any gaps.

### 2. Re‑implement Key Functions from Memory (60–75 min)

In a new file `Week1Review.java`, re‑implement (no copy/paste; only from what’s in your head):

1. `int sumArray(int[] nums)`
2. `int maxInArray(int[] nums)`
3. `void reverseInPlace(int[] nums)`
4. `String reverseString(String s)`
5. `boolean isPalindromeAlnum(String s)` – from **Valid Palindrome**
6. `int maxSumSubarrayOfSizeK(int[] nums, int k)`
7. `int maxSubArray(int[] nums)` – Kadane

After writing each:
- Add a comment with:
  - Time complexity
  - Space complexity (not counting input array/string)

### 3. LeetCode Mixed Block (60–90 min)

**Goal:** Apply patterns without much guidance.

Try to solve these **in order**, giving each at least 20 minutes before looking at hints:

1. **Contains Duplicate** (Easy)  
   - Pattern: HashSet, O(n)
   - If you get stuck, ask: “Can I track what I’ve seen so far?”

2. **Best Time to Buy and Sell Stock** (Easy)  
   - Pattern: Single pass, track min price and max profit.
   - Think: As you walk through prices, what info do you need to keep?

If you still have energy:

3. **Another pass on Two Sum**  
   - Solve it again **from scratch**, this time aiming to write clean code quickly and confidently.

### 4. End‑of‑Week Reflection (15–20 min)

Write a short summary:
- Which patterns do you feel most comfortable with?
- Which ones are still fuzzy (e.g., sliding window vs prefix sums)?
- A list of at least 3 questions you have going into Week 2 (e.g., “When exactly do I use HashMap vs array for counts?”).

Keep this summary; it will guide what to emphasize next week (hashing + more sliding window).

---

If you’d like, next I can:
- Turn Week 2 into a similar Day‑by‑Day plan,  
- Or help you build a **daily checklist** template (so each day you know: review X, learn Y, solve Z problems).
