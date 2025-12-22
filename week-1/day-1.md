### Day 1 – Foundations: Big‑O Intuition + Java Arrays (Speed & Accuracy Focus)

**Main outcomes for today**

By the end of Day 1, you should be able to:

1. Look at a simple piece of code and estimate its time complexity.
2. Comfortably declare, initialize, and iterate over Java arrays.
3. Implement a few basic array functions **without** looking anything up.
4. Start building **speed and accuracy** through small, timed drills.

Plan for ~2–3 hours. If you have less time, keep the order but reduce the number of practice questions.

---

## Part 1 – Big‑O, But Only What You Really Need (45–60 min)

### 1.1 Concept: What Big‑O Actually Tells You

Focus only on the most common cases for interviews:

- **O(1)** – Constant time  
  Example: accessing `arr[i]`, basic arithmetic, reading a variable.

- **O(log n)** – Logarithmic  
  Example: binary search on a sorted array, repeatedly halving a search space.

- **O(n)** – Linear  
  Example: a single loop over an array.

- **O(n log n)** – “Linearithmic”  
  Example: efficient general‑purpose sorting (`Arrays.sort`).

- **O(n²)** – Quadratic  
  Example: nested loops over the full array (`for i` inside `for j`).

You do **not** need to master every complexity variant on Day 1. Focus on:

- “How many times does the innermost operation run compared to `n`?”
- “What loops or recursion drive the count?”

---

### 1.2 Guided Exercise: Estimating Complexity (on paper) – 20–25 min

Without IDE, on paper or a doc, try these. After you guess, verify your reasoning.

**Code A**

```java
int sum = 0;
for (int i = 0; i < n; i++) {
    sum += i;
}
```

- Q1: How many times does the body of the loop run (in terms of `n`)?
- Q2: What is the time complexity?  
- Q3: What is the extra space complexity?

**Code B**

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        System.out.println(i + " " + j);
    }
}
```

- Q4: How many times does `println` run?
- Q5: What is the time complexity?

**Code C**

```java
for (int i = 1; i < n; i *= 2) {
    System.out.println(i);
}
```

- Q6: How many times does this loop run relative to `n`?
- Q7: What is the time complexity?

**Code D**

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < 5; j++) {
        System.out.println(i + " " + j);
    }
}
```

- Q8: Is this O(n), O(n²), or something else? Why?

**Check your reasoning**

After you answer, confirm:

- A: O(n) time, O(1) extra space.
- B: O(n²) time.
- C: O(log n) time (i doubles each time).
- D: O(n) time (inner loop is constant 5; 5n is still O(n)).

If any of these surprised you, write a 1‑sentence explanation for that snippet (“This is O(n) because …”).

---

## Part 2 – Java Arrays: Syntax → Practice (45–60 min)

### 2.1 Concept: Arrays in Java (10–15 min)

Key points:

- Fixed size, contiguous block of memory.
- All elements have the same type.
- Access is O(1): `arr[i]`.

Basic patterns:

```java
// Declaration & initialization
int[] arr = new int[5];           // [0,0,0,0,0]
int[] arr2 = {1, 2, 3, 4};        // length 4

// Length
int n = arr2.length;

// Index-based loop
for (int i = 0; i < arr2.length; i++) {
    System.out.println(arr2[i]);
}

// Enhanced for loop
for (int num : arr2) {
    System.out.println(num);
}
```

Mentally note:

- Use **index loop** when you care about positions.
- Use **enhanced for loop** for simple iteration when you don’t need indices.

---

### 2.2 Coding: Warm‑up Implementation (in IDE) – 30–45 min

Create a file, e.g. `Day1Arrays.java` with a `main` method.

For each method:

- First **think in plain language** (1–2 lines).
- Then write code.
- Then write a comment above it with time & space complexity.

#### Function 1 – Sum of Array

```java
// Returns the sum of all elements in nums.
// Time: O(n), Space: O(1)
public static int sumArray(int[] nums) {
    // TODO: implement
}
```

Steps you should follow mentally:

- Initialize `sum = 0`.
- Loop over each element, add to sum.
- Return `sum`.

Test in `main`:

```java
public static void main(String[] args) {
    int[] a = {1, 2, 3, 4};
    System.out.println(sumArray(a)); // expected 10
}
```

#### Function 2 – Maximum in Array

```java
// Returns the maximum value in nums (assume nums.length > 0).
// Time: O(n), Space: O(1)
public static int maxInArray(int[] nums) {
    // TODO: implement
}
```

Reasoning:

- Initialize `max = nums[0]`.
- Loop from i = 1 to end:
  - If `nums[i] > max`, update `max`.
- Return `max`.

Test with:

- `[1, 2, 3, 4]` → 4  
- `[-5, -2, -10]` → -2

#### Function 3 – Reverse Array (New Array)

```java
// Returns a new array with elements of nums in reverse order.
// Time: O(n), Space: O(n)
public static int[] reverseArray(int[] nums) {
    // TODO: implement
}
```

Reasoning:

- Create `int[] res = new int[nums.length]`.
- For `i` from 0 to `nums.length - 1`:
  - `res[nums.length - 1 - i] = nums[i]`.
- Return `res`.

Test:

- Input: `[1, 2, 3]` → Output: `[3, 2, 1]`.

**Speed booster tip:**  
Try to type each function in **under 5 minutes** without logical errors. If you exceed that, after the first pass, re-implement once more to shorten your mental steps.

---

## Part 3 – Speed‑Oriented Practice Questions (Arrays & Big‑O)

We’ll use three difficulty levels. You don’t need LeetCode yet; keep it local for speed.

### 3.1 Level 1 – Accuracy First (No Timer at First)

Goal: 100% correct logic, clean code, correct complexity.

#### Q1. Count Even Numbers

**Task**

```java
// Count how many even numbers are in nums.
public static int countEvens(int[] nums) { ... }
```

Hints:

- Loop through `nums`.
- If `num % 2 == 0`, increment counter.

**After coding:**  
Write time & space complexity.

---

#### Q2. Contains Target

**Task**

```java
// Return true if target exists in nums, else false.
public static boolean contains(int[] nums, int target) { ... }
```

Hints:

- Linear scan, compare each element to target.
- Early return when found.

---

#### Q3. Count Element Occurrences

**Task**

```java
// Return how many times target appears in nums.
public static int countOccurrences(int[] nums, int target) { ... }
```

---

Once you can implement Q1–Q3 **without thinking hard**, you’re ready to add a timer (see 3.3).

---

### 3.2 Level 2 – Slightly More Thinking (Still Pure Arrays)

#### Q4. Check if Array is Sorted (Non‑Decreasing)

**Task**

```java
// Return true if nums is sorted in non-decreasing order (each element
// is >= previous element), else false.
public static boolean isSorted(int[] nums) { ... }
```

Hints:

- Edge cases: empty or single‑element arrays → sorted.
- Loop from i = 1 to n-1, compare `nums[i]` with `nums[i-1]`.

---

#### Q5. Find Second Largest Element

**Task**

```java
// Return the second largest distinct element in nums.
// Assume nums.length >= 2, and there is at least 2 distinct values.
public static int secondLargest(int[] nums) { ... }
```

Approach:

- Track `max` and `secondMax`:
  - Initialize `max = Integer.MIN_VALUE`, `secondMax = Integer.MIN_VALUE`.
  - For each `num`:
    - If `num > max`: set `secondMax = max`, `max = num`.
    - Else if `num < max && num > secondMax`: update `secondMax = num`.

Take it slow once to get the conditions right, then later aim for speed.

---

#### Q6. Reverse Array In‑Place

**Task**

```java
// Reverse nums in-place (modify the original array).
public static void reverseInPlace(int[] nums) { ... }
```

Approach:

- Two pointers: `left = 0`, `right = nums.length - 1`.
- While `left < right`, swap and move pointers inward.

Complexity: O(n) time, O(1) extra space.

---

### 3.3 Level 3 – Speed Drills (Once Logic is Solid)

Pick any 3–5 of the functions you wrote today:

- `sumArray`
- `maxInArray`
- `reverseArray`
- `contains`
- `isSorted`
- `reverseInPlace`

**Drill format (15–20 min):**

1. Set a timer for **5 minutes** per function.
2. In a fresh file (or fresh section):
   - Write the function **from scratch**.
   - Add a quick test in `main`.
3. Goal:
   - No compile errors.
   - Correct output for at least 2–3 quick test cases.
   - Time under 5 minutes, then gradually aim for **3 minutes** as you get comfortable.

If you often make off‑by‑one errors:

- After writing, **read the loop boundaries out loud**:
  - “i starts at 0, runs while i < nums.length…”

This deliberate check trains accuracy while you speed up.

---

## Part 4 – Short Big‑O Application Drill (10–15 min)

Look at the functions you just wrote and answer for each:

Example for `sumArray`:

- Time: O(n) – single loop through all elements.
- Space: O(1) – only uses `sum` and loop index.

Do the same for:

- `maxInArray`
- `reverseArray`
- `reverseInPlace`
- `secondLargest`
- `countOccurrences`

Write your answers in a notebook. This repetition makes Big‑O feel natural, not theoretical.

---

## Part 5 – Reflection & Planning (10–15 min)

In your notebook, write brief answers:

1. **Today I implemented:**
   - List 4–6 function names (e.g., `sumArray`, `reverseInPlace`, `secondLargest`).

2. **Patterns I noticed:**
   - Example: “Most array problems start with: initialize a variable, loop through array, update variable based on condition.”

3. **Where I was slow or error‑prone:**
   - Example: “Off‑by‑one in reverse; forgot to handle nums.length == 0 in isSorted.”

4. **Plan for Day 2 (preview):**
   - Re‑type `sumArray`, `maxInArray`, and `reverseInPlace` from memory as warm‑up.
   - Start transitioning to LeetCode (Two Sum) with the same careful thought → then optimize.

---

## Summary of Day 1 Practice Questions (Ordered by Difficulty)

**Level 1 – Foundation (Accuracy)**  
1. `sumArray(int[] nums)`  
2. `maxInArray(int[] nums)`  
3. `reverseArray(int[] nums)`  
4. `countEvens(int[] nums)`  
5. `contains(int[] nums, int target)`  
6. `countOccurrences(int[] nums, int target)`

**Level 2 – Slightly Harder Logic**  
7. `isSorted(int[] nums)`  
8. `secondLargest(int[] nums)`  
9. `reverseInPlace(int[] nums)`

**Level 3 – Speed Drills**  
- Re‑implement any of the above with a **per‑function timer**.

---

If you want, next I can:

- Turn Day 2 into a similarly detailed guide (introducing problem‑solving steps and Two Sum), or  
- Create a **daily “warm‑up drill sheet”** (short list of functions to re‑implement every morning for speed).
