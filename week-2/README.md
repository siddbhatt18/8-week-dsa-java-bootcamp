Here’s your **Week 2: Day 8–14 plan** (I’ll still call them Day 1–7 for Week 2), focused on **HashMap/HashSet** and **Two Pointers / Sliding Window**. The structure mirrors Week 1: learn → implement → LeetCode → reflect.

---

## Week 2 – Focus

- Hash-based structures: `HashMap`, `HashSet`
- Classic problems with counts/frequencies, lookups, grouping
- Stronger grip on two pointers & sliding window

---

## Day 1 (Week 2) – HashMap Deep Dive & Frequency Patterns

**Goal:** Become comfortable using HashMap for frequency counting and lookups.

### 1. HashMap Usage Patterns (30–45 min)

Review & practice:

- Basic operations
  ```java
  Map<Character, Integer> map = new HashMap<>();
  map.put('a', 1);
  int val = map.getOrDefault('a', 0);
  boolean hasKey = map.containsKey('a');
  map.remove('a');
  ```

- Common idiom: **frequency counting**
  ```java
  for (char c : s.toCharArray()) {
      map.put(c, map.getOrDefault(c, 0) + 1);
  }
  ```

- Iterate over keys/entries:
  ```java
  for (Map.Entry<Character, Integer> entry : map.entrySet()) {
      char key = entry.getKey();
      int value = entry.getValue();
  }
  ```

### 2. Implement Frequency-Based Functions (45–60 min)

Write these as separate methods:

1. **Character frequency in a string**
   ```java
   Map<Character, Integer> charFrequency(String s) { ... }
   ```

2. **Most frequent character in a string**
   ```java
   char mostFrequentChar(String s) { ... }
   ```

3. **Are two strings anagrams?** (any characters, not just a–z)
   ```java
   boolean isAnagram(String s, String t) { ... }
   ```
   - Use `Map<Character, Integer>` or two frequency arrays if only lowercase.

### 3. LeetCode Practice (45–60 min)

1. **Valid Anagram** (`#242`, Easy)
   - Use exactly your `isAnagram` approach.
   - Time complexity: O(n).

2. **First Unique Character in a String** (`#387`, Easy)
   - Use HashMap or int[26] to count.
   - Then second pass to find first with count 1.

**Reflection (10–15 min)**  
For each problem, explicitly state:
- Why HashMap is a good fit.
- What the time and space complexities are.

---

## Day 2 – HashSet & Duplicate/Uniqueness Problems

**Goal:** Learn when and how to use HashSet to track seen elements.

### 1. HashSet Basics (30–45 min)

Practice:

```java
Set<Integer> set = new HashSet<>();
set.add(10);
boolean has10 = set.contains(10);
set.remove(10);
```

- Key idea: membership check in O(1) average.
- Typical uses:
  - Detect duplicates.
  - Check if element has been seen before.
  - Store visited nodes/indices.

### 2. Implement Set-Based Functions (45–60 min)

1. **Contains duplicate? (manual version)**
   ```java
   boolean containsDuplicate(int[] nums) { ... }
   ```
   - Loop through array, if `set.contains(num)` → true.
   - Else add to set.

2. **Remove duplicates from an array (return new length)**
   - You can:
     - Use a HashSet and create a new array with unique elements.
   ```java
   int[] removeDuplicates(int[] nums) { ... }
   ```

3. **Check if a string has all unique characters**
   ```java
   boolean allUniqueChars(String s) { ... }
   ```

### 3. LeetCode Practice (45–60 min)

1. **Contains Duplicate** (`#217`, Easy)
   - Use HashSet; it’s basically the same as your practice function.

2. **Intersection of Two Arrays** (`#349`, Easy)
   - Put all elements of first array into a set.
   - Iterate second array; if in set, add to result set.

**Stretch:**  
3. **Happy Number** (`#202`, Easy/Medium)
   - Use HashSet to detect cycles in sums-of-squares process.

**Reflection (10–15 min)**  
Compare HashMap vs HashSet:
- When do you need counts/values (Map)?
- When do you only care about existence (Set)?

---

## Day 3 – Combining HashMap with Arrays/Strings

**Goal:** Solve more complex problems using Map for grouping/relationships.

### 1. Concept: Mapping Keys to Groups (30–45 min)

Understand pattern:
- Key → List of values:
  ```java
  Map<String, List<String>> map = new HashMap<>();
  map.putIfAbsent(key, new ArrayList<>());
  map.get(key).add(value);
  ```

Use cases:
- Grouping anagrams.
- Group by some “signature” (pattern, category).

### 2. Implement Grouping Functions (45–60 min)

1. **Group words by their length**
   ```java
   Map<Integer, List<String>> groupByLength(String[] words) { ... }
   ```

2. **Group strings by sorted characters** (basis of anagrams problem)
   ```java
   Map<String, List<String>> groupBySortedChars(String[] strs) { ... }
   ```
   - For each string, sort the chars to form a key: `char[] -> Arrays.sort -> new String(chars)`.

### 3. LeetCode Practice (60–90 min)

1. **Group Anagrams** (`#49`, Medium)
   - Use the sorted-string trick:
     - key = sorted characters
     - value = list of words

2. **Two Sum** (`#1`, Easy; quick revision)
   - Solve in <10–15 minutes using HashMap.

If time:
3. Re-implement **Valid Anagram** (`#242`) or **First Unique Character** (`#387`) from memory.

**Reflection (10–15 min)**  
Ask:
- How did using a “signature” (sorted string) as a key simplify the problem?
- Could there be an alternative representation (like char frequency array)?

---

## Day 4 – Two Pointers Consolidation

**Goal:** Strengthen the two-pointer pattern and apply it in new contexts.

### 1. Two Pointers Review (20–30 min)

On paper or notes, outline algorithms for:

- **Checking palindrome** (string).
- **Merging two sorted arrays**.
- **Move zeroes** (from Week 1).

Write high-level logic (not full code), focusing on:
- Pointers initialization.
- How/when they move.
- Stopping conditions.

### 2. Implement New Two-Pointer Problems (45–60 min)

1. **Remove Element (in-place) style**
   ```java
   int removeElement(int[] nums, int val) {
       int k = 0; // index to place next kept element
       for (int i = 0; i < nums.length; i++) {
           if (nums[i] != val) {
               nums[k] = nums[i];
               k++;
           }
       }
       return k;
   }
   ```
   - This is the core idea of LeetCode `#27`.

2. **Sorted Two-Sum (two-pointer version)**
   ```java
   int[] twoSumSorted(int[] nums, int target) { ... }
   ```
   - Assume `nums` is sorted.
   - Use left/right pointers; move them based on sum.

### 3. LeetCode Practice (60–90 min)

1. **Move Zeroes** (`#283`, Easy, again)
   - Implement quickly; aim to finish within 15–20 minutes.

2. **Valid Palindrome** (`#125`, Easy, again if needed)
   - Practice skipping non-alphanumeric characters properly.

3. **Two Sum II – Input Array Is Sorted** (`#167`, Easy)
   - Direct application of the sorted two-pointer idea.

**Reflection (10–15 min)**  
For each problem, explicitly write:
- Is this **hash** pattern or **two-pointer** pattern?
- Why did you choose that over the other?

---

## Day 5 – Sliding Window, Part 1 (Fixed Window & Basics)

**Goal:** Get comfortable with sliding window on arrays and strings.

### 1. Fixed-Size Sliding Window (30–45 min)

Revisit and/or implement:

1. **Max sum of subarray of size k** (if not done last week)
   ```java
   int maxSumSubarrayOfSizeK(int[] nums, int k) { ... }
   ```
   - First window: sum of first k elements.
   - Then slide: remove `nums[left]`, add `nums[right]`.

2. **Average of all subarrays of size k**
   ```java
   double[] averageSubarrayOfSizeK(int[] nums, int k) { ... }
   ```

### 2. Variable-Size Sliding Window Concept (30–45 min)

Understand pattern (restate for yourself):

```java
int left = 0;
for (int right = 0; right < s.length(); right++) {
    // include s.charAt(right) in window

    while (windowIsInvalid) {
        // exclude s.charAt(left) from window
        left++;
    }

    // now [left, right] is valid, maybe update best answer
}
```

Typical conditions:
- No more than K distinct chars.
- No repeated char.
- Sum / length constraints.

### 3. LeetCode Practice (60–90 min)

1. **Longest Substring Without Repeating Characters** (`#3`, Medium, again)
   - This time:
     - Start from scratch.
     - Try to solve in <40 minutes.
     - Use HashMap/array to track last position of each char.

2. **Minimum Size Subarray Sum** (`#209`, Medium)
   - Given target and array, find minimal length of subarray with sum ≥ target.
   - Use variable sliding window:
     - Expand right; add to sum.
     - While sum ≥ target, update answer and shrink from left.

**Reflection (10–15 min)**  
- Write both window conditions in words:
  - For `#3`: “window has all unique characters”.
  - For `#209`: “window sum is at least target”.

---

## Day 6 – Sliding Window, Part 2 (Frequency + Window)

**Goal:** Combine sliding window with HashMap/frequency arrays.

### 1. Sliding Window with Frequencies (30–45 min)

Understand this generic setup for strings:

- You maintain two frequency maps/arrays:
  - `need` – frequencies of chars you need.
  - `window` – frequencies of chars currently in window.

Example template:

```java
Map<Character, Integer> need = new HashMap<>();
Map<Character, Integer> window = new HashMap<>();
int left = 0, right = 0;
int valid = 0; // how many characters have correct count

while (right < s.length()) {
    char c = s.charAt(right);
    right++;

    // update window counts and valid

    while (windowTooBigOrValidCondition) {
        char d = s.charAt(left);
        left++;

        // update window counts and valid
    }
}
```

### 2. LeetCode Practice – Sliding Window + Counts (75–105 min)

1. **Permutation in String** (`#567`, Medium)
   - Check if `s2` contains a permutation of `s1`.
   - Use two freq arrays of size 26 (or Map).
   - Sliding window on `s2` of size `s1.length()`.

2. **Find All Anagrams in a String** (`#438`, Medium, optional but very similar)
   - Repeated applications of anagram check using window of fixed size.

If you have time or want variety:
3. Re-solve **Minimum Size Subarray Sum** (`#209`) or `#3` again.

**Reflection (10–15 min)**  
- How did you manage frequencies?
- Did you use arrays (for lowercase letters) or maps?
- Which approach felt simpler?

---

## Day 7 – Review, Mixed Practice, and Pattern Recognition

**Goal:** Consolidate Hash + Window + Two-Pointer skills and recognize patterns.

### 1. Quick Concept Review (30–45 min)

Without coding, answer in a notebook:

- For each pattern, describe in 2–3 sentences:
  - **HashMap frequency counting**
  - **HashSet for uniqueness**
  - **Two pointers (sorted array / palindrome)**
  - **Sliding window**
- For each, write down 1–2 LeetCode problems where you’ve used it.

### 2. Re-solve Selected Problems (60–90 min)

Pick at least 3, and try to solve each in **<30 minutes**:

- Hash-based:
  - `#1 Two Sum`
  - `#242 Valid Anagram`
  - `#387 First Unique Character in a String`
  - `#217 Contains Duplicate`
- Two-pointers / Sliding window:
  - `#3 Longest Substring Without Repeating Characters`
  - `#209 Minimum Size Subarray Sum`
  - `#167 Two Sum II – Input Array Is Sorted`

Do not look at old code initially. After you finish, compare with:
- Your previous solution (if saved).
- Top-voted/official solutions for alternative patterns.

### 3. Light Stretch (Optional, 30–45 min)

Pick **one** slightly more challenging or new problem to peek into:

- `#424 Longest Repeating Character Replacement` (sliding window, string)
- `#76 Minimum Window Substring` (advanced sliding window, stretch – just read and think, even partial attempt is useful)

You don’t have to fully solve these yet; getting exposed to the pattern is enough.

---

## How to Use Week 2

- Aim daily for:
  - One short **concept/theory** block.
  - 1–3 LeetCode problems (small to medium).
  - 10–15 minutes reflection (pattern, complexity, mistakes).
- Keep your **pattern notebook** updated:
  - Problem name, pattern used, key idea, time/space.

If you want, next I can:
- Build a **Week 3 daily plan** (Linked Lists, Stacks, Queues, fast/slow pointers), or  
- Provide **Java template code snippets** for sliding window and hashmap-based frequency problems.
