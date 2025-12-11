# Week 1: Arrays & Strings Fundamentals - Daily Structured Plan

## 📅 **DAY 1: Array Fundamentals & Big O Notation**

### 🌅 **Morning Session (45 minutes)**
#### Theory & Concepts
- **What to Learn:**
  - Array declaration and initialization in Java
  - Array indexing (0-based)
  - Array length property
  - Common array operations

#### Java Code Examples to Practice:
```java
// Array basics to code along
int[] nums = new int[5];  // Declaration
int[] nums2 = {1, 2, 3, 4, 5};  // Initialization
System.out.println(nums2.length);  // Length property
System.out.println(nums2[0]);  // Accessing elements

// Basic traversal patterns
for (int i = 0; i < nums.length; i++) {
    System.out.println(nums[i]);
}

for (int num : nums) {  // Enhanced for loop
    System.out.println(num);
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Big O Notation Basics
- **Understand:**
  - O(1) - Constant time (array access by index)
  - O(n) - Linear time (single loop)
  - O(n²) - Quadratic time (nested loops)
  - O(log n) - Logarithmic (binary search preview)
  - Space complexity basics

#### Practice Problems:
```java
// Analyze time complexity of these methods:
public int findMax(int[] arr) {
    int max = arr[0];  // O(1)
    for (int i = 1; i < arr.length; i++) {  // O(n)
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;  // Total: O(n)
}

public void printPairs(int[] arr) {
    for (int i = 0; i < arr.length; i++) {  // O(n)
        for (int j = 0; j < arr.length; j++) {  // O(n)
            System.out.println(arr[i] + ", " + arr[j]);
        }
    }
    // Total: O(n²)
}
```

### 🌙 **Evening Session (30 minutes)**
#### Hands-on Practice
- **Code these array problems without looking at solutions:**
  1. Find the maximum element in an array
  2. Reverse an array in-place
  3. Calculate sum of all elements
  4. Find if a specific element exists

### 📝 **Day 1 Checklist**
- [ ] Understand array memory allocation
- [ ] Master basic array traversal
- [ ] Can identify O(1), O(n), O(n²) complexities
- [ ] Complete 4 basic array problems

---

## 📅 **DAY 2: Advanced Array Patterns & ArrayList**

### 🌅 **Morning Session (45 minutes)**
#### Theory & Concepts
- **ArrayList vs Array:**
  - Dynamic sizing
  - ArrayList methods (add, remove, get, set, size)
  - When to use ArrayList vs array

#### Java Code Examples:
```java
import java.util.ArrayList;
import java.util.Arrays;

// ArrayList operations
ArrayList<Integer> list = new ArrayList<>();
list.add(10);  // Adding elements
list.add(20);
list.add(1, 15);  // Insert at index
list.remove(0);  // Remove by index
list.get(0);  // Access element
list.size();  // Get size

// Converting between array and ArrayList
int[] arr = {1, 2, 3};
ArrayList<Integer> listFromArray = new ArrayList<>();
for (int num : arr) {
    listFromArray.add(num);
}

// ArrayList to array
Integer[] arrFromList = list.toArray(new Integer[0]);
```

### 🌞 **Afternoon Session (45 minutes)**
#### Common Array Patterns
- **Master these patterns:**
  1. Running sum/prefix sum
  2. Finding duplicates
  3. Array rotation
  4. Merging arrays

#### Code Templates:
```java
// Prefix sum pattern
public int[] runningSum(int[] nums) {
    for (int i = 1; i < nums.length; i++) {
        nums[i] += nums[i - 1];
    }
    return nums;
}

// In-place array modification pattern
public void rotateArray(int[] nums, int k) {
    k = k % nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
}

private void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
  - First attempt: Use nested loops (understand why it's O(n²))
  - Second attempt: Use sorting (O(n log n))
  - Third attempt: Use HashSet (O(n)) - preview for next week

### 📝 **Day 2 Checklist**
- [ ] Comfortable with ArrayList operations
- [ ] Understand when to use ArrayList vs array
- [ ] Master prefix sum pattern
- [ ] Complete Contains Duplicate with 3 approaches

---

## 📅 **DAY 3: String Fundamentals in Java**

### 🌅 **Morning Session (45 minutes)**
#### String Basics
- **Core String Methods:**
  - charAt(index)
  - length()
  - substring(start, end)
  - indexOf(str)
  - equals() vs ==
  - toLowerCase(), toUpperCase()
  - trim()
  - split()

#### Practice Code:
```java
String str = "Hello World";

// Character access
char firstChar = str.charAt(0);  // 'H'
char lastChar = str.charAt(str.length() - 1);  // 'd'

// Substring operations
String sub = str.substring(0, 5);  // "Hello"
String sub2 = str.substring(6);  // "World"

// String comparison
String s1 = "hello";
String s2 = "hello";
String s3 = new String("hello");
System.out.println(s1 == s2);  // true (string pool)
System.out.println(s1 == s3);  // false (different objects)
System.out.println(s1.equals(s3));  // true (content comparison)

// String to char array
char[] charArray = str.toCharArray();
for (char c : charArray) {
    System.out.print(c + " ");
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### String Immutability & StringBuilder
- **Understanding Immutability:**
  - Why strings are immutable
  - Performance implications
  - StringBuilder for efficient string manipulation

#### StringBuilder Practice:
```java
// Inefficient string concatenation
String result = "";
for (int i = 0; i < 1000; i++) {
    result += "a";  // Creates new string each time - O(n²)
}

// Efficient with StringBuilder
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append("a");  // O(n)
}
String result = sb.toString();

// StringBuilder methods
sb.append("Hello");
sb.insert(0, "Start: ");
sb.delete(0, 7);
sb.reverse();
```

### 🌙 **Evening Session (30 minutes)**
#### String Problem Patterns
- **Implement these common patterns:**
  1. Check if string is palindrome
  2. Count occurrences of each character
  3. Reverse words in a string

```java
// Palindrome check
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Character frequency
public void countChars(String s) {
    int[] freq = new int[26];  // for lowercase letters
    for (char c : s.toCharArray()) {
        if (c >= 'a' && c <= 'z') {
            freq[c - 'a']++;
        }
    }
}
```

### 📝 **Day 3 Checklist**
- [ ] Master essential String methods
- [ ] Understand String immutability
- [ ] Comfortable with StringBuilder
- [ ] Implement 3 string manipulation patterns

---

## 📅 **DAY 4: String Advanced Patterns & Character Arrays**

### 🌅 **Morning Session (45 minutes)**
#### Character Manipulation
- **ASCII values and character arithmetic:**
  - Converting char to int
  - Character validation
  - Case conversion without built-in methods

#### Practice Code:
```java
// Character operations
char c = 'A';
int asciiValue = (int) c;  // 65
char nextChar = (char)(c + 1);  // 'B'

// Check character types
public boolean isLetter(char c) {
    return (c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z');
}

public boolean isDigit(char c) {
    return c >= '0' && c <= '9';
}

// Manual case conversion
public char toLowerCase(char c) {
    if (c >= 'A' && c <= 'Z') {
        return (char)(c + 32);  // or c - 'A' + 'a'
    }
    return c;
}

// Convert digit char to int
char digit = '5';
int value = digit - '0';  // 5
```

### 🌞 **Afternoon Session (45 minutes)**
#### String Algorithm Patterns
- **Master these patterns:**
  1. Sliding window for substrings
  2. Two-pointer for string problems
  3. String matching basics

#### Implementation:
```java
// Find longest substring with k distinct characters (preview)
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    if (s == null || s.length() == 0 || k == 0) return 0;
    
    int left = 0, maxLen = 0;
    HashMap<Character, Integer> map = new HashMap<>();
    
    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        map.put(c, map.getOrDefault(c, 0) + 1);
        
        while (map.size() > k) {
            char leftChar = s.charAt(left);
            map.put(leftChar, map.get(leftChar) - 1);
            if (map.get(leftChar) == 0) {
                map.remove(leftChar);
            }
            left++;
        }
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [344. Reverse String](https://leetcode.com/problems/reverse-string/)
  - Implement with two pointers
  - Must be in-place (O(1) space)
  - Handle both iterative and recursive solutions

### 📝 **Day 4 Checklist**
- [ ] Understand ASCII and character arithmetic
- [ ] Can validate and convert characters
- [ ] Implement basic sliding window
- [ ] Complete Reverse String problem

---

## 📅 **DAY 5: Introduction to Two-Pointer Technique**

### 🌅 **Morning Session (45 minutes)**
#### Two-Pointer Patterns
- **Three main patterns:**
  1. Pointers at opposite ends moving towards center
  2. Pointers at same end moving in same direction
  3. Fast and slow pointers

#### Visual Understanding:
```java
// Pattern 1: Opposite ends
public boolean isPalindrome(int[] arr) {
    int left = 0;
    int right = arr.length - 1;
    
    while (left < right) {
        if (arr[left] != arr[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Pattern 2: Same direction
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    
    int slow = 0;
    for (int fast = 1; fast < nums.length; fast++) {
        if (nums[fast] != nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }
    return slow + 1;
}

// Pattern 3: Fast and slow (preview for linked lists)
public boolean hasCycle(int[] arr) {
    // Conceptual - actual implementation needs linked list
    int slow = 0, fast = 0;
    while (fast < arr.length - 1) {
        slow += 1;
        fast += 2;
        if (slow == fast) return true;
    }
    return false;
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Two-Pointer Problem Solving Strategy
- **Step-by-step approach:**
  1. Identify if two-pointer applies
  2. Decide pointer placement (start/end/both start)
  3. Define movement conditions
  4. Handle edge cases

#### Practice Problems:
```java
// Merge two sorted arrays
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int p1 = m - 1;  // Pointer for nums1
    int p2 = n - 1;  // Pointer for nums2
    int p = m + n - 1;  // Pointer for merged array
    
    while (p1 >= 0 && p2 >= 0) {
        if (nums1[p1] > nums2[p2]) {
            nums1[p] = nums1[p1];
            p1--;
        } else {
            nums1[p] = nums2[p2];
            p2--;
        }
        p--;
    }
    
    // Copy remaining elements from nums2
    while (p2 >= 0) {
        nums1[p] = nums2[p2];
        p2--;
        p--;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [1. Two Sum](https://leetcode.com/problems/two-sum/)
  - First attempt: Brute force with nested loops
  - Second attempt: Think about optimization (preview HashMap solution)
  - Focus on understanding the problem-solving process

### 📝 **Day 5 Checklist**
- [ ] Identify three two-pointer patterns
- [ ] Know when to use two pointers
- [ ] Implement array merge with two pointers
- [ ] Complete Two Sum (brute force acceptable)

---

## 📅 **DAY 6: Problem-Solving Practice Day**

### 🌅 **Morning Session (45 minutes)**
#### Review and Consolidate
- **Quick review of week's concepts:**
  - Array traversal patterns
  - String manipulation
  - Two-pointer technique
  - Time complexity analysis

#### Self-Assessment Problems:
```java
// Problem 1: Find second largest element
public int findSecondLargest(int[] arr) {
    // Your implementation
    // Consider edge cases: array size < 2, duplicates
}

// Problem 2: Check if two strings are rotations
public boolean isRotation(String s1, String s2) {
    // Hint: "abcde" rotated = "cdeab"
    // Your implementation
}

// Problem 3: Move all zeros to end
public void moveZeroes(int[] nums) {
    // Maintain relative order of non-zero elements
    // Your implementation
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### LeetCode Problem Set
- **Solve in order:**
  1. [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
     - Apply two-pointer technique
     - Handle alphanumeric validation
  
  2. Start [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
     - Try without division
     - Think about prefix and suffix products

### 🌙 **Evening Session (30 minutes)**
#### Solution Analysis
- **For each problem solved today:**
  1. Write down your approach
  2. Identify time/space complexity
  3. Look at one optimal solution
  4. Note what you learned

#### Solution Template:
```java
/*
Problem: [Problem Name]
Approach: [Your approach in 2-3 sentences]
Time Complexity: O(?)
Space Complexity: O(?)
Key Learning: [What new thing you learned]
*/

// Your solution code
```

### 📝 **Day 6 Checklist**
- [ ] Complete 3 self-assessment problems
- [ ] Solve Valid Palindrome independently
- [ ] Attempt Product of Array Except Self
- [ ] Document solutions with complexity analysis

---

## 📅 **DAY 7: Week Review & Advanced Challenge**

### 🌅 **Morning Session (60 minutes)**
#### Comprehensive Review
- **Create your personal notes covering:**
  1. Array methods cheat sheet
  2. String methods cheat sheet
  3. Two-pointer patterns
  4. Common time complexities

#### Knowledge Check Quiz:
```java
// Answer these without running code:

// 1. What's the output?
String s = "hello";
s.concat(" world");
System.out.println(s);  // Output: ?

// 2. Time complexity?
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {
        // O(1) operation
    }
}  // Complexity: ?

// 3. Will this compile?
int[] arr = new int[5];
ArrayList<int> list = new ArrayList<>();  // Issue?

// 4. Best approach for finding duplicates?
// a) Nested loops b) Sorting c) HashSet d) Two pointers

// 5. Space complexity of StringBuilder with n appends?
// O(1), O(n), O(n²), or O(log n)?
```

### 🌞 **Afternoon Session (90 minutes)**
#### Complete LeetCode Weekly Challenge
- **Complete all Week 1 problems:**
  1. Finish [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
  2. Review and optimize all previous solutions
  3. Bonus: Try [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)
     - Use only O(1) space
     - Can't modify array

### 🌙 **Evening Session (30 minutes)**
#### Week 1 Reflection & Planning
- **Document in your learning journal:**
  1. **Strengths identified:** What came easily?
  2. **Challenges faced:** What was difficult?
  3. **Key insights:** Top 3 things learned
  4. **Patterns recognized:** Common problem-solving patterns
  5. **Week 2 preparation:** What to review before starting HashMap

#### Create Your Reference Sheet:
```java
// WEEK 1 PATTERNS REFERENCE

// 1. Array Traversal
for (int i = 0; i < arr.length; i++) { }
for (int num : arr) { }

// 2. Two Pointers
int left = 0, right = arr.length - 1;
while (left < right) { }

// 3. String to Char Array
char[] chars = str.toCharArray();

// 4. StringBuilder for Concatenation
StringBuilder sb = new StringBuilder();
sb.append(str);

// 5. In-place Array Modification
// Swap: temp variable or XOR

// 6. Frequency Counting
int[] freq = new int[26];  // for letters
freq[c - 'a']++;

// 7. Sliding Window (preview)
int left = 0;
for (int right = 0; right < arr.length; right++) { }
```

### 📝 **Day 7 Final Checklist**
- [ ] Complete comprehensive notes
- [ ] Score at least 4/5 on knowledge quiz
- [ ] Solve all Week 1 LeetCode problems
- [ ] Document top 5 learnings
- [ ] Create pattern reference sheet
- [ ] Ready for Week 2: HashMap & HashSet

---

## 🎯 **End of Week 1 Milestones**

### You Should Now Be Able To:
✅ Implement common array operations efficiently  
✅ Manipulate strings using various Java methods  
✅ Apply two-pointer technique to appropriate problems  
✅ Analyze time and space complexity  
✅ Solve array/string problems systematically  

### Problems Completed (Minimum):
- ✅ Two Sum (at least brute force)
- ✅ Contains Duplicate  
- ✅ Reverse String  
- ✅ Valid Palindrome  
- ✅ Product of Array Except Self (attempted)

### Prepare for Week 2:
- Review HashMap basic operations if time permits
- Rest and consolidate Week 1 learning
- Maintain confidence - you've built a solid foundation!

## 💪 **Motivational Note**
Congratulations on completing Week 1! You've covered the fundamental building blocks that will support all future learning. Arrays and strings appear in nearly every coding interview, and you now have the tools to approach them confidently. Remember: mastery comes from repetition and understanding, not just completion. Keep practicing!
