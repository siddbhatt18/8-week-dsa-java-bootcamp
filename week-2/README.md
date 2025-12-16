Below is your **Day 1–Day 7 plan for Week 2**, focusing on:

- HashMap / HashSet
- Two Pointers
- Sliding Window  

Assume ~2–3 hours per day; adjust as needed.

---

## Day 1 – HashMap & HashSet Fundamentals

**Goals:**
- Understand what hash tables are and when to use `HashMap` and `HashSet`.
- Practice basic operations in Java.

### 1. Concept Primer (20–30 min)

Read/understand (notes or short article/video):

- Hash table idea: key → value mapping, average O(1) get/put.
- `HashMap<K, V>`:
  - Operations: `put`, `get`, `containsKey`, `remove`, `keySet`, `entrySet`.
- `HashSet<E>`:
  - Internally uses a `HashMap`.
  - Operations: `add`, `contains`, `remove`, iteration.

Think:  
- When do I need a map? (When I care about mapping key → value, like number → index.)  
- When do I need a set? (When I just care if something exists or not.)

### 2. Java Practice: HashMap (45–60 min)

Create class: `week2.day1.HashMapBasics`.

**Exercises:**

1. Frequency counter:
   ```java
   public static Map<String, Integer> wordFrequency(String[] words) {
       Map<String, Integer> map = new HashMap<>();
       for (String w : words) {
           map.put(w, map.getOrDefault(w, 0) + 1);
       }
       return map;
   }
   ```
   - Test it with: `{"apple", "banana", "apple", "orange", "banana", "apple"}`.

2. Invert map (if values are unique):
   ```java
   public static Map<Integer, String> invertMap(Map<String, Integer> map) {
       Map<Integer, String> inverted = new HashMap<>();
       for (Map.Entry<String, Integer> entry : map.entrySet()) {
           inverted.put(entry.getValue(), entry.getKey());
       }
       return inverted;
   }
   ```

3. Practice iteration:
   - Print all keys.
   - Print all values.
   - Print all key-value pairs.

### 3. Java Practice: HashSet (30–45 min)

Create class: `week2.day1.HashSetBasics`.

**Exercises:**

1. Remove duplicates from array:
   ```java
   public static int countUnique(int[] nums) {
       Set<Integer> set = new HashSet<>();
       for (int n : nums) set.add(n);
       return set.size();
   }
   ```

2. Intersection of two integer arrays:
   - Given `int[] a` and `int[] b`, return the set of elements that appear in both.
   - Use a `HashSet` for `a`, then check elements of `b`.

---

## Day 2 – More Hashing + LeetCode Practice (HashMap/HashSet)

**Goals:**
- Apply hashing to simple LeetCode problems.
- Strengthen your map/set usage.

### 1. Review (10–15 min)
From memory:
- Write the code snippet for:
  - Creating a `HashMap<String, Integer>`.
  - Incrementing a count with `getOrDefault`.
  - Creating a `HashSet<Integer>` and checking membership.

### 2. Revisit Two Sum (1, Easy) With HashMap (45–60 min)

Create `week2.day2.TwoSumRevisit`.

- Re-implement Two Sum from scratch using only the idea (not your old code).

Template:

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{}; // or throw exception
}
```

Analyze:
- Time complexity: O(n)
- Space complexity: O(n)

### 3. LeetCode: Contains Duplicate (217, Easy) – Re-solve (30–45 min)

Create `week2.day2.ContainsDuplicateRevisit`.

- Try to solve without looking:
  - Use `HashSet`.
  - Return true on the first duplicate, else false.

### 4. New LeetCode: Valid Anagram (242, Easy) With HashMap (30–45 min)

Create `week2.day2.ValidAnagramMap`.

- Implement using `Map<Character, Integer>` (not just array of 26).

Concepts reinforced:
- Character counting with `HashMap`
- Removing when count is zero (optional)

---

## Day 3 – Two Pointers (Fundamentals)

**Goals:**
- Understand two-pointer pattern: same-direction and opposite-ends.
- Implement basic two-pointer solutions on arrays/strings.

### 1. Concept Primer (20–30 min)

Two main versions:

1. Opposite ends:
   - `left = 0`, `right = n-1`
   - Move them towards each other based on some condition.
2. Same direction (fast/slow):
   - `slow` moves 1 step, `fast` moves 2 steps (cycle detection, skipping).

Use two pointers when:
- You have a sorted array/string.
- You’re searching for pairs/segments.
- You want in-place modifications without extra memory.

### 2. Practice: Opposite-Ends Two Pointers (45–60 min)

Create class: `week2.day3.TwoPointersOpposite`.

**Exercises:**

1. Check if an array is a palindrome:
   ```java
   public static boolean isPalindromeArray(int[] arr) {
       int left = 0, right = arr.length - 1;
       while (left < right) {
           if (arr[left] != arr[right]) return false;
           left++;
           right--;
       }
       return true;
   }
   ```

2. Given a sorted array and a target sum, check if any pair sums to target:
   ```java
   public static boolean hasPairWithSum(int[] nums, int target) {
       int left = 0, right = nums.length - 1;
       while (left < right) {
           int sum = nums[left] + nums[right];
           if (sum == target) return true;
           else if (sum < target) left++;
           else right--;
       }
       return false;
   }
   ```

### 3. LeetCode: Reverse String (344, Easy) – Re-solve (30–45 min)

Create `week2.day3.ReverseStringRevisit`.

- Implement with two pointers.
- Focus on clean, bug-free code.

### 4. LeetCode: Valid Palindrome (125, Easy) (45–60 min)

Create `week2.day3.ValidPalindromeLC`.

**Approach:**

- Convert to lowercase (or not strictly needed).
- Use `left` and `right`.
- While `left < right`:
  - Move left until it’s alphanumeric.
  - Move right until it’s alphanumeric.
  - Compare characters; if mismatch, return false.

Concepts reinforced:
- Two pointers on string
- Character checks with `Character.isLetterOrDigit`

---

## Day 4 – Two Pointers on Arrays (LeetCode Focus)

**Goals:**
- Use two pointers for in-place array operations.
- Solve classic Easy/Medium problems.

### 1. LeetCode: Move Zeroes (283, Easy) (45–60 min)

Create `week2.day4.MoveZeroesLC`.

**Idea:**
- Use a “slow” index `insertPos` to track where next non-zero should go.
- Iterate `i` from 0 to `n-1`:
  - If `nums[i] != 0`, set `nums[insertPos] = nums[i]`, `insertPos++`.
- After the loop, fill remaining positions with 0.

Concepts reinforced:
- In-place modification
- Two pointers in same direction (logical, not always two variables)

### 2. LeetCode: Remove Duplicates from Sorted Array (26, Easy) (45–60 min)

Create `week2.day4.RemoveDuplicatesLC`.

**Approach:**
- Input array is sorted.
- Use `slow` to mark index to write next unique.
- Loop `fast` from 1 to `n-1`:
  - If `nums[fast] != nums[slow]`:
    - `slow++`
    - `nums[slow] = nums[fast]`
- Return `slow + 1` as the length.

Concepts reinforced:
- Same-direction two pointers
- Handling sorted arrays

### 3. LeetCode: Two Sum II – Input array is sorted (167, Easy) (30–45 min)

Create `week2.day4.TwoSumIISortedLC`.

**Approach:**
- Since array is sorted:
  - `left = 0`, `right = n-1`
  - If `nums[left] + nums[right] < target` → `left++`
  - If `> target` → `right--`
  - If `== target` → found.

---

## Day 5 – Sliding Window (Basics)

**Goals:**
- Understand sliding window pattern: fixed and variable size.
- Implement basic windows on arrays.

### 1. Concept Primer (20–30 min)

Sliding window patterns:

1. Fixed-size window:
   - Window length `k`.
   - Maintain sum or some metric for `[i, i+k-1]`.
2. Variable-size window:
   - Expand `right` to satisfy condition.
   - Shrink from `left` when condition is violated.
   - Track best answer (max length, min length, etc.).

General template (variable):

```java
int left = 0;
for (int right = 0; right < n; right++) {
    // expand window with nums[right]

    while (/* condition violated */) {
        // shrink from left
        left++;
    }

    // update answer
}
```

### 2. Fixed-Size Window Practice (45–60 min)

Create `week2.day5.FixedWindowPractice`.

**Exercises:**

1. Maximum sum of any subarray of size `k`:
   - First compute sum of first `k`.
   - Slide window: subtract `nums[left]`, add `nums[right]` as you move.

2. Average of every subarray of size `k` (reuse sum from above).

### 3. Variable-Size Window: Intro Problem (45–60 min)

Create `week2.day5.VariableWindowPractice`.

**Exercise:**
- Given `int[] nums` and `int S`, find the minimum length of a contiguous subarray with sum ≥ S (if none, return 0).  
  (This is essentially LeetCode 209 – but try a custom version first.)

Idea:
- `left = 0`, `sum = 0`
- For each `right`:
  - Add `nums[right]` to `sum`.
  - While `sum >= S`:
    - Update minLength.
    - Subtract `nums[left]` from `sum`, `left++`.

---

## Day 6 – Sliding Window on Strings (LeetCode)

**Goals:**
- Apply sliding window to strings with sets/maps.
- Tackle an important Medium problem: Longest Substring Without Repeating Characters.

### 1. LeetCode: Longest Substring Without Repeating Characters (3, Medium) (60–90 min)

Create `week2.day6.LongestSubstringNoRepeatLC`.

**Approach 1 (with HashSet):**

- `Set<Character> set = new HashSet<>();`
- `left = 0`, `maxLen = 0`
- For `right` from 0 to n-1:
  - While `s.charAt(right)` is in set:
    - remove `s.charAt(left)` from set, `left++`
  - Add `s.charAt(right)` to set
  - Update `maxLen = max(maxLen, right - left + 1)`

**Approach 2 (with HashMap) – optional:**
- Track last index of each character.
- Move `left` to `max(left, lastIndex + 1)` when you see a repeated character.

Concepts reinforced:
- Sliding window on string
- Using `HashSet`/`HashMap` to manage window constraints

### 2. LeetCode: Minimum Size Subarray Sum (209, Medium) (45–60 min)

Create `week2.day6.MinSubArraySumLC`.

- This is the formal version of your Day 5 exercise.

**Approach:**
- Same as custom problem:
  - `left = 0`, `sum = 0`, `minLen = INF`
  - For each `right`:
    - Add `nums[right]` to `sum`
    - While `sum >= target`:
      - Update `minLen`
      - Subtract `nums[left]`, `left++`

Concepts reinforced:
- Variable-size window shrinks while maintaining condition
- Translating a pattern from your own exercise to LeetCode

---

## Day 7 – Integration & Mixed Review

**Goals:**
- Consolidate HashMap/HashSet, Two Pointers, Sliding Window.
- Solve a mix of old and new problems more independently.

### 1. Quick Concept Quiz (written, 20–30 min)

Without looking at notes, write down:

1. Code snippet to:
   - Create `HashMap<Integer, Integer>` and increment counts.
   - Create `HashSet<String>` and check membership.

2. Two-pointers template for:
   - Opposite ends in sorted array to find a pair sum.
   - Same direction for removing duplicates from sorted array.

3. Sliding window template for:
   - Longest substring without repeating characters.

Check your answers against your code afterwards.

### 2. Re-solve Key Problems From Scratch (60–90 min)

Pick at least **3** of these and solve in *new files* without copying:

1. **Two Sum II – Input array is sorted (167, Easy)**  
   - Two pointers.

2. **Move Zeroes (283, Easy)**  
   - Two pointers / write index.

3. **Valid Palindrome (125, Easy)**  
   - Two pointers on string.

4. **Minimum Size Subarray Sum (209, Medium)**  
   - Sliding window on array.

5. **Longest Substring Without Repeating Characters (3, Medium)**  
   - Sliding window on string with `HashSet` or `HashMap`.

After each:
- Write 2–3 lines:  
  - Pattern used (hashing / two pointers / sliding window)  
  - Time and space complexity

### 3. Identify Weak Spots & Plan for Week 3 (15–30 min)

Reflect:
- Which pattern feels hardest?
  - HashMap/HashSet logic?
  - Two pointers (off-by-one errors)?
  - Sliding window invariants?
- Note 1–2 problems you struggled on; mark them for a re-try next week.

Preview for **Week 3**:
- Sorting & Binary Search.
- You’ll often pair those with two pointers and hashing, so having this week strong will pay off.

---

If you’d like, I can now:
- Generate the same kind of **Day 1–7 plan for Week 3 (Sorting + Binary Search)**, or
- Make a one-page **cheat sheet for HashMap/HashSet, Two Pointers, Sliding Window in Java**.
