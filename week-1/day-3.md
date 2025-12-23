### Day 3 – Strings, StringBuilder, and Your First Two‑Pointer String Problem

**Main outcomes for today**

By the end of Day 3, you should be able to:

1. Work comfortably with `String` and `char` in Java.
2. Use `StringBuilder` to build/transform strings efficiently.
3. Understand and implement the **two‑pointer pattern** on strings (Valid Palindrome).
4. Solve several string/array problems of increasing difficulty that reinforce:
   - Scanning
   - Filtering
   - Building new outputs
   - Using pointers at both ends

Plan for ~2–3 hours. If you have less time, keep the order but reduce the number of practice questions.

---

## Part 1 – Warm‑Up: Arrays & HashMap Recall (15–20 min)

Goal: Keep previous days’ skills “warm” before adding new topics.

In a file `Day3Warmup.java`, from memory, re‑implement:

1. `sumArray(int[] nums)`
2. `maxInArray(int[] nums)`
3. `twoSumHashMap(int[] nums, int target)` (optimized version from Day 2)

Skeleton:

```java
import java.util.*;

public class Day3Warmup {

    public static int sumArray(int[] nums) {
        // TODO
    }

    public static int maxInArray(int[] nums) {
        // TODO
    }

    public static int[] twoSumHashMap(int[] nums, int target) {
        // TODO
    }

    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4};
        System.out.println(sumArray(a));   // 10
        System.out.println(maxInArray(a)); // 4

        int[] nums = {2, 7, 11, 15};
        System.out.println(Arrays.toString(twoSumHashMap(nums, 9))); // [0,1] or [1,0]
    }
}
```

Focus:

- Get them correct without looking at old code.
- If you’re stuck on `twoSumHashMap`, write the **idea in words** first:
  - “Scan once; for each value, check if complement already in map; if not, put current value and index.”

---

## Part 2 – Strings Fundamentals in Java (20–30 min)

### 2.1 Key Concepts

1. **`String` is immutable**
   - Once created, you can’t change it. Operations like `s + "x"` create new strings.
   - Repeated concatenation in a loop is inefficient.

2. **Common `String` methods**
   - `int length()`
   - `char charAt(int index)`
   - `String substring(int beginIndex, int endIndex)` (endIndex is exclusive)
   - `char[] toCharArray()`
   - `toLowerCase()`, `toUpperCase()`
   - `trim()`, `split(String regex)` (just awareness for now)

3. **Character utilities**
   - `Character.isLetterOrDigit(c)`
   - `Character.isLowerCase(c)`, `isUpperCase(c)`
   - `Character.toLowerCase(c)`, `toUpperCase(c)`

4. **StringBuilder**
   - Mutable sequence of characters; good for building strings in loops.

   Example:

   ```java
   StringBuilder sb = new StringBuilder();
   sb.append('a');
   sb.append("hello");
   String result = sb.toString();
   ```

---

### 2.2 Quick Hands‑On: Tiny Experiments (10–15 min)

In `Day3StringsIntro.java`, run small tests:

```java
public class Day3StringsIntro {
    public static void main(String[] args) {
        String s = "Hello";
        System.out.println(s.length());        // 5
        System.out.println(s.charAt(1));       // 'e'
        System.out.println(s.substring(1, 4)); // "ell"

        char c = 'A';
        System.out.println(Character.isLetterOrDigit(c)); // true
        System.out.println(Character.toLowerCase(c));     // 'a'

        StringBuilder sb = new StringBuilder();
        sb.append('J');
        sb.append("ava");
        System.out.println(sb.toString()); // "Java"
    }
}
```

Make sure you’re comfortable:

- Indexing into a string with `charAt`.
- Using `StringBuilder` to append in a loop.

---

## Part 3 – Core String Practice Functions (40–50 min)

Now you’ll implement some classic string operations using arrays and `StringBuilder`.

Create `Day3StringsPractice.java`.

### 3.1 Reverse String (Return New String)

```java
// Return a new string that is the reverse of s.
// e.g., "abc" -> "cba"
// Time: O(n), Space: O(n)
public static String reverseString(String s) {
    // Option A: use char array
    char[] arr = s.toCharArray();
    int left = 0, right = arr.length - 1;
    while (left < right) {
        char tmp = arr[left];
        arr[left] = arr[right];
        arr[right] = tmp;
        left++;
        right--;
    }
    return new String(arr);
}
```

If you’d like, first try implementing it **yourself**, then compare to this template.

---

### 3.2 Count Vowels

```java
// Count how many vowels (a, e, i, o, u, both lowercase and uppercase) are in s.
// Time: O(n), Space: O(1)
public static int countVowels(String s) {
    int count = 0;
    for (int i = 0; i < s.length(); i++) {
        char c = Character.toLowerCase(s.charAt(i));
        if (c == 'a' || c == 'e' || c == 'i' ||
            c == 'o' || c == 'u') {
            count++;
        }
    }
    return count;
}
```

Test:

```java
public static void main(String[] args) {
    System.out.println(countVowels("hello"));       // 2
    System.out.println(countVowels("AEIOUxyz"));    // 5
}
```

---

### 3.3 Remove Vowels Using StringBuilder

```java
// Return a new string with all vowels removed from s.
// Time: O(n), Space: O(n)
public static String removeVowels(String s) {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < s.length(); i++) {
        char c = Character.toLowerCase(s.charAt(i));
        if (c == 'a' || c == 'e' || c == 'i' ||
            c == 'o' || c == 'u') {
            continue;
        }
        sb.append(s.charAt(i)); // use original char to preserve case
    }
    return sb.toString();
}
```

Test:

```java
public static void main(String[] args) {
    System.out.println(removeVowels("hello"));   // "hll"
    System.out.println(removeVowels("LeetCode"));// "LtCd"
}
```

---

## Part 4 – Two‑Pointer Pattern on Strings: Valid Palindrome (50–70 min)

This is the main DSA concept of the day.

### 4.1 Understand the Problem (10–15 min, no coding first)

**Problem (LeetCode: Valid Palindrome)**

> Given a string `s`, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Examples:

- `"A man, a plan, a canal: Panama"` → true  
- `"race a car"` → false

On paper, answer:

1. **Restate:**
   - “Check if the string reads the same forward and backward when you ignore non‑letters/digits and ignore case differences.”

2. **Inputs/Outputs:**
   - Input: `String s`
   - Output: `boolean` (true if palindrome under those conditions)

3. **Brute force idea #1 (clean + check):**
   - Build a cleaned string:
     - Keep only letters/digits.
     - Convert to lowercase.
   - Then check if cleaned string is a palindrome using indices `0..n-1`.
   - Complexity: O(n) time, O(n) space.

4. **Optimized idea #2 (two pointers directly):**
   - Use two indices: `left = 0`, `right = s.length() - 1`.
   - While left < right:
     - Move left forward until it points to a letter/digit.
     - Move right backward until it points to a letter/digit.
     - Compare lowercase chars at left and right.
       - If not equal → false.
     - Move both pointers inward.
   - If loop finishes → true.
   - Complexity: O(n) time, O(1) extra space.

Both are acceptable; the two‑pointer version is more idiomatic and space‑efficient.

---

### 4.2 Implement: Clean + Check Version (Optional First Pass)

If you want a gentler step:

```java
// Simple version: clean the string, then check palindrome.
// Time: O(n), Space: O(n)
public static boolean isPalindromeClean(String s) {
    StringBuilder sb = new StringBuilder();
    // 1. Clean the string
    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        if (Character.isLetterOrDigit(c)) {
            sb.append(Character.toLowerCase(c));
        }
    }
    String cleaned = sb.toString();

    // 2. Check if cleaned is palindrome
    int left = 0, right = cleaned.length() - 1;
    while (left < right) {
        if (cleaned.charAt(left) != cleaned.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}
```

---

### 4.3 Implement: Direct Two‑Pointer Version (Main Pattern to Learn)

```java
// Optimal version: two pointers directly on original string.
// Time: O(n), Space: O(1)
public static boolean isPalindromeTwoPointers(String s) {
    int left = 0;
    int right = s.length() - 1;

    while (left < right) {
        // Move left to next alphanumeric char
        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
            left++;
        }
        // Move right to previous alphanumeric char
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
            right--;
        }

        char cLeft = Character.toLowerCase(s.charAt(left));
        char cRight = Character.toLowerCase(s.charAt(right));
        if (cLeft != cRight) {
            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

Test in `main`:

```java
public static void main(String[] args) {
    String s1 = "A man, a plan, a canal: Panama";
    String s2 = "race a car";
    String s3 = ".,";
    System.out.println(isPalindromeTwoPointers(s1)); // true
    System.out.println(isPalindromeTwoPointers(s2)); // false
    System.out.println(isPalindromeTwoPointers(s3)); // true (no alnum characters -> empty string -> palindrome)
}
```

### 4.4 Mental checkpoint

In your notebook, explain in your own words:

- “What is the **two‑pointer** idea here?”
  - Example answer: “Start one pointer at each end of the string, move inward, skipping irrelevant characters, and compare corresponding characters.”

This same pattern will appear in:
- Reversing/processing arrays from both ends.
- Many string problems (e.g., palindrome, valid parentheses variants).

---

## Part 5 – Additional Practice Questions (Increasing Difficulty)

Use these to apply and expand your DSA skills with arrays and strings.

### Level 1 – Direct String Handling

#### Q1. `toLowerCaseManual(String s)`

Implement a method that converts a string to lowercase **without** using `s.toLowerCase()` (use `Character.toLowerCase` per char):

```java
public static String toLowerCaseManual(String s) {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        sb.append(Character.toLowerCase(c));
    }
    return sb.toString();
}
```

(This is easy, but good for `StringBuilder` fluency.)

---

#### Q2. `removeNonAlnum(String s)`

Return a new string containing only alphanumeric characters from `s`:

```java
public static String removeNonAlnum(String s) {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        if (Character.isLetterOrDigit(c)) {
            sb.append(c);
        }
    }
    return sb.toString();
}
```

Extend by:
- Also converting to lowercase if you want.

---

### Level 2 – Logic + Two Pointers/Indices

#### Q3. Check if String is Palindrome (Simple Version)

Ignore case but do **not** ignore non‑alphanumeric characters.

```java
// Return true if s is a palindrome ignoring case (but counting all characters).
public static boolean isSimplePalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        char cLeft = Character.toLowerCase(s.charAt(left));
        char cRight = Character.toLowerCase(s.charAt(right));
        if (cLeft != cRight) return false;
        left++;
        right--;
    }
    return true;
}
```

This reinforces the basic two‑pointer form.

---

#### Q4. Reverse Only Letters (LeetCode style, but do it locally)

**Problem idea:**

> Given a string `s`, reverse only the letters and keep non‑letter characters in their original positions.

Example:
- Input: `"a-bC-dEf-ghIj"`
- Output: `"j-Ih-gfE-dCba"`

Approach:

- Convert to char array for easier modification.
- Use two pointers `left` and `right`.
  - Move `left` forward until `Character.isLetter(arr[left])` is true.
  - Move `right` backward until `Character.isLetter(arr[right])` is true.
  - Swap the letters.
  - Continue while `left < right`.

Skeleton:

```java
public static String reverseOnlyLetters(String s) {
    char[] arr = s.toCharArray();
    int left = 0, right = arr.length - 1;

    while (left < right) {
        if (!Character.isLetter(arr[left])) {
            left++;
        } else if (!Character.isLetter(arr[right])) {
            right--;
        } else {
            char tmp = arr[left];
            arr[left] = arr[right];
            arr[right] = tmp;
            left++;
            right--;
        }
    }
    return new String(arr);
}
```

This is an **excellent** practice of:
- Two pointers
- Skipping certain characters
- Using conditions properly.

---

### Level 3 – Stretch / Deeper Thinking

#### Q5. Longest Vowel Sequence

> Given a string `s`, return the length of the longest **contiguous substring** that contains only vowels (a, e, i, o, u, case‑insensitive).

Example:
- `"earthideaooop"` → longest vowel run is `"ideaooo"` length 7.

Approach:

- Iterate through `s`.
- If current char is vowel → increment current run length.
- Else → reset current run length to 0.
- Track a global max.

Skeleton:

```java
public static int longestVowelRun(String s) {
    int maxLen = 0;
    int currentLen = 0;
    for (int i = 0; i < s.length(); i++) {
        char c = Character.toLowerCase(s.charAt(i));
        if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') {
            currentLen++;
            if (currentLen > maxLen) {
                maxLen = currentLen;
            }
        } else {
            currentLen = 0;
        }
    }
    return maxLen;
}
```

This sneakily introduces the idea of:
- Scanning with a running “state” (similar to Kadane’s algorithm later).

---

#### Q6. Check if Two Strings are Anagrams (Pre‑HashMap Version)

Later you’ll do this with `HashMap` or arrays, but for now:

> Given two strings `s` and `t`, check if they are anagrams (contain the same characters in any order, case‑insensitive). You may assume only lowercase letters for this version.

Simple version (for lowercase only):

- If lengths differ → false.
- Use an `int[26]` array as frequency counter:
  - For each char in `s`, increment count.
  - For each char in `t`, decrement count.
- If all counts are zero at the end → anagram.

This prepares you for Week 2’s hashing/frequency problems.

---

## Part 6 – Mini Speed Drill (10–15 min)

Pick 3–4 of these functions:

- `reverseString`
- `countVowels`
- `removeVowels`
- `isSimplePalindrome`
- `isPalindromeTwoPointers` (valid palindrome with skipping)

For each:

1. Set a **5 minute timer**.
2. Re‑implement the function from scratch (in a new file or new methods).
3. Add 1–2 quick test cases.
4. Check correctness.

Aim to:

- Avoid off‑by‑one errors with `left`/`right`.
- Use `Character` helpers correctly.
- Gradually reduce time per function to **3–4 minutes** as you repeat on future days.

---

## Part 7 – Reflection (10–15 min)

In your notebook:

1. **Today I learned:**
   - 2–3 bullets about `String` and `StringBuilder`.
   - 1–2 bullets about the two‑pointer pattern.

2. **Two‑pointer summary in my own words:**
   - Write 2–3 sentences describing how and why you used it in `isPalindromeTwoPointers` and `reverseOnlyLetters`.

3. **What felt tricky:**
   - Skipping non‑alphanumeric characters?
   - Conditions in the while loops?
   - Remembering to convert to lowercase before comparing?

4. **Connection to future topics:**
   - Note that this same two‑pointer + scanning logic appears in:
     - Moving zeros in arrays.
     - Working with sorted arrays (3Sum, etc.).
     - Certain DP and greedy problems.

---

### Summary of Day 3 Practice Questions (Difficulty Ladder)

**Core guided problems**
- `reverseString(String s)`
- `countVowels(String s)`
- `removeVowels(String s)`
- `isPalindromeTwoPointers(String s)` (Valid Palindrome pattern)

**Level 1**
1. `toLowerCaseManual(String s)`
2. `removeNonAlnum(String s)`

**Level 2**
3. `isSimplePalindrome(String s)` (no ignoring non‑alnum)
4. `reverseOnlyLetters(String s)`

**Level 3 (Stretch)**
5. `longestVowelRun(String s)`
6. Simple anagram check using frequency array `int[26]`

If you’d like, next I can:

- Build a detailed **Day 4 guide** (two‑pointers on arrays, in‑place modifications like Move Zeroes), or  
- Create a compact “Week 1 daily warm‑up” (10–15 minute recurring drill) to reinforce arrays + strings + maps.
