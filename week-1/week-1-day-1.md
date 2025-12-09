# Week 1, Day 1: Deep Dive - Java Essentials for DSA

## 🎯 Learning Objectives
By the end of today, you will:
1. Understand Big O notation and why it matters
2. Analyze time and space complexity of simple code
3. Know essential Java collections for DSA
4. Set up your coding environment properly

**Time Required:** 2-3 hours

---

## 📚 Part 1: Big O Notation (60 minutes)

### What is Big O and Why Should You Care?

Big O notation describes **how your algorithm's runtime or memory grows** as input size increases. It's the language interviewers use to discuss efficiency.

**Real-world analogy:**
- **O(1)**: Looking up a word in a dictionary using the page number
- **O(log n)**: Finding a word by opening the dictionary in the middle, then halving your search
- **O(n)**: Reading every word until you find yours
- **O(n²)**: Comparing every word with every other word

### Core Complexities (Memorize These)

```java
// O(1) - Constant Time
// Runtime doesn't change with input size
public int getFirstElement(int[] arr) {
    return arr[0];  // Always one operation
}

// O(n) - Linear Time  
// Runtime grows proportionally with input
public int sumArray(int[] arr) {
    int sum = 0;
    for (int num : arr) {  // Loops n times
        sum += num;
    }
    return sum;
}

// O(n²) - Quadratic Time
// Nested loops = multiply complexities
public void printPairs(int[] arr) {
    for (int i = 0; i < arr.length; i++) {      // n times
        for (int j = 0; j < arr.length; j++) {  // n times for each i
            System.out.println(arr[i] + "," + arr[j]);
        }
    }
}  // Total: n × n = n²

// O(log n) - Logarithmic Time
// Halving the problem each step (binary search)
public int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        
        if (arr[mid] < target) 
            left = mid + 1;   // Eliminate left half
        else 
            right = mid - 1;  // Eliminate right half
    }
    return -1;
}
// Each iteration cuts search space in half: n → n/2 → n/4 → ... → 1

// O(n log n) - Linearithmic Time
// Most efficient sorting algorithms (merge sort, quick sort)
Arrays.sort(arr);  // Built-in sort is O(n log n)
```

### Complexity Ranking (Best to Worst)
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)
```

**Growth comparison** (when n = 1000):
- O(1) = 1 operation
- O(log n) ≈ 10 operations
- O(n) = 1,000 operations
- O(n log n) ≈ 10,000 operations
- O(n²) = 1,000,000 operations
- O(2ⁿ) = 10³⁰⁰ operations (universe-ending)

---

### 🧠 Practice: Analyze These

**Exercise 1:**
```java
public int mystery1(int[] arr) {
    int count = 0;
    for (int i = 0; i < arr.length; i++) {
        count++;
    }
    for (int i = 0; i < arr.length; i++) {
        count++;
    }
    return count;
}
```
**Answer:** O(n) — Two separate loops = n + n = 2n → drop constant → O(n)

---

**Exercise 2:**
```java
public void mystery2(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        for (int j = i; j < arr.length; j++) {
            System.out.println(arr[i] + arr[j]);
        }
    }
}
```
**Answer:** O(n²) — Inner loop runs fewer times, but still quadratic growth
- i=0: n iterations
- i=1: n-1 iterations
- i=2: n-2 iterations
- Total: n + (n-1) + (n-2) + ... + 1 = n(n+1)/2 = O(n²)

---

**Exercise 3:**
```java
public int mystery3(int n) {
    if (n <= 1) return 1;
    return mystery3(n - 1) + mystery3(n - 1);
}
```
**Answer:** O(2ⁿ) — Each call makes 2 recursive calls (exponential tree)

---

### Space Complexity

Space complexity measures **additional memory** used (excluding input).

```java
// O(1) Space - Only using fixed variables
public int sum(int[] arr) {
    int total = 0;  // One integer variable
    for (int num : arr) {
        total += num;
    }
    return total;
}

// O(n) Space - Creating array/list proportional to input
public int[] double(int[] arr) {
    int[] result = new int[arr.length];  // New array of size n
    for (int i = 0; i < arr.length; i++) {
        result[i] = arr[i] * 2;
    }
    return result;
}

// O(n) Space - Recursive call stack
public int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
// Call stack: factorial(5) → factorial(4) → ... → factorial(1)
// Maximum stack depth = n
```

---

## 📚 Part 2: Java Collections Framework (45 minutes)

### Essential Collections for DSA

Here are the **only collections** you need for 95% of LeetCode problems:

```java
import java.util.*;

public class EssentialCollections {
    
    // 1. ARRAYLIST - Dynamic array (most common)
    ArrayList<Integer> list = new ArrayList<>();
    list.add(5);           // O(1) - append
    list.add(0, 10);       // O(n) - insert at index (shifts elements)
    list.get(0);           // O(1) - access by index
    list.remove(0);        // O(n) - remove by index
    list.size();           // O(1) - get size
    
    // 2. HASHMAP - Key-value pairs (critical for optimization)
    HashMap<String, Integer> map = new HashMap<>();
    map.put("apple", 5);   // O(1) average - add/update
    map.get("apple");      // O(1) average - retrieve
    map.containsKey("apple"); // O(1) average - check existence
    map.remove("apple");   // O(1) average - delete
    
    // Iterating through HashMap
    for (String key : map.keySet()) {
        System.out.println(key + ": " + map.get(key));
    }
    
    // 3. HASHSET - Unique elements only
    HashSet<Integer> set = new HashSet<>();
    set.add(5);            // O(1) average - add
    set.contains(5);       // O(1) average - check existence
    set.remove(5);         // O(1) average - delete
    
    // 4. STACK - LIFO (Last In First Out)
    Stack<Integer> stack = new Stack<>();
    stack.push(5);         // O(1) - add to top
    stack.pop();           // O(1) - remove from top
    stack.peek();          // O(1) - view top without removing
    stack.isEmpty();       // O(1) - check if empty
    
    // 5. QUEUE - FIFO (First In First Out)
    Queue<Integer> queue = new LinkedList<>();
    queue.offer(5);        // O(1) - add to back
    queue.poll();          // O(1) - remove from front
    queue.peek();          // O(1) - view front
    
    // 6. PRIORITYQUEUE - Min/Max heap
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    minHeap.offer(5);      // O(log n) - add
    minHeap.poll();        // O(log n) - remove min
    minHeap.peek();        // O(1) - view min
}
```

### When to Use Which Collection?

| Need | Use | Why |
|------|-----|-----|
| Store ordered elements with index access | `ArrayList` | Fast random access |
| Check if element exists quickly | `HashSet` | O(1) lookup |
| Store key-value pairs | `HashMap` | O(1) lookup by key |
| Process in order added | `Queue` | FIFO |
| Process in reverse order | `Stack` | LIFO |
| Always access min/max element | `PriorityQueue` | O(1) peek, O(log n) add/remove |
| Need sorted order | `TreeSet/TreeMap` | O(log n) operations |

---

### 🧠 Practice: Choose the Right Collection

**Scenario 1:** You need to count how many times each word appears in a text.

**Answer:** `HashMap<String, Integer>` 
```java
HashMap<String, Integer> wordCount = new HashMap<>();
for (String word : text.split(" ")) {
    wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
}
```

---

**Scenario 2:** You need to check if there are duplicate numbers in an array.

**Answer:** `HashSet<Integer>`
```java
public boolean containsDuplicate(int[] nums) {
    HashSet<Integer> seen = new HashSet<>();
    for (int num : nums) {
        if (seen.contains(num)) return true;
        seen.add(num);
    }
    return false;
}
```

---

**Scenario 3:** You need to process tasks in the order they arrive.

**Answer:** `Queue<Task>`
```java
Queue<Task> taskQueue = new LinkedList<>();
taskQueue.offer(newTask);
Task next = taskQueue.poll();
```

---

## 📚 Part 3: Critical Java Syntax for DSA (30 minutes)

### Array Operations

```java
// 1. Declaration and Initialization
int[] arr1 = new int[5];              // [0, 0, 0, 0, 0]
int[] arr2 = {1, 2, 3, 4, 5};         // Direct initialization
int[] arr3 = new int[]{1, 2, 3};      // Explicit

// 2. Length
arr1.length  // NOT arr1.length() - it's a property, not method!

// 3. Copying arrays
int[] copy = arr2.clone();                          // Shallow copy
int[] copy2 = Arrays.copyOf(arr2, arr2.length);    // Copy with size
int[] subarray = Arrays.copyOfRange(arr2, 1, 4);   // Copy range [1,4)

// 4. Sorting
Arrays.sort(arr2);                    // Ascending order
Arrays.sort(arr2, Collections.reverseOrder()); // ERROR - only works with Integer[]

// 5. Filling
Arrays.fill(arr1, -1);               // All elements = -1

// 6. Converting to String
System.out.println(Arrays.toString(arr2));  // [1, 2, 3, 4, 5]
```

### String Operations

```java
String s = "hello";

// 1. Immutability - Strings CANNOT be changed!
s.toUpperCase();    // Creates new string, doesn't modify s
System.out.println(s); // Still "hello"

String upper = s.toUpperCase(); // Must store result

// 2. Common methods
s.length()          // 5
s.charAt(0)         // 'h'
s.substring(1, 4)   // "ell" - [start, end)
s.indexOf('l')      // 2 - first occurrence
s.contains("ll")    // true
s.split("")         // ["h","e","l","l","o"] - each character

// 3. StringBuilder for modifications (IMPORTANT!)
StringBuilder sb = new StringBuilder();
sb.append("h");           // O(1) amortized
sb.append("ello");        
sb.toString();            // "hello"
sb.reverse();             // Modifies sb
sb.deleteCharAt(0);       // Remove character
sb.insert(0, 'h');        // Insert character

// String concatenation in loop = O(n²) - BAD!
String result = "";
for (int i = 0; i < 1000; i++) {
    result += "a";  // Creates new string each time!
}

// StringBuilder in loop = O(n) - GOOD!
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append("a");  // Modifies existing
}
```

### Character Operations

```java
char c = 'a';

// 1. Checking character types
Character.isDigit(c)        // false
Character.isLetter(c)       // true
Character.isLetterOrDigit(c) // true
Character.isWhitespace(c)   // false

// 2. Case conversion
Character.toLowerCase('A')  // 'a'
Character.toUpperCase('a')  // 'A'

// 3. Converting char to int
char digit = '5';
int value = digit - '0';    // 5 (ASCII arithmetic)
int value2 = Character.getNumericValue(digit); // 5

// 4. Converting int to char
int num = 5;
char c = (char)(num + '0'); // '5'
```

---

## 🎯 Part 4: Hands-On Practice (30 minutes)

### Exercise 1: Analyze Complexity

```java
public int mystery(int[] arr) {
    int result = 0;
    for (int i = 0; i < arr.length; i++) {
        for (int j = 0; j < arr.length; j++) {
            if (arr[i] == arr[j]) {
                result++;
            }
        }
    }
    return result;
}
```

**Questions:**
1. What is the time complexity?
2. What is the space complexity?
3. What does this function actually do?

<details>
<summary>Click for answers</summary>

1. **Time:** O(n²) - nested loops
2. **Space:** O(1) - only one variable
3. Counts total pairs (including same element with itself)
</details>

---

### Exercise 2: Fix the Bug

```java
public List<Integer> doubleValues(int[] arr) {
    List<Integer> result = new ArrayList<>();
    for (int num : arr) {
        result.add(num * 2);
    }
    return result;
}

// Usage
int[] nums = {1, 2, 3};
List<Integer> doubled = doubleValues(nums);
doubled.add(100);  // What happens to 'nums'?
```

**Question:** Does modifying `doubled` affect the original `nums` array?

<details>
<summary>Click for answer</summary>

**No.** The ArrayList is a completely separate data structure. The original array `nums` remains unchanged. The function creates new Integer objects in a new ArrayList.
</details>

---

### Exercise 3: Optimize This Code

```java
// Find if array has duplicates
public boolean hasDuplicates(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[i] == arr[j]) {
                return true;
            }
        }
    }
    return false;
}
```

**Current complexity:** O(n²)  
**Your task:** Optimize to O(n) using a Java collection.

<details>
<summary>Click for solution</summary>

```java
public boolean hasDuplicates(int[] arr) {
    HashSet<Integer> seen = new HashSet<>();
    for (int num : arr) {
        if (seen.contains(num)) {
            return true;  // Found duplicate
        }
        seen.add(num);
    }
    return false;
}
```

**Time:** O(n) - single pass  
**Space:** O(n) - HashSet can grow to size n  
**Trade-off:** We used extra space to improve time!
</details>

---

## 📝 Day 1 Checklist

Before moving to Day 2, ensure you can:

- [ ] Explain Big O in your own words
- [ ] Identify O(1), O(n), O(n²), O(log n) in code
- [ ] Know when to use ArrayList vs HashMap vs HashSet
- [ ] Understand that Strings are immutable
- [ ] Use StringBuilder for string concatenation in loops
- [ ] Access array length with `.length` (not `.length()`)
- [ ] Recognize space-time tradeoffs

---

## 🎓 Today's Key Insights

1. **Big O simplifies:** Drop constants, keep dominant term
   - `O(2n + 5)` → `O(n)`
   - `O(n² + n)` → `O(n²)`

2. **HashMap is your best friend:** Most optimizations use O(1) lookup

3. **Arrays are fixed size, ArrayLists are dynamic**

4. **String concatenation in loops = performance killer**

5. **Space-time tradeoff is everywhere:** Sometimes using O(n) space gives you O(1) time

---

## 📖 Homework (Optional but Recommended)

1. **Read:** [Big O Cheat Sheet](https://www.bigocheatsheet.com/)
2. **Watch:** [Big O Notation - CS Dojo](https://www.youtube.com/watch?v=v4cd1O4zkGw) (15 min)
3. **Practice:** Write 5 functions and analyze their complexity
4. **Prepare:** Review array manipulation basics before Day 2

---

## 💡 Pro Tips for Tomorrow

- Tomorrow you'll use everything you learned today
- Keep this guide open as reference
- Don't memorize—understand the "why"
- Make mistakes now, learn from them

**You're building the foundation. Take it seriously, but don't stress.** 🚀

---

**Questions for self-reflection:**
1. Can I explain to someone why HashMap is O(1)?
2. What's the difference between `length` and `length()` and `size()`?
3. When would I choose ArrayList over array?

If you can answer these, you're ready for Day 2! 💪
