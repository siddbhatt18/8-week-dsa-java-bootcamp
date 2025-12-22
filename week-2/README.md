**Week 2 Focus:**  
- Get comfortable with `HashMap` and `HashSet`  
- Practice frequency counting and “seen so far” logic  
- Deepen sliding window (variable‑size)  
- Practice reading constraints and designing from scratch

Assume ~2–3 hours/day. Adjust as needed; the important part is thinking *before* coding.

---

## Day 1 – HashMap & HashSet Fundamentals

### 1. Quick Warm‑up (15–20 min)
From Week 1, briefly:
- Re‑write from memory a simple method:  
  `int maxSubArray(int[] nums)` (Kadane’s).  
- Don’t worry if it’s not perfect; just wake up your “problem‑solving” mode.

### 2. Concept Study: HashMap & HashSet (30–40 min)

**a) HashMap Basics**
- Maps keys to values. In Java:
  ```java
  Map<String, Integer> map = new HashMap<>();
  map.put("apple", 3);
  int count = map.get("apple");    // 3
  boolean hasBanana = map.containsKey("banana"); // false
  map.remove("apple");
  ```
- Operations you must know:
  - `put(key, value)`
  - `get(key)` (and what happens if key not present → returns `null` for objects)
  - `containsKey(key)`
  - `getOrDefault(key, defaultValue)`

**b) HashSet Basics**
- Stores unique values only:
  ```java
  Set<Integer> set = new HashSet<>();
  set.add(5);
  set.contains(5); // true
  set.remove(5);
  ```
- Good for checking membership: “have I seen this element before?”

### 3. Coding Exercises: Map & Set (45–60 min)

Create `Week2Day1.java` with a `main` method.

1. **Count Word Frequencies**
   - Method: `Map<String, Integer> wordCount(String[] words)`
   - For each word, increase its count in a `HashMap`.
   - Steps:
     - Initialize `HashMap<String, Integer> map = new HashMap<>();`
     - Loop through `words`:
       - If `map.containsKey(word)` then increment.
       - Else put with value 1.
   - Print the map in `main` for a sample array like `{"apple","banana","apple","orange","banana","apple"}`.

2. **Find First Repeated Integer**
   - Method: `Integer firstRepeated(int[] nums)`  
     Return the *first* number that appears twice when scanning from left to right, or `null` if none.
   - Use a `HashSet<Integer>`:
     - For each number:
       - If in set → return it.
       - Else add to set.
   - Discuss complexity in a comment.

**Think, don’t just type:**
- Why is this O(n)? What would a naive solution look like (O(n²))?

### 4. Short Written Exercise (10–15 min)
On paper, answer:
- Difference between `HashMap` and `HashSet` in your own words.
- Name at least 3 situations where you might want to use a map.

---

## Day 2 – Contains Duplicate & Frequency Patterns

### 1. Quick Review (10–15 min)
From memory:
- Sketch code (even in pseudo‑Java) for `firstRepeated(int[] nums)`.
- Confirm you use `HashSet` and not an array.

### 2. LeetCode: Contains Duplicate (Easy) (45–60 min)

**Problem:** Given an array of integers, check if any value appears at least twice.

1. **Think First (10–15 min)**
   - Brute force? Nested loops, O(n²).
   - Can a set help?
     - If you insert as you go, the moment you see a duplicate → return true.

2. **Implement with HashSet**
   - Steps:
     - Create `HashSet<Integer>`.
     - Loop over `nums`:
       - If `set.contains(num)` → return true.
       - Else `set.add(num)`.
     - End of loop → return false.

3. **Complexity Comment**
   - Time: O(n) average, Space: O(n).

4. **Optional Variation**
   - Also solve it by **sorting** and checking neighbors (no set).
   - Complexity: O(n log n).

### 3. Concept: Frequency Counting Patterns (20–30 min)

Learn this template:

```java
Map<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray()) {
    freq.put(c, freq.getOrDefault(c, 0) + 1);
}
```

- Use `getOrDefault` to simplify code.
- Realize this pattern appears in anagrams, character counts, etc.

### 4. Coding: Character Frequency (30–40 min)

In `Week2Day2.java`:

1. **Char Frequency in a String**
   - Method: `Map<Character, Integer> charFrequency(String s)`
   - Implement using `toCharArray()` and `getOrDefault`.

2. **Most Frequent Character**
   - Method: `char mostFrequentChar(String s)`
   - Use your `charFrequency` method, then:
     - Track the character with max frequency.
   - Handle empty string by returning something like `'\0'` or throwing exception (document choice in a comment).

### 5. Reflection (10–15 min)
Write:
- Explain how `HashMap` helps you avoid nested loops in frequency problems.
- Which is easier for you right now: arrays or hash maps? Why?

---

## Day 3 – Valid Anagram & Array vs Map Counting

### 1. Quick Review (10–15 min)
- Re‑implement from memory in scratch file: `charFrequency(String s)`.
- Try to write it in one go without hesitating too much; correct later.

### 2. LeetCode: Valid Anagram (Easy) (45–60 min)

**Problem:** Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`.

1. **Think First (10–15 min):**
   - What’s an anagram? Same letters, same counts.
   - Approaches:
     - Sort both strings and compare → O(n log n).
     - Count frequencies of each letter and compare maps/arrays → O(n).

2. **Approach 1 – Sort**
   - Convert to char arrays, sort both, compare.

3. **Approach 2 – HashMap or int[26]**
   - If strings contain only lowercase a–z, use `int[26]`.
     - For each char in `s`, increment count.
     - For each char in `t`, decrement count.
     - Check if all are zero.
   - If general unicode, use `HashMap<Character,Integer>`.

4. **After Solving:**
   - In notes, compare:
     - Sort vs count approach: trade‑offs?
     - Which is simpler to implement? Faster?

### 3. Concept: When to Use Array vs HashMap for Counting (20–30 min)

Rules of thumb:
- If characters are limited (e.g., lowercase letters `a–z`): use `int[26]`.
- If characters/keys can be many types (unicode, strings, etc.): use `HashMap`.

For example:
```java
int[] counts = new int[26];
int index = c - 'a';  // mapping 'a'..'z' to 0..25
counts[index]++;
```

### 4. Coding Practice: Anagram Grouping (Prep) (30–40 min)

Don’t solve full “Group Anagrams” on LeetCode yet; just:

1. **Canonical Representation by Sorting**
   - Method: `String sortString(String s)`
   - Converts `s` to char array, sorts, convert back to `String`.

2. **Map from Sorted Key to List of Words**
   - Method: `Map<String, List<String>> groupBySortedKey(String[] words)`
   - For each word:
     - Compute `key = sortString(word)`.
     - Add the word to `map.get(key)` list (create list if needed).

You don’t need to finish a polished solution, just get used to:
- Using maps where value is `List<String>`.
- Checking for key existence and initializing a new list.

### 5. Reflection (10–15 min)
Write:
- Describe in words how you could use a map to group anagrams.
- Which part of implementing `Map<String, List<String>>` felt awkward? (You’ll revisit this.)

---

## Day 4 – Two Sum II & Sorted Arrays + Two Pointers

### 1. Quick Review (10–15 min)
- Re‑write small example of `Map<String, List<String>>` usage on paper.
- Just outline logic; don’t worry about syntax perfection.

### 2. Concept: Using Sorted Data with Two Pointers (20–30 min)

Key idea:
- If array is sorted, you can often use:
  - `left = 0`, `right = n - 1`
  - Move pointers inward based on condition (sum too big or too small, etc.).

Example pattern:
```java
while (left < right) {
    int sum = nums[left] + nums[right];
    if (sum == target) { ... }
    else if (sum < target) left++;
    else right--;
}
```

### 3. LeetCode: Two Sum II – Input array is sorted (Easy) (45–60 min)

1. **Think First (10–15 min):**
   - You can solve with HashMap, but the problem *says* the array is sorted.
   - Use two pointers:
     - If sum < target → need bigger sum → `left++`.
     - If sum > target → need smaller sum → `right--`.

2. **Implement Two‑Pointer Solution**
   - Pay attention to:
     - 1‑indexed result (LC requires indices starting at 1).

3. **Compare to Two Sum I:**
   - In notebook, write:
     - Why Two Sum I preferred HashMap but Two Sum II is simpler with two pointers.

### 4. Additional Practice: Find Pair With Target Sum (Custom) (30–40 min)

In `Week2Day4.java`:

1. **Unsorted Version:**
   - Method: `boolean hasPairWithSum(int[] nums, int target)`
   - Implement using `HashSet`:
     - For each `num`:
       - If `target - num` in set → return true.
       - Else add `num`.

2. **Sorted Version (Two Pointers):**
   - Overload another method: `boolean hasPairWithSumSorted(int[] nums, int target)`
   - Assume `nums` sorted; use two pointers as in Two Sum II.

**Write a comment** comparing complexity and when you’d use each.

### 5. Reflection (10–15 min)
- In which scenarios is it worth sorting first before using two pointers?
- What extra cost does sorting introduce?

---

## Day 5 – Sliding Window: Variable‑Size Windows

### 1. Quick Review (10–15 min)
- Describe in words (no code):  
  - Fixed window (size k) vs variable window.
- Give an example of each from Week 1/2.

### 2. Concept: Variable Sliding Window (25–35 min)

Pattern for “smallest/longest subarray/substring with some property”:
- Use two pointers (`left`, `right`) for the window’s boundaries.
- Expand `right` step by step, update your data structure (map, count, etc.).
- While the window is **invalid** or **too big**, move `left` to shrink it and update your structure.
- Often uses a `HashMap` or array for counts of elements in the window.

Sketch this generic template:

```java
int left = 0;
for (int right = 0; right < s.length(); right++) {
    // include s.charAt(right) in window

    while (window is invalid) {
        // exclude s.charAt(left) from window
        left++;
    }

    // maybe update answer (max/min length, etc.)
}
```

### 3. LeetCode: Minimum Size Subarray Sum (Medium) (60–80 min)

**Problem (paraphrase it yourself first):**
- Given positive integers `nums` and an integer `target`, find the minimal length of a contiguous subarray of which the sum ≥ target.

1. **Think First (15–20 min):**
   - Brute force: check all subarrays, compute sum → O(n²) or worse.
   - But all numbers are positive → when you add more elements, the sum only increases.
   - This makes it perfect for a sliding window:
     - Expand `right` until sum ≥ target.
     - Then try to shrink from `left` while keeping sum ≥ target.

2. **Implement:**
   - Maintain `currentSum`, `minLength`.
   - For each `right`:
     - Add `nums[right]` to sum.
     - While `sum >= target`:
       - Update `minLength = min(minLength, right - left + 1)`.
       - Subtract `nums[left]`, increment `left`.

3. **Edge Cases:**
   - If no subarray found, return 0.

4. **Complexity:** O(n) time, O(1) extra space.

### 4. Small Custom Problem: Longest Subarray with Sum ≤ K (30–40 min, Thinky)

Not a direct LeetCode one, just to push your thinking.

**Problem:**
- Given an array of positive integers `nums` and an integer `k`, find the length of the *longest* subarray with sum ≤ k.

**Hints:**
- Also positive integers → sliding window works.
- Similar to min subarray, but now:
  - Expand right, and while `sum > k`, move left.
  - Track max length where sum ≤ k.

Try to:
- Think on paper first.
- Then implement `int longestSubarraySumAtMostK(int[] nums, int k)`.

### 5. Reflection (10–15 min)
On paper:
- What role does “all numbers are positive” play in sliding window problems?
- Imagine numbers could be negative too – why would this break the simple window logic?

---

## Day 6 – Longest Substring Without Repeating Characters

### 1. Quick Review (10–15 min)
- Re‑state, from memory, the logic of **Minimum Size Subarray Sum**.
- Specifically, when do you move `right` and when do you move `left`?

### 2. Concept: Sliding Window with HashMap/Set on Strings (25–35 min)

Idea:
- Process string with `right` index.
- Use `HashSet` or `HashMap<Character, Integer>` to track characters in current window.
- If you detect a duplicate or invalid condition:
  - Move `left` forward, updating your structure, until valid again.

### 3. LeetCode: Longest Substring Without Repeating Characters (Medium) (60–80 min)

1. **Understand the Problem:**
   - We want the length of the longest substring (continuous) without any repeated characters.

2. **Think Before Coding (15–20 min):**
   - Approaches:
     - Brute force: check all substrings → O(n²) or worse.
     - Sliding window:
       - `left`, `right`, and a `Set<Character>` or `Map<Character, Integer>`.
   - Basic idea with `HashSet`:
     - Move `right`, adding chars.
     - If you see a char that’s already in set:
       - Remove `s.charAt(left)` from set, `left++`, until no duplicates.

3. **Implement with HashSet First**
   - Keep track of `maxLen`.

4. **Optional Improvement (Map with Last Seen Index)**
   - Use `Map<Character, Integer>` to jump `left` more efficiently:
     - If you see `c` again at position `i`, and `lastIndex[c] >= left`, set `left = lastIndex[c] + 1`.

### 4. Short Follow‑Up Practice (20–30 min)

In `Week2Day6.java`, write:
- `int lengthOfLongestSubstringTwoDistinct(String s)` (just think/pseudo‑code if time short)
  - At most 2 distinct characters in the window.
  - Hint: use a `Map<Character, Integer>` to store counts; when `map.size() > 2`, shrink from left.

Even if you don’t fully code it, try to:
- Outline the steps in comments.
- Identify where you grow/shrink the window.

### 5. Reflection (10–15 min)
Write:
- How is this sliding window problem different from the subarray sum ones?
- What’s the same about all sliding window problems you’ve seen so far?

---

## Day 7 – Mixed Review: Hash + Windows

### 1. Concept Review (30–40 min)

Without referencing your notes initially, on paper write:

- Basic API snippets:
  - HashMap: `put`, `get`, `containsKey`, `getOrDefault`
  - HashSet: `add`, `contains`, `remove`
- Sliding window generic steps, in 4–5 bullet points.
- Two ways to check if two strings are anagrams.

Then check and correct with your notes.

### 2. Re‑implement from Memory (60–75 min)

In `Week2Review.java`, re‑implement these methods, *without* copying any previous code:

1. `boolean containsDuplicate(int[] nums)` – using `HashSet`
2. `boolean isAnagram(String s, String t)` – using counts or map
3. `int minSubArrayLen(int target, int[] nums)` – Minimum Size Subarray Sum
4. `int lengthOfLongestSubstring(String s)` – Longest Substring Without Repeating Characters

For each:
- Add a comment with time and space complexity.
- Add a short 1–2 line *intuition* comment above the method: e.g.  
  `// Use a sliding window and HashSet to keep substring without duplicates.`

### 3. LeetCode Mini‑Session (60–75 min)

Try to solve (or re‑solve) these in one sitting, from a blank editor on LeetCode:

1. **Two Sum (Easy)** – Use HashMap without referring to old code.
2. **Valid Anagram (Easy)** – Try counts approach only.
3. **Contains Duplicate (Easy)** – Using HashSet.

For each:
- Spend at least 10–15 minutes thinking before you look at any solution tab.
- After solving, read one top solution, and note one thing you’d improve in yours (naming, structure, etc.).

### 4. End‑of‑Week Reflection (15–20 min)

In your notebook, write:

1. **Patterns List**  
   Make a small “cheat sheet” like:

   - Arrays + HashSet → duplicates, existence checks.
   - Strings + HashMap → frequencies, sliding window on characters.
   - Sliding window (+ map or set) → substring/subarray problems with local constraints.
   - Two pointers on sorted arrays → sum/comparison‑based problems.

2. **Confidence Rating (1–5)**  
   Rate your comfort on:
   - HashMap/HashSet usage
   - Frequency counting
   - Sliding window
   - Two pointers

3. **Questions for Next Week**  
   Write 3–5 questions you still have, e.g.:
   - “How do I choose between HashMap and array for counts?”
   - “When sliding window breaks (e.g., with negatives), what’s next?”
   - “How to get better at designing from scratch quickly?”

You’ll use these questions to guide Week 3 and beyond.

---

If you want, I can next turn **Week 3** into a similar day‑by‑day plan (linked lists + stacks/queues), building directly on what you’ve just practiced.
