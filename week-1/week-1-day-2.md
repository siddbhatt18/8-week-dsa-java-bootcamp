# Week 1, Day 2: Deep Dive - Time & Space Complexity Mastery + Java Collections Deep Dive

## 🎯 Learning Objectives
By the end of today, you will:
1. Master complexity analysis for nested loops, recursion, and complex patterns
2. Understand space-time tradeoffs deeply
3. Know advanced Java Collections techniques
4. Apply Big O analysis to real code patterns you'll see in LeetCode

**Time Required:** 2-3 hours

---

## 📚 Part 1: Advanced Big O Analysis (60 minutes)

### Yesterday's Recap (2 minutes)

Quick review - what's the complexity?
```java
// 1. This?
for (int i = 0; i < n; i++) { }

// 2. This?
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) { }
}

// 3. This?
HashMap<Integer, Integer> map = new HashMap<>();
map.put(key, value);
```

<details>
<summary>Answers</summary>

1. O(n) - single loop
2. O(n²) - nested loops
3. O(1) - hash map operations average case
</details>

---

### Pattern 1: Analyzing Non-Standard Loops

**Not all nested loops are O(n²)!**

```java
// Example 1: j starts at i (not 0)
public void printPairs(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        for (int j = i; j < arr.length; j++) {
            System.out.println(arr[i] + ", " + arr[j]);
        }
    }
}
```

**Analysis:**
- When i=0: inner loop runs n times
- When i=1: inner loop runs n-1 times
- When i=2: inner loop runs n-2 times
- ...
- When i=n-1: inner loop runs 1 time

**Total:** n + (n-1) + (n-2) + ... + 1 = n(n+1)/2 = (n² + n)/2

**Drop constants and non-dominant terms:** O(n²)

**Key Insight:** Still quadratic, but runs about half as many times as a true n² loop.

---

```java
// Example 2: j grows exponentially
public void mystery(int n) {
    for (int i = 1; i < n; i++) {
        for (int j = 1; j < n; j = j * 2) {
            System.out.println(i + ", " + j);
        }
    }
}
```

**Analysis:**
- Outer loop: runs n times → O(n)
- Inner loop: j doubles each time (1, 2, 4, 8, 16...)
  - How many times does j double before exceeding n?
  - 2^k = n → k = log₂(n)
  - Inner loop: O(log n)

**Total:** O(n) × O(log n) = **O(n log n)**

---

```java
// Example 3: Both variables grow together
public void mystery(int n) {
    for (int i = 1; i < n; i = i * 2) {
        for (int j = 1; j < n; j = j * 2) {
            System.out.println(i + ", " + j);
        }
    }
}
```

**Analysis:**
- Outer loop: O(log n) - i doubles
- Inner loop: O(log n) - j doubles
- **Total:** O(log n) × O(log n) = **O(log² n)**

---

### Pattern 2: Recursion Complexity

**Rule of thumb:**
- **Time complexity** = (Number of recursive calls) × (Work per call)
- **Space complexity** = Maximum depth of call stack

```java
// Example 1: Linear recursion
public int factorial(int n) {
    if (n <= 1) return 1;           // Base case: O(1)
    return n * factorial(n - 1);    // Recursive call
}
```

**Time Analysis:**
- factorial(n) calls factorial(n-1) calls factorial(n-2) ... calls factorial(1)
- Total calls: n
- Work per call: O(1) (just multiplication)
- **Time:** O(n)

**Space Analysis:**
- Call stack: factorial(5) → factorial(4) → factorial(3) → factorial(2) → factorial(1)
- Maximum depth: n
- **Space:** O(n)

---

```java
// Example 2: Binary recursion (tree structure)
public int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n-1) + fibonacci(n-2);
}
```

**Visual call tree for fib(5):**
```
                    fib(5)
                   /      \
              fib(4)      fib(3)
             /     \      /     \
        fib(3)   fib(2) fib(2) fib(1)
        /   \     /  \   /  \
    fib(2) fib(1) f(1) f(0) f(1) f(0)
    /  \
  f(1) f(0)
```

**Time Analysis:**
- Each call makes 2 recursive calls
- Tree depth: n
- Nodes at each level: 2^0, 2^1, 2^2, ..., 2^n
- Total nodes: 2^(n+1) - 1 ≈ 2^n
- **Time:** O(2^n) - EXPONENTIAL! 💀

**Space Analysis:**
- Only ONE path is active at a time (not all branches simultaneously)
- Maximum depth: n (left-most path)
- **Space:** O(n)

**Key Insight:** Time ≠ Space in recursion!

---

```java
// Example 3: Divide and conquer (binary search)
public int binarySearch(int[] arr, int target, int left, int right) {
    if (left > right) return -1;
    
    int mid = left + (right - left) / 2;
    if (arr[mid] == target) return mid;
    
    if (arr[mid] > target)
        return binarySearch(arr, target, left, mid - 1);
    else
        return binarySearch(arr, target, mid + 1, right);
}
```

**Analysis:**
- Each call eliminates half the array
- T(n) = T(n/2) + O(1)
- Recurrence: n → n/2 → n/4 → ... → 1
- Number of divisions: log₂(n)
- **Time:** O(log n)
- **Space:** O(log n) - call stack depth

---

### 🧠 Practice: Analyze These Recursions

**Exercise 1:**
```java
public void printN(int n) {
    if (n <= 0) return;
    System.out.println(n);
    printN(n - 1);
    printN(n - 1);
}
```

<details>
<summary>Answer</summary>

**Time:** O(2^n)
- Each call makes 2 recursive calls (binary tree)
- Similar to Fibonacci

**Space:** O(n)
- Maximum call stack depth is n (left branch)

**What it does:** Prints numbers in a binary tree pattern
</details>

---

**Exercise 2:**
```java
public int sum(int n) {
    if (n <= 0) return 0;
    return n + sum(n - 1);
}
```

<details>
<summary>Answer</summary>

**Time:** O(n)
- Makes n recursive calls
- Each call does O(1) work

**Space:** O(n)
- Call stack depth is n

**What it does:** Calculates 1+2+3+...+n
</details>

---

**Exercise 3:**
```java
public int mystery(int n) {
    if (n <= 1) return 1;
    return mystery(n / 2) + mystery(n / 2);
}
```

<details>
<summary>Answer</summary>

**Time:** O(n)
- Though we divide by 2, we make TWO calls
- T(n) = 2T(n/2) + O(1)
- Tree has log(n) levels, but each level does 2^i work
- Total: 2^0 + 2^1 + 2^2 + ... + 2^log(n) = n

**Space:** O(log n)
- Maximum depth is log(n)

**Note:** If we cached results, this would be O(log n) time!
</details>

---

## 📚 Part 2: Space-Time Tradeoffs (45 minutes)

### The Golden Rule

> "You can often trade space for time, but rarely time for space."

### Classic Tradeoff Example: Two Sum Problem

**Problem:** Find two numbers in array that sum to target.

**Approach 1: Brute Force (No extra space)**
```java
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) {
                return new int[]{i, j};
            }
        }
    }
    return new int[]{};
}
```
- **Time:** O(n²) - nested loops
- **Space:** O(1) - no extra data structures
- **Tradeoff:** Slow but memory-efficient

---

**Approach 2: HashMap Optimization (Using space)**
```java
public int[] twoSum(int[] nums, int target) {
    HashMap<Integer, Integer> map = new HashMap<>();
    
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}
```
- **Time:** O(n) - single loop, O(1) lookups
- **Space:** O(n) - HashMap can store all elements
- **Tradeoff:** Fast but uses more memory

**Improvement:** 100x faster for n=1000 (1,000,000 vs 1,000 operations)

---

### When to Make the Tradeoff?

| Use Time-Optimal (more space) | Use Space-Optimal (more time) |
|-------------------------------|-------------------------------|
| Large datasets | Memory-constrained systems |
| Frequent queries | One-time operations |
| Real-time requirements | Small datasets |
| Interviews (usually) | Embedded systems |

**Interview tip:** Always mention the tradeoff!
> "I'm using a HashMap here, which takes O(n) space but improves time from O(n²) to O(n). In a memory-constrained environment, we could use the two-pointer approach if we're allowed to sort."

---

### Common Space-Time Patterns

**Pattern 1: Caching (Memoization)**

```java
// WITHOUT memoization: O(2^n)
public int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}

// WITH memoization: O(n) time, O(n) space
HashMap<Integer, Integer> memo = new HashMap<>();

public int fibMemo(int n) {
    if (n <= 1) return n;
    if (memo.containsKey(n)) return memo.get(n);
    
    int result = fibMemo(n-1) + fibMemo(n-2);
    memo.put(n, result);
    return result;
}
```

**Impact:** fib(40) runs in milliseconds instead of minutes!

---

**Pattern 2: Preprocessing**

```java
// Problem: Answer many range sum queries on same array

// Approach 1: Calculate each time
// Query time: O(n), Space: O(1)
public int rangeSum(int[] arr, int left, int right) {
    int sum = 0;
    for (int i = left; i <= right; i++) {
        sum += arr[i];
    }
    return sum;
}

// Approach 2: Prefix sum array
// Preprocessing: O(n), Query time: O(1), Space: O(n)
class RangeSumQuery {
    int[] prefixSum;
    
    public RangeSumQuery(int[] arr) {
        prefixSum = new int[arr.length + 1];
        for (int i = 0; i < arr.length; i++) {
            prefixSum[i + 1] = prefixSum[i] + arr[i];
        }
    }
    
    public int rangeSum(int left, int right) {
        return prefixSum[right + 1] - prefixSum[left];
    }
}
```

**Tradeoff:** If you query 1000 times, preprocessing wins!

---

## 📚 Part 3: Java Collections - Advanced Techniques (45 minutes)

### HashMap Deep Dive

**The Most Important Collection for LeetCode**

```java
HashMap<Integer, Integer> map = new HashMap<>();

// 1. Basic operations (review)
map.put(1, 100);              // Add/Update: O(1)
map.get(1);                   // Retrieve: O(1)
map.containsKey(1);           // Check key: O(1)
map.containsValue(100);       // Check value: O(n) - avoid!
map.remove(1);                // Delete: O(1)

// 2. Default value pattern (CRITICAL!)
// BAD - verbose
if (map.containsKey(key)) {
    map.put(key, map.get(key) + 1);
} else {
    map.put(key, 1);
}

// GOOD - use getOrDefault
map.put(key, map.getOrDefault(key, 0) + 1);

// 3. Iteration patterns
for (Integer key : map.keySet()) {
    System.out.println(key + ": " + map.get(key));
}

for (Integer value : map.values()) {
    System.out.println(value);
}

for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

// 4. Advanced: compute methods (Java 8+)
map.compute(key, (k, v) -> (v == null) ? 1 : v + 1);
map.computeIfAbsent(key, k -> new ArrayList<>());
map.merge(key, 1, Integer::sum);  // Increment or initialize
```

---

### HashMap Common Patterns

**Pattern 1: Frequency Counter**
```java
// Count character frequencies in string
public HashMap<Character, Integer> countChars(String s) {
    HashMap<Character, Integer> freq = new HashMap<>();
    for (char c : s.toCharArray()) {
        freq.put(c, freq.getOrDefault(c, 0) + 1);
    }
    return freq;
}
```

**Pattern 2: Group By Key**
```java
// Group strings by length
public HashMap<Integer, List<String>> groupByLength(String[] words) {
    HashMap<Integer, List<String>> groups = new HashMap<>();
    for (String word : words) {
        int len = word.length();
        groups.computeIfAbsent(len, k -> new ArrayList<>()).add(word);
    }
    return groups;
}
```

**Pattern 3: Two Sum Lookup**
```java
// Find complement in O(1)
public int[] twoSum(int[] nums, int target) {
    HashMap<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        if (map.containsKey(target - nums[i])) {
            return new int[]{map.get(target - nums[i]), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}
```

---

### HashSet Advanced

```java
HashSet<Integer> set = new HashSet<>();

// 1. Duplicate detection (instant)
public boolean hasDuplicates(int[] arr) {
    HashSet<Integer> seen = new HashSet<>();
    for (int num : arr) {
        if (!seen.add(num)) return true;  // add() returns false if exists!
    }
    return false;
}

// 2. Set operations
HashSet<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3, 4));
HashSet<Integer> set2 = new HashSet<>(Arrays.asList(3, 4, 5, 6));

// Union
HashSet<Integer> union = new HashSet<>(set1);
union.addAll(set2);  // {1, 2, 3, 4, 5, 6}

// Intersection
HashSet<Integer> intersection = new HashSet<>(set1);
intersection.retainAll(set2);  // {3, 4}

// Difference
HashSet<Integer> difference = new HashSet<>(set1);
difference.removeAll(set2);  // {1, 2}
```

---

### ArrayList vs LinkedList

**When to use which?**

```java
// ArrayList - backed by dynamic array
ArrayList<Integer> arrayList = new ArrayList<>();
arrayList.get(100);      // O(1) - random access
arrayList.add(value);    // O(1) amortized - append
arrayList.add(0, value); // O(n) - insert at beginning
arrayList.remove(0);     // O(n) - remove from beginning

// LinkedList - doubly-linked nodes
LinkedList<Integer> linkedList = new LinkedList<>();
linkedList.get(100);       // O(n) - must traverse
linkedList.addFirst(value); // O(1) - insert at beginning
linkedList.addLast(value);  // O(1) - append
linkedList.removeFirst();   // O(1) - remove from beginning
```

**Decision matrix:**
| Operation | ArrayList | LinkedList | Winner |
|-----------|-----------|------------|--------|
| Random access | O(1) | O(n) | ArrayList |
| Add/remove at end | O(1) | O(1) | Tie |
| Add/remove at beginning | O(n) | O(1) | LinkedList |
| Memory overhead | Lower | Higher | ArrayList |

**Rule of thumb:** Use ArrayList 95% of the time. Use LinkedList only when you frequently add/remove from beginning.

---

### Stack vs Queue Implementation

```java
// STACK - Last In First Out
Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.pop();    // Returns 2 (last added)

// Better: Use Deque as stack (more flexible)
Deque<Integer> stack = new ArrayDeque<>();
stack.push(1);
stack.pop();

// QUEUE - First In First Out
Queue<Integer> queue = new LinkedList<>();
queue.offer(1);
queue.offer(2);
queue.poll();   // Returns 1 (first added)

// Better: Use ArrayDeque as queue (faster)
Deque<Integer> queue = new ArrayDeque<>();
queue.offer(1);
queue.poll();
```

**Why ArrayDeque over Stack/LinkedList?**
- Faster than Stack (no synchronization overhead)
- Faster than LinkedList (array-based = better cache locality)
- Can act as both stack AND queue

---

## 🧠 Part 4: Hands-On Complexity Analysis (30 minutes)

### Exercise Set 1: Determine Complexity

**Problem 1:**
```java
public int mystery(String s) {
    int count = 0;
    for (int i = 0; i < s.length(); i++) {
        String sub = s.substring(0, i);  // Creates new string
        count += sub.length();
    }
    return count;
}
```

<details>
<summary>Answer</summary>

**Time:** O(n²)
- Loop runs n times: O(n)
- substring() creates new string of length i: O(i)
- Total: 1 + 2 + 3 + ... + n = n(n+1)/2 = O(n²)

**Space:** O(n)
- Largest substring created is length n-1

**Hidden cost:** String operations often have hidden complexity!
</details>

---

**Problem 2:**
```java
public void mystery(int n) {
    for (int i = n; i > 0; i = i / 2) {
        for (int j = 0; j < i; j++) {
            System.out.println(j);
        }
    }
}
```

<details>
<summary>Answer</summary>

**Time:** O(n)
- Outer loop: log(n) iterations (i halves each time)
- Inner loop iterations: n + n/2 + n/4 + n/8 + ... + 1
- Geometric series: approaches 2n
- **Total:** O(n)

**Not O(n log n)!** The inner loop does LESS work each iteration.
</details>

---

**Problem 3:**
```java
public int search(int[][] matrix, int target) {
    int rows = matrix.length;
    int cols = matrix[0].length;
    
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            if (matrix[i][j] == target) {
                return i * cols + j;
            }
        }
    }
    return -1;
}
```

<details>
<summary>Answer</summary>

**Time:** O(rows × cols) or O(n×m)
- Must check every element in worst case
- Alternative notation: O(n) where n = total elements

**Space:** O(1)
- No extra data structures

**Key insight:** For 2D arrays, complexity is rows × cols
</details>

---

### Exercise Set 2: Optimize These

**Challenge 1:**
```java
// Check if two strings are anagrams
public boolean isAnagram(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    
    char[] arr1 = s1.toCharArray();
    char[] arr2 = s2.toCharArray();
    Arrays.sort(arr1);  // O(n log n)
    Arrays.sort(arr2);  // O(n log n)
    
    return Arrays.equals(arr1, arr2);
}
```

**Current:** O(n log n) time, O(n) space  
**Your task:** Optimize to O(n) time

<details>
<summary>Solution</summary>

```java
public boolean isAnagram(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    
    HashMap<Character, Integer> freq = new HashMap<>();
    
    // Count characters in s1
    for (char c : s1.toCharArray()) {
        freq.put(c, freq.getOrDefault(c, 0) + 1);
    }
    
    // Subtract characters from s2
    for (char c : s2.toCharArray()) {
        freq.put(c, freq.getOrDefault(c, 0) - 1);
        if (freq.get(c) < 0) return false;
    }
    
    return true;
}
```

**Time:** O(n) - two passes  
**Space:** O(1) - at most 26 letters (constant)

**Alternative for lowercase only:**
```java
public boolean isAnagram(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    
    int[] count = new int[26];
    for (int i = 0; i < s1.length(); i++) {
        count[s1.charAt(i) - 'a']++;
        count[s2.charAt(i) - 'a']--;
    }
    
    for (int c : count) {
        if (c != 0) return false;
    }
    return true;
}
```
**Space:** O(1) - array size 26 is constant
</details>

---

**Challenge 2:**
```java
// Find first repeated character
public char firstRepeated(String s) {
    for (int i = 0; i < s.length(); i++) {
        for (int j = i + 1; j < s.length(); j++) {
            if (s.charAt(i) == s.charAt(j)) {
                return s.charAt(i);
            }
        }
    }
    return '\0';
}
```

**Current:** O(n²) time, O(1) space  
**Your task:** Optimize to O(n) time

<details>
<summary>Solution</summary>

```java
public char firstRepeated(String s) {
    HashSet<Character> seen = new HashSet<>();
    
    for (char c : s.toCharArray()) {
        if (seen.contains(c)) {
            return c;
        }
        seen.add(c);
    }
    return '\0';
}
```

**Time:** O(n) - single pass  
**Space:** O(n) - worst case all characters unique

**Tradeoff:** Used O(n) space to gain O(n) time improvement (from O(n²))
</details>

---

## 📝 Day 2 Checklist

Before moving to Day 3, ensure you can:

- [ ] Analyze loops where the iterator doesn't increment by 1
- [ ] Calculate recursion complexity (time AND space separately)
- [ ] Explain space-time tradeoffs with examples
- [ ] Use `getOrDefault()` with HashMap
- [ ] Recognize when nested loops are NOT O(n²)
- [ ] Choose between ArrayList and LinkedList
- [ ] Identify when to use HashSet vs HashMap

---

## 🎓 Today's Key Insights

1. **Not all nested loops are O(n²)**
   - Check what the inner loop actually does
   - j starting at i cuts iterations in half (still O(n²) though)
   - j doubling makes it O(log n)

2. **Recursion complexity requires two analyses**
   - Time: count total operations
   - Space: measure max call stack depth
   - They're often different!

3. **HashMap is almost always the optimization**
   - O(n²) → O(n): use HashMap for lookups
   - O(n) → O(1): precompute and store

4. **String operations have hidden costs**
   - `substring()` creates new string: O(length)
   - `concat()` in loop: O(n²) total
   - Use StringBuilder: O(n) total

5. **Geometric series ≠ quadratic**
   - n + n/2 + n/4 + ... = O(n), not O(n log n)
   - Memorize: geometric series sums to O(first term)

---

## 🧪 Challenge Problems (Optional)

Test your understanding:

**1. Mystery Function**
```java
public void process(int n) {
    for (int i = 1; i < n; i = i * 2) {
        for (int j = 0; j < n; j++) {
            for (int k = 0; k < n; k++) {
                System.out.println(i + "," + j + "," + k);
            }
        }
    }
}
```

<details>
<summary>Answer</summary>

**Time:** O(n² log n)
- Outer: O(log n) - i doubles
- Middle: O(n)
- Inner: O(n)
- Total: log n × n × n = O(n² log n)

**Space:** O(1)
</details>

---

**2. Optimize This**
```java
// Find intersection of two arrays
public List<Integer> intersect(int[] arr1, int[] arr2) {
    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < arr1.length; i++) {
        for (int j = 0; j < arr2.length; j++) {
            if (arr1[i] == arr2[j]) {
                result.add(arr1[i]);
                break;
            }
        }
    }
    return result;
}
```

<details>
<summary>Solution</summary>

```java
public List<Integer> intersect(int[] arr1, int[] arr2) {
    HashSet<Integer> set = new HashSet<>();
    for (int num : arr2) {
        set.add(num);
    }
    
    List<Integer> result = new ArrayList<>();
    for (int num : arr1) {
        if (set.contains(num)) {
            result.add(num);
            set.remove(num);  // Handle duplicates
        }
    }
    return result;
}
```

**Original:** O(n × m) time  
**Optimized:** O(n + m) time, O(m) space
</details>

---

## 📖 Homework

1. **Practice:** Analyze 5 LeetCode solutions for complexity
2. **Read:** [Big O Misconceptions](https://stackoverflow.com/questions/487258/what-is-a-plain-english-explanation-of-big-o-notation)
3. **Code:** Implement HashMap-based and sorting-based anagram checker, compare runtime
4. **Prepare:** Review array basics - tomorrow we start solving problems!

---

## 💡 Pro Tips for Tomorrow

Tomorrow we start **actual problem-solving**!

**You'll need:**
- ✅ Big O analysis (check!)
- ✅ HashMap for optimizations (check!)
- ✅ When to trade space for time (check!)
- 🎯 Array manipulation techniques (Day 3!)

**Mindset shift:** You now have the tools. Tomorrow you'll learn the **patterns**.

---

## 🎯 Self-Assessment Questions

Test yourself without looking back:

1. What's the complexity of this?
```java
for (int i = 1; i <= n; i = i * 3) {
    System.out.println(i);
}
```

2. How would you optimize a frequency counter from O(n²) to O(n)?

3. What's the space complexity of recursive Fibonacci?

4. When should you use LinkedList instead of ArrayList?

<details>
<summary>Answers</summary>

1. O(log₃ n) - i triples each time (dividing search space by 3)
2. Use HashMap instead of nested loops
3. O(n) - max call stack depth, NOT O(2^n)
4. When you frequently add/remove from the beginning AND don't need random access
</details>

---

**Ready for Day 3?** Tomorrow you'll apply everything you learned to solve your first real LeetCode problems! 🎉

**Remember:** You're not just learning to code—you're learning to think like a computer scientist. The complexity analysis you learned today will guide EVERY optimization you make. 🧠
