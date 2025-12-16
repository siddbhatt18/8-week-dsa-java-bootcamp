Below is a **Day 1–Day 7 plan for Week 1** focused on Java basics, arrays, and strings.  
Assume ~2–3 hours per day. Adjust time up/down as needed.

---

## Day 1 – Setup & Java Basics

**Goals:**
- Set up Java environment and IDE.
- Understand and run a simple Java program.
- Learn basic Java syntax: variables, types, conditionals.

### 1. Environment Setup (30–45 min)
- Install:
  - **JDK 17+**
  - **IDE**: IntelliJ IDEA Community (recommended) or VS Code with Java extension.
- Create a project:
  - New Java project: `dsa-java-learning`
  - Create package: `week1.day1`
  - Add class: `HelloWorld.java`

**Practice:**
```java
package week1.day1;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, DSA in Java!");
    }
}
```
- Run it. Confirm it prints the message.

### 2. Java Basics (60–90 min)
Learn:
- Primitive types: `int`, `long`, `double`, `boolean`, `char`
- Reference types: `String`
- Variables and assignment:
  ```java
  int age = 25;
  double height = 1.75;
  boolean isStudent = true;
  ```
- Conditionals:
  ```java
  if (age >= 18) {
      System.out.println("Adult");
  } else {
      System.out.println("Minor");
  }
  ```
- Loops:
  - `for` loop
  - `while` loop

**Exercises (code in `week1.day1.BasicsPractice`):**
1. Write a program to:
   - Declare an `int` `a = 10`, `b = 3`.
   - Print:
     - `a + b`
     - `a - b`
     - `a * b`
     - `a / b` (integer division)
2. Write a program to:
   - Read a number from code (hardcode a value, no input needed).
   - Print “Even” if divisible by 2, else “Odd”.

### 3. Methods (30–45 min)
Learn:
- Method signature:
  ```java
  public static int add(int x, int y) {
      return x + y;
  }
  ```

**Exercise:**
- In `week1.day1.MethodsPractice`:
  - Write methods:
    - `int square(int n)`
    - `boolean isPositive(int n)`
  - Call them from `main` and print results.

---

## Day 2 – More Java Essentials + Intro to Arrays

**Goals:**
- Get comfortable with loops and methods.
- Learn how to declare, initialize, and iterate over arrays.

### 1. Loop Practice (45–60 min)
In `week1.day2.LoopPractice`:

**Exercises:**
1. Print numbers from 1 to 20 using a `for` loop.
2. Print the sum of numbers from 1 to 100.
3. Print the multiplication table of 5 (from 5×1 to 5×10).

### 2. Arrays Basics (60–90 min)
Learn:
- Declaration & initialization:
  ```java
  int[] arr = new int[5];
  int[] nums = {1, 2, 3, 4, 5};
  ```
- Access:
  - `arr[0]` for first element
  - `arr[arr.length - 1]` for last element
- Loop through arrays:
  ```java
  for (int i = 0; i < nums.length; i++) {
      System.out.println(nums[i]);
  }

  for (int num : nums) {
      System.out.println(num);
  }
  ```

**Exercises (in `week1.day2.ArrayBasics`):**
1. Create an `int[]` of length 5; assign values and print all.
2. Write a method `int sumArray(int[] arr)` that returns the sum of elements.
3. Write a method `int maxArray(int[] arr)` that returns the maximum element.

### 3. First LeetCode-Style Thinking (30–45 min)
Without coding yet, read these problem statements to get used to the style:
- **Two Sum (1)**
- **Contains Duplicate (217)**

For each:
- Restate the problem in your own words.
- Identify input type (`int[]`, `int`).
- Identify output type (`int[]`, `boolean`, etc.).

---

## Day 3 – Arrays Practice + First LeetCode Problems (Easy)

**Goals:**
- Practice array operations.
- Solve your first LeetCode problems in Java.

### 1. Practice Common Array Tasks (45–60 min)
In `week1.day3.ArrayPractice`:

**Implement:**
1. `int[] reverseArray(int[] arr)`  
   - Create a new array, fill it with elements from end to start.
2. `int findIndex(int[] arr, int target)`  
   - Return index of `target` or `-1` if not found (linear search).
3. `int[] prefixSums(int[] arr)`  
   - `prefix[i] = arr[0] + ... + arr[i]`.

### 2. LeetCode: Two Sum (1, Easy) (60–90 min)
- Create a class `week1.day3.TwoSumLC`.

**Steps:**
1. Read the problem statement carefully on LeetCode.
2. Brute force idea:
   - Double loop: check all pairs.
3. Implement brute force in Java.
4. Then learn optimal `HashMap` approach:
   ```java
   Map<Integer, Integer> map = new HashMap<>();
   for (int i = 0; i < nums.length; i++) {
       int complement = target - nums[i];
       if (map.containsKey(complement)) {
           return new int[]{map.get(complement), i};
       }
       map.put(nums[i], i);
   }
   ```

**Concepts reinforced:**
- Array indexing
- Basic `HashMap` usage (quick preview of Week 2)

### 3. LeetCode: Contains Duplicate (217, Easy) (30–45 min)
- Class: `week1.day3.ContainsDuplicateLC`

**Approach:**
- Use a `HashSet<Integer>`:
  - Iterate through array, if `set.contains(num)` → return true; else `set.add(num)`.

**Concepts reinforced:**
- Looping over arrays
- `HashSet` operations (also preview for Week 2)

---

## Day 4 – Strings Fundamentals

**Goals:**
- Understand String basics.
- Practice simple string operations.

### 1. String Basics (45–60 min)
Learn:
- `String` is immutable.
- Useful methods:
  - `length()`
  - `charAt(i)`
  - `toLowerCase()`, `toUpperCase()`
  - `substring(start, end)`
  - `indexOf()`, `contains()`
- `StringBuilder` basics:
  ```java
  StringBuilder sb = new StringBuilder();
  sb.append("Hello");
  sb.append(" ");
  sb.append("World");
  String result = sb.toString();
  ```

**Exercises (in `week1.day4.StringBasics`):**
1. Given `String s = "HelloWorld";`
   - Print the first character, last character, and length.
2. Implement `String toUpperCaseManual(String s)`:
   - Use `charAt` and `Character.toUpperCase`.
3. Implement `String reverseString(String s)` using:
   - (a) StringBuilder’s `reverse` method  
   - (b) Manual loop from end to start.

### 2. Character Counting (45–60 min)
In `week1.day4.CharCount`:

**Exercises:**
1. Count vowels in a lowercase string.
2. Implement `boolean isAnagramSimple(String s, String t)`:
   - Assume only lowercase letters a–z.
   - Use `int[26]` frequency arrays:
     - Increment for `s`, decrement for `t`.
     - Check all counts are zero.

This prepares you for **Valid Anagram (242)**.

### 3. Light Concept Review (15–30 min)
- Review:
  - Arrays syntax
  - For loops
  - Basic methods
- Try to explain to yourself:
  - How to reverse an array
  - How to reverse a string

---

## Day 5 – LeetCode Strings & Arrays (Easy)

**Goals:**
- Apply string & array concepts to LeetCode.
- Practice debugging and thinking about edge cases.

### 1. LeetCode: Valid Anagram (242, Easy) (45–60 min)
- Class: `week1.day5.ValidAnagramLC`

**Steps:**
1. Re-read your `isAnagramSimple` from Day 4.
2. Adapt it to full LeetCode solution:
   - Handle length mismatch (if lengths differ, return false).
   - Use frequency array or `HashMap<Character, Integer>` (try both if you have time).

**Concepts reinforced:**
- Frequency counting
- Comparing two strings via counts, not sort cost (optional: also try solution using `Arrays.sort(char[])`).

### 2. LeetCode: Valid Palindrome (125, Easy) – Optional Preview of Two Pointers (45–60 min)
- Class: `week1.day5.ValidPalindromeLC`

**Approach:**
- Convert string to lowercase.
- Use two pointers `left` and `right`.
- Move them inward while:
  - Skipping non-alphanumeric characters with `Character.isLetterOrDigit`.
  - Checking equality of characters.

**Concepts reinforced:**
- String traversal
- Basic two-pointer logic (important for later weeks)

### 3. Array Review: Small Custom Problems (30–45 min)
In `week1.day5.ArrayReview`:

**Exercises:**
1. Rotate array right by 1: `[1,2,3,4] → [4,1,2,3]` (not in-place required yet).
2. Find second largest number in an array (assume length ≥ 2).

---

## Day 6 – More Arrays: Prefix Sums & Simple Patterns

**Goals:**
- Understand prefix sums.
- Solve 1–2 simple LC-style tasks using arrays.

### 1. Prefix Sums (45–60 min)
In `week1.day6.PrefixSumPractice`:

**Learn & Implement:**
- `int[] buildPrefixSum(int[] nums)`
  - `prefix[0] = nums[0]`
  - `prefix[i] = prefix[i-1] + nums[i]`
- Given `prefix`, sum of subarray `[l, r]`:
  - If `l == 0`: `prefix[r]`
  - Else: `prefix[r] - prefix[l - 1]`

**Exercise:**
- Given `int[] nums` and queries `(l, r)`, return subarray sum for each query using prefix sums.

### 2. LeetCode: Best Time to Buy and Sell Stock (121, Easy) (45–60 min)
- Class: `week1.day6.BestTimeToBuySellStockLC`

**Approach:**
- Maintain:
  - `minPriceSoFar`
  - `maxProfit = 0`
- For each price `p`:
  - `minPriceSoFar = min(minPriceSoFar, p)`
  - `maxProfit = max(maxProfit, p - minPriceSoFar)`

**Concepts reinforced:**
- Single-pass array scanning
- Maintaining running min and best result

### 3. LeetCode: Reverse String (344, Easy) (30–45 min)
- Class: `week1.day6.ReverseStringLC`

**Approach:**
- Input is `char[] s`
- Use two pointers `left`, `right`.
- Swap `s[left]` and `s[right]`, move inward until `left >= right`.

**Concepts reinforced:**
- In-place modification
- Two-pointer basics

---

## Day 7 – Consolidation & Self-Check

**Goals:**
- Review everything from Week 1.
- Identify weak spots.
- Attempt 1–2 problems with minimal help.

### 1. Concept Review (45–60 min)
Without looking at code:
- Write on paper / notes:
  - Syntax to create:
    - An integer array of length 10.
    - A `StringBuilder`.
  - The for-loop template for iterating over an array.
  - Method signature for a function that takes `int[]` and returns `int`.

Then:
- Re-open your code for:
  - `TwoSumLC`
  - `ValidAnagramLC`
  - `BestTimeToBuySellStockLC`
- For each, write a 3–4 line explanation of:
  - Main idea
  - Time complexity
  - Space complexity

### 2. Independent Practice (60–90 min)
Try to solve (with as little help as possible):

1. **LeetCode: Move Zeroes (283, Easy)**  
   - Class: `week1.day7.MoveZeroesLC`
   - Goal: Move all `0`s to the end while keeping the order of non-zero elements.
   - Hint: Think in terms of a “write index” that tracks where the next non-zero should go.

2. Re-solve one of:
   - **Two Sum (1)**
   - **Valid Anagram (242)**
   - **Best Time to Buy and Sell Stock (121)**  
   from scratch in a new file (no copy-pasting). Time yourself: aim for <20 minutes.

### 3. Reflection (15–30 min)
Ask yourself:
- Which of these do I feel least confident about?
  - Loops
  - Arrays
  - Strings
  - HashMap/HashSet basics you touched
- Note these; you’ll reinforce them early in Week 2.

---

If you want, next I can:
- Turn Week 2 into a similar Day 1–7 plan (HashMap/HashSet, two pointers, sliding window),  
- Or provide a short “cheat sheet” of Java syntax you should memorize before moving on.
