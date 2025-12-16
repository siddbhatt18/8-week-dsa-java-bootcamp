### Week 1 – Day 3  
**Theme:** Arrays Practice + First LeetCode Problems (Two Sum & Contains Duplicate)  
**Goal for today:**  
- Deepen your understanding of arrays via common patterns (reverse, search, prefix sums).  
- Learn how to read and approach a LeetCode problem systematically.  
- Implement and submit your first 2 LeetCode solutions in Java.

---

## 0. High-Level Plan (2–3 hours)

1. Quick review (10–15 min)  
2. Array practice utilities (reverse, search, prefix sums) (45–60 min)  
3. LeetCode: Two Sum (1) – brute force + HashMap (60–75 min)  
4. LeetCode: Contains Duplicate (217) – using HashSet (30–45 min)  
5. Short reflection & pattern summary (10–15 min)

Work inside package: `week1.day3`.

---

## 1. Quick Review from Day 2 (10–15 min)

Without looking at code, in a notebook / text file:

1. Write how to:
   - Declare an array of 5 integers: `arr`.
   - Initialize `int[] nums = {1, 4, 9};`
2. Write a `for` loop that:
   - Prints all elements of `nums` using indices.
3. Write a method header:
   ```java
   public static int maxArray(int[] arr)
   ```
4. Describe in words what this code does:
   ```java
   int sum = 0;
   for (int value : arr) {
       sum += value;
   }
   ```

Then glance quickly through your `ArrayBasics`, `ArrayMethods`, and `ArrayPracticeDay2` to refresh.

---

## 2. Array Practice Utilities (45–60 min)

Today we’ll build a small collection of array utilities. These patterns show up repeatedly in DSA.

Create `ArrayPracticeDay3.java` in `week1.day3`:

```java
package week1.day3;

public class ArrayPracticeDay3 {

    // 1. Reverse array: returns a NEW array
    public static int[] reverseArray(int[] arr) {
        int n = arr.length;
        int[] result = new int[n];
        for (int i = 0; i < n; i++) {
            result[i] = arr[n - 1 - i];
        }
        return result;
    }

    // 2. Find index of target (linear search), -1 if not found
    public static int findIndex(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                return i;
            }
        }
        return -1;
    }

    // 3. Build prefix sums array
    // prefix[i] = arr[0] + arr[1] + ... + arr[i]
    public static int[] prefixSums(int[] arr) {
        int n = arr.length;
        int[] prefix = new int[n];
        if (n == 0) return prefix; // empty array, return empty

        prefix[0] = arr[0];
        for (int i = 1; i < n; i++) {
            prefix[i] = prefix[i - 1] + arr[i];
        }
        return prefix;
    }

    // 4. Query sum of subarray [l, r] using prefix sums
    public static int rangeSum(int[] prefix, int l, int r) {
        if (l == 0) {
            return prefix[r];
        } else {
            return prefix[r] - prefix[l - 1];
        }
    }

    public static void main(String[] args) {
        int[] data = {3, 1, 4, 1, 5};

        // Test reverseArray
        int[] reversed = reverseArray(data);
        System.out.print("Reversed: ");
        for (int x : reversed) {
            System.out.print(x + " ");
        }
        System.out.println();

        // Test findIndex
        System.out.println("Index of 4: " + findIndex(data, 4));
        System.out.println("Index of 9: " + findIndex(data, 9));

        // Test prefix sums
        int[] prefix = prefixSums(data);
        System.out.print("Prefix sums: ");
        for (int x : prefix) {
            System.out.print(x + " ");
        }
        System.out.println();

        // Test rangeSum with prefix (sum of indices 1..3 => 1 + 4 + 1 = 6)
        int l = 1, r = 3;
        int sum13 = rangeSum(prefix, l, r);
        System.out.println("Sum from index " + l + " to " + r + " = " + sum13);
    }
}
```

Run and verify:

- Reverse logic
- Index search correctness
- Prefix sums and rangeSum correctness

### 2.1 Concept Notes

- **Reverse pattern:** index from start maps to index from end: `n - 1 - i`.
- **Linear search:** simple `for` and `==` compare.
- **Prefix sums:** powerful pattern to answer many range-sum queries in O(1) after O(n) precompute.

---

## 3. LeetCode Workflow Introduction (10–15 min)

Before coding the actual LeetCode problems, get used to a structured workflow you’ll use daily.

For each problem:

1. **Read & Restate**  
   - Read the problem once fully.
   - In your own words: “We are given … we must return …”
2. **Identify Input/Output**  
   - Types: `int[]`, `int`, `boolean`, etc.
   - Constraints (rough idea is enough early on).
3. **Start with Brute Force**  
   - Don’t jump directly to optimal.
   - Think: “What’s the simplest way ignoring efficiency?”
4. **Then Improve with Known Patterns**  
   - HashMap, HashSet, two pointers, etc.
5. **Write Pseudocode Before Java**  
   - 3–10 lines in plain English.
6. **Implement in Java + Test Small Cases**  
   - Use main method or LeetCode’s run feature.
7. **Analyze Complexity**  
   - Time: O(n), O(n²), etc.
   - Space: additional memory?

Now apply this to Two Sum.

---

## 4. LeetCode: Two Sum (Problem 1, Easy) (60–75 min)

### 4.1 Read & Restate

Open LeetCode: https://leetcode.com/problems/two-sum/

- You get an array `nums` and an integer `target`.
- You must return **indices** of the two numbers such that `nums[i] + nums[j] == target`.
- You can’t use the same element twice.
- Exactly one valid answer exists.
- Order of indices doesn’t really matter (e.g., `[1, 2]` or `[2, 1]`).

### 4.2 Brute Force Idea

- For every pair `(i, j)` with `i < j`, check if `nums[i] + nums[j] == target`.
- If yes, return `[i, j]`.

**Pseudo-code (brute force):**

```
for i from 0 to n-1:
    for j from i+1 to n-1:
        if nums[i] + nums[j] == target:
            return [i, j]
return []  // or per problem statement (though LC guarantees solution)
```

Time: O(n²). Space: O(1).

### 4.3 Implement Brute Force in Java (Locally)

Create `TwoSumBrute.java` in `week1.day3`:

```java
package week1.day3;

import java.util.Arrays;

public class TwoSumBrute {

    public static int[] twoSumBrute(int[] nums, int target) {
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        // Problem guarantees a solution, but we return an empty array just in case
        return new int[]{};
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        int[] res = twoSumBrute(nums, target);
        System.out.println("Result: " + Arrays.toString(res)); // Expect [0, 1]
    }
}
```

Run and confirm.

### 4.4 Optimized Idea – HashMap

Goal: avoid O(n²). Idea:

- For each element `nums[i]`, we want another element `target - nums[i]`.
- Use a **HashMap** to remember numbers we’ve seen and their indices.
- As we go through the array:
  - Let `current = nums[i]`
  - `complement = target - current`
  - If `complement` is already in the map, return `[map.get(complement), i]`
  - Else store `current` and its index in the map.

Pseudo-code:

```
create empty map: value -> index
for i from 0 to n-1:
    complement = target - nums[i]
    if map contains complement:
        return [map[complement], i]
    put nums[i] -> i in map
```

Time: O(n). Space: O(n).

### 4.5 Implement Optimized Two Sum in Java

Create `TwoSumLC.java` in `week1.day3`:

```java
package week1.day3;

import java.util.HashMap;
import java.util.Map;
import java.util.Arrays;

public class TwoSumLC {

    // Optimized O(n) solution using HashMap
    public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>(); // value -> index

        for (int i = 0; i < nums.length; i++) {
            int current = nums[i];
            int complement = target - current;

            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }

            map.put(current, i);
        }

        // As per problem, there will always be one solution
        return new int[]{};
    }

    public static void main(String[] args) {
        int[] nums1 = {2, 7, 11, 15};
        int target1 = 9;
        System.out.println("Test 1: " + Arrays.toString(twoSum(nums1, target1)));

        int[] nums2 = {3, 2, 4};
        int target2 = 6;
        System.out.println("Test 2: " + Arrays.toString(twoSum(nums2, target2)));

        int[] nums3 = {3, 3};
        int target3 = 6;
        System.out.println("Test 3: " + Arrays.toString(twoSum(nums3, target3)));
    }
}
```

Run and check:

- Expected outputs:
  - Test 1: indices like `[0, 1]`
  - Test 2: `[1, 2]`
  - Test 3: `[0, 1]`

### 4.6 Submit on LeetCode

1. Go back to the Two Sum problem on LeetCode.
2. Choose language: **Java**.
3. Paste the body of `twoSum` method into the LeetCode template (do not include `main`).
4. Click **Run Code** with sample tests.
5. Click **Submit**.

**Reflect:**  
- Brute force: O(n²) time, O(1) extra space.  
- Optimized: O(n) time, O(n) space (for HashMap).  
- Pattern: **Array + HashMap for complement lookup**.

---

## 5. LeetCode: Contains Duplicate (Problem 217, Easy) (30–45 min)

### 5.1 Read & Restate

Open: https://leetcode.com/problems/contains-duplicate/

- Given an integer array `nums`.
- Return `true` if any value appears at least twice.  
- Return `false` if all elements are distinct.

### 5.2 Brute Force Idea (Concept Only)

- Compare every pair `(i, j)`, `i < j`.  
- If `nums[i] == nums[j]`, return `true`. Else after checking all pairs, return `false`.
- Time: O(n²). Space: O(1).  
You don’t have to implement this; just understand it.

### 5.3 Optimized Idea – HashSet

- Use a `HashSet<Integer>`.
- Scan the array:
  - If the set already contains `nums[i]`, return `true`.
  - Else add `nums[i]` to the set.
- If we finish loop without finding duplicates, return `false`.

Pseudo-code:

```
create empty set
for each num in nums:
    if num in set:
        return true
    else:
        add num to set
return false
```

Time: O(n). Space: O(n).

### 5.4 Implement Contains Duplicate in Java

Create `ContainsDuplicateLC.java` in `week1.day3`:

```java
package week1.day3;

import java.util.HashSet;
import java.util.Set;

public class ContainsDuplicateLC {

    public static boolean containsDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<>();

        for (int num : nums) {
            if (seen.contains(num)) {
                return true; // found a duplicate
            }
            seen.add(num);
        }

        return false; // no duplicates
    }

    public static void main(String[] args) {
        int[] a = {1, 2, 3, 1};
        int[] b = {1, 2, 3, 4};
        int[] c = {1, 1, 1, 3, 3, 4, 3, 2, 4, 2};

        System.out.println("a has duplicate: " + containsDuplicate(a)); // true
        System.out.println("b has duplicate: " + containsDuplicate(b)); // false
        System.out.println("c has duplicate: " + containsDuplicate(c)); // true
    }
}
```

Run locally and verify outputs.

### 5.5 Submit on LeetCode

1. Go to the Contains Duplicate problem page.
2. Choose **Java**.
3. Paste the body of `containsDuplicate` into their template.
4. Run then Submit.

**Pattern:**  
- This is your first **“HashSet for duplicate detection”** pattern.

---

## 6. Short Reflection & Pattern Summary (10–15 min)

Answer these questions in your notes:

1. For **Two Sum**:
   - What is the brute-force approach? Time complexity?
   - What is the optimized approach?  
   - What role does the HashMap play?
2. For **Contains Duplicate**:
   - Why is a HashSet a good fit?
   - What’s the time and space complexity?
3. Arrays:
   - Explain what prefix sums are and one use-case.
   - Explain the difference between returning a **new reversed array** vs. reversing in-place.

If any explanation feels shaky, revisit that section or code.

---

## 7. Optional Extra Practice (If Time Allows)

### 7.1 Re-implement Without Looking

In a new file `TwoSumFromScratch.java`:

- Implement the optimized `twoSum` from memory.
- Test with a few inputs.
- Then compare with your earlier `TwoSumLC` implementation.

### 7.2 Small Custom Problems (In `ArrayExtrasDay3.java`)

Try to implement:

1. `int countOccurrences(int[] arr, int target)`  
   - Count how many times `target` appears.
2. `boolean containsValue(int[] arr, int target)`  
   - Return `true` if `target` appears, else `false`.
3. `int[] copyArray(int[] arr)`  
   - Return a new array that is an exact copy of `arr`.

---

## 8. Preview of Day 4

On **Day 4**, you will:

- Dive into **Strings** in Java (`String` vs `StringBuilder`).  
- Practice string operations: character access, transformations, building new strings.  
- Implement simple string-based problems that prepare you for **Valid Anagram (242)** and later two-pointer problems.

If you’d like, I can next create a detailed, structured **Day 4 of Week 1** guide focused on string fundamentals.
