# Day 1, Week 1: Arrays Fundamentals & Big O Notation - Complete Study Guide

## 🎯 **Day 1 Learning Objectives**
By the end of today, you will:
- ✅ Understand how arrays work in memory
- ✅ Master basic array operations in Java
- ✅ Identify and analyze Big O notation for simple algorithms
- ✅ Write 4 fundamental array manipulation programs

---

## 📚 **PART 1: MORNING SESSION (45 Minutes)**
### Arrays: The Foundation of DSA

### 📖 **1.1 What is an Array?**

An array is a **contiguous block of memory** that stores elements of the same data type. Think of it as a row of boxes, where each box has a number (index) and can hold one item.

```
Index:    0     1     2     3     4
Array: [ 10 ][ 20 ][ 30 ][ 40 ][ 50 ]
         ↑                          ↑
     First element            Last element
```

### 💻 **1.2 Array Declaration & Initialization in Java**

```java
// Method 1: Declare then initialize
int[] numbers;                      // Declaration
numbers = new int[5];               // Initialization (all values = 0)

// Method 2: Declare and initialize with size
int[] scores = new int[10];         // Creates array of 10 integers (all 0)

// Method 3: Declare and initialize with values
int[] ages = {25, 30, 35, 40};     // Size automatically set to 4

// Method 4: Alternative syntax (less common)
int grades[] = new int[]{85, 90, 95}; // Explicitly using new keyword
```

### 🔍 **1.3 Understanding Array Memory**

```java
public class ArrayMemoryDemo {
    public static void main(String[] args) {
        // When you create an array:
        int[] arr = new int[5];
        
        // Memory visualization:
        // Stack Memory: arr (reference variable) → points to heap
        // Heap Memory: [0][0][0][0][0] (actual array)
        
        System.out.println(arr);        // Prints memory address like [I@6d06d69c
        System.out.println(arr.length); // 5 - length is a property, not method!
        
        // Arrays are objects in Java
        System.out.println(arr.getClass().getName()); // [I means int array
    }
}
```

### 🛠️ **1.4 Essential Array Operations**

```java
public class ArrayOperations {
    public static void main(String[] args) {
        int[] nums = {10, 20, 30, 40, 50};
        
        // 1. Accessing elements (O(1) - constant time)
        int firstElement = nums[0];         // 10
        int lastElement = nums[nums.length - 1]; // 50
        int middleElement = nums[nums.length / 2]; // 30
        
        // 2. Modifying elements (O(1) - constant time)
        nums[0] = 100;                      // First element now 100
        nums[nums.length - 1] = 500;        // Last element now 500
        
        // 3. IMPORTANT: Array bounds
        // nums[-1];         // ArrayIndexOutOfBoundsException
        // nums[5];          // ArrayIndexOutOfBoundsException (index 0-4 only)
        
        // 4. Array size is FIXED after creation
        // nums.length = 10; // COMPILATION ERROR - length is final
    }
}
```

### 📝 **1.5 Array Traversal Patterns - MASTER THESE!**

```java
public class ArrayTraversal {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        
        // Pattern 1: Standard for loop (when you need index)
        System.out.println("Standard for loop:");
        for (int i = 0; i < arr.length; i++) {
            System.out.println("Index " + i + ": " + arr[i]);
        }
        
        // Pattern 2: Enhanced for loop (when you only need values)
        System.out.println("\nEnhanced for loop:");
        for (int value : arr) {
            System.out.println("Value: " + value);
        }
        
        // Pattern 3: Reverse traversal
        System.out.println("\nReverse traversal:");
        for (int i = arr.length - 1; i >= 0; i--) {
            System.out.println("Index " + i + ": " + arr[i]);
        }
        
        // Pattern 4: Step traversal (every 2nd element)
        System.out.println("\nEvery second element:");
        for (int i = 0; i < arr.length; i += 2) {
            System.out.println("Index " + i + ": " + arr[i]);
        }
        
        // Pattern 5: While loop traversal
        System.out.println("\nWhile loop:");
        int index = 0;
        while (index < arr.length) {
            System.out.println(arr[index]);
            index++;
        }
    }
}
```

### ✍️ **Morning Practice Exercise 1: Array Basics**

Complete this code without looking at solutions:

```java
public class MorningPractice {
    public static void main(String[] args) {
        // TODO 1: Create an array of 7 integers with your favorite numbers
        
        // TODO 2: Print the third element
        
        // TODO 3: Change the last element to 100
        
        // TODO 4: Print all elements using enhanced for loop
        
        // TODO 5: Calculate and print the sum of all elements
        
        // TODO 6: Find and print the largest element
    }
}
```

**Solution** (Try yourself first!):
<details>
<summary>Click to see solution</summary>

```java
public class MorningPractice {
    public static void main(String[] args) {
        // TODO 1: Create an array of 7 integers
        int[] myArray = {5, 10, 15, 20, 25, 30, 35};
        
        // TODO 2: Print the third element (index 2)
        System.out.println("Third element: " + myArray[2]);
        
        // TODO 3: Change the last element to 100
        myArray[myArray.length - 1] = 100;
        
        // TODO 4: Print all elements
        System.out.println("All elements:");
        for (int num : myArray) {
            System.out.print(num + " ");
        }
        System.out.println();
        
        // TODO 5: Calculate sum
        int sum = 0;
        for (int num : myArray) {
            sum += num;
        }
        System.out.println("Sum: " + sum);
        
        // TODO 6: Find largest
        int max = myArray[0];
        for (int num : myArray) {
            if (num > max) {
                max = num;
            }
        }
        System.out.println("Largest: " + max);
    }
}
```
</details>

---

## 🚀 **PART 2: AFTERNOON SESSION (45 Minutes)**
### Big O Notation: The Language of Efficiency

### 📖 **2.1 What is Big O Notation?**

Big O describes the **worst-case** performance of an algorithm as input size grows. It answers: "How does runtime/space grow as data gets bigger?"

### 📊 **2.2 Common Time Complexities (From Best to Worst)**

| Big O | Name | Example | When n=1000 | Real-world Analogy |
|-------|------|---------|-------------|-------------------|
| O(1) | Constant | Array access by index | 1 operation | Finding a page in a book when you know the page number |
| O(log n) | Logarithmic | Binary search | ~10 operations | Finding a word in a dictionary |
| O(n) | Linear | Simple loop | 1000 operations | Reading a book page by page |
| O(n log n) | Linearithmic | Efficient sorting | ~10,000 operations | Sorting a deck of cards efficiently |
| O(n²) | Quadratic | Nested loops | 1,000,000 operations | Comparing every person with every other person in a room |
| O(2ⁿ) | Exponential | Recursive fibonacci | 2^1000 operations | Trying all combinations of a password |

### 🔍 **2.3 Analyzing Code Complexity - Step by Step**

```java
public class ComplexityAnalysis {
    
    // Example 1: O(1) - Constant Time
    public static int getFirst(int[] arr) {
        return arr[0];  // Always 1 operation, regardless of array size
    }
    
    // Example 2: O(n) - Linear Time
    public static int findMax(int[] arr) {
        int max = arr[0];                    // O(1)
        for (int i = 1; i < arr.length; i++) { // Loop runs n-1 times
            if (arr[i] > max) {              // O(1)
                max = arr[i];                // O(1)
            }
        }
        return max;                          // O(1)
        // Total: O(1) + O(n-1) * O(1) + O(1) = O(n)
    }
    
    // Example 3: O(n²) - Quadratic Time
    public static void printPairs(int[] arr) {
        for (int i = 0; i < arr.length; i++) {        // Outer loop: n times
            for (int j = 0; j < arr.length; j++) {    // Inner loop: n times
                System.out.println(arr[i] + "," + arr[j]); // O(1)
            }
        }
        // Total: n * n * O(1) = O(n²)
    }
    
    // Example 4: O(n²) but different pattern
    public static void printTriangle(int[] arr) {
        for (int i = 0; i < arr.length; i++) {        // n times
            for (int j = 0; j <= i; j++) {            // 1, 2, 3...n times
                System.out.print(arr[j] + " ");       // O(1)
            }
            System.out.println();
        }
        // Total: 1 + 2 + 3 + ... + n = n(n+1)/2 = O(n²)
    }
    
    // Example 5: O(log n) - Logarithmic Time (preview)
    public static int binarySearchPreview(int[] sortedArr, int target) {
        int left = 0, right = sortedArr.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;  // Prevent overflow
            
            if (sortedArr[mid] == target) {
                return mid;
            } else if (sortedArr[mid] < target) {
                left = mid + 1;  // Eliminate half
            } else {
                right = mid - 1; // Eliminate half
            }
        }
        return -1;
        // Each iteration cuts search space in half: O(log n)
    }
}
```

### 📏 **2.4 Rules for Big O Analysis**

```java
public class BigORules {
    
    // Rule 1: Drop Constants
    public static void rule1(int[] arr) {
        for (int i = 0; i < arr.length; i++) { }  // O(n)
        for (int i = 0; i < arr.length; i++) { }  // O(n)
        // Total: O(n) + O(n) = O(2n) → O(n) (drop the 2)
    }
    
    // Rule 2: Drop Non-Dominant Terms
    public static void rule2(int[] arr) {
        // O(n) part
        for (int i = 0; i < arr.length; i++) { }
        
        // O(n²) part
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr.length; j++) { }
        }
        // Total: O(n) + O(n²) → O(n²) (n² dominates n)
    }
    
    // Rule 3: Different Variables for Different Inputs
    public static void rule3(int[] arr1, int[] arr2) {
        for (int i = 0; i < arr1.length; i++) { }  // O(n)
        for (int j = 0; j < arr2.length; j++) { }  // O(m)
        // Total: O(n + m) - DON'T simplify to O(n)!
    }
    
    // Rule 4: Nested Loops Multiply
    public static void rule4(int[] arr1, int[] arr2) {
        for (int i = 0; i < arr1.length; i++) {      // O(n)
            for (int j = 0; j < arr2.length; j++) {  // O(m)
                // Operation
            }
        }
        // Total: O(n * m)
    }
}
```

### 💡 **2.5 Space Complexity Basics**

```java
public class SpaceComplexity {
    
    // O(1) Space - Constant
    public static int sum(int[] arr) {
        int total = 0;  // Only one variable regardless of input size
        for (int num : arr) {
            total += num;
        }
        return total;
    }
    
    // O(n) Space - Linear
    public static int[] copyArray(int[] arr) {
        int[] newArr = new int[arr.length];  // Space grows with input
        for (int i = 0; i < arr.length; i++) {
            newArr[i] = arr[i];
        }
        return newArr;
    }
    
    // O(n²) Space - Quadratic
    public static int[][] createMatrix(int n) {
        int[][] matrix = new int[n][n];  // n*n space
        return matrix;
    }
}
```

### ✍️ **Afternoon Practice Exercise: Complexity Analysis**

Analyze the time complexity of each method:

```java
public class ComplexityPractice {
    
    // Problem 1: What's the time complexity?
    public static void mystery1(int[] arr) {
        System.out.println(arr[0]);
        System.out.println(arr[arr.length / 2]);
        System.out.println(arr[arr.length - 1]);
    }
    // Your answer: O(?)
    
    // Problem 2: What's the time complexity?
    public static void mystery2(int[] arr) {
        for (int i = 0; i < arr.length; i += 2) {
            System.out.println(arr[i]);
        }
    }
    // Your answer: O(?)
    
    // Problem 3: What's the time complexity?
    public static void mystery3(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                System.out.println(arr[i] + arr[j]);
            }
        }
    }
    // Your answer: O(?)
    
    // Problem 4: What's the time complexity?
    public static boolean mystery4(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                return true;  // Early exit possible
            }
        }
        return false;
    }
    // Your answer: Best case O(?), Worst case O(?)
}
```

**Answers**:
<details>
<summary>Click to see answers</summary>

1. O(1) - Only 3 operations regardless of array size
2. O(n) - Still visits n/2 elements, constants dropped
3. O(n²) - Nested loops with triangular pattern (n-1 + n-2 + ... + 1)
4. Best: O(1) if target is first element, Worst: O(n) if target not present
</details>

---

## 🌙 **PART 3: EVENING SESSION (30 Minutes)**
### Hands-on Coding Practice

### 🎯 **Problem Set: Core Array Algorithms**

Implement these fundamental array algorithms from scratch:

### **Problem 1: Find Maximum Element**
```java
public class Problem1 {
    public static int findMax(int[] arr) {
        // TODO: Handle edge cases
        // TODO: Find and return the maximum element
        // Time: O(n), Space: O(1)
    }
    
    public static void main(String[] args) {
        // Test cases
        System.out.println(findMax(new int[]{3, 7, 1, 9, 4})); // Should print 9
        System.out.println(findMax(new int[]{-5, -2, -8}));   // Should print -2
        System.out.println(findMax(new int[]{42}));           // Should print 42
    }
}
```

<details>
<summary>Solution</summary>

```java
public static int findMax(int[] arr) {
    if (arr == null || arr.length == 0) {
        throw new IllegalArgumentException("Array cannot be null or empty");
    }
    
    int max = arr[0];
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}
```
</details>

### **Problem 2: Reverse Array In-Place**
```java
public class Problem2 {
    public static void reverseArray(int[] arr) {
        // TODO: Reverse the array in-place (modify original array)
        // TODO: Use two pointers approach
        // Time: O(n), Space: O(1)
    }
    
    public static void main(String[] args) {
        int[] test1 = {1, 2, 3, 4, 5};
        reverseArray(test1);
        System.out.println(Arrays.toString(test1)); // [5, 4, 3, 2, 1]
        
        int[] test2 = {1, 2, 3, 4};
        reverseArray(test2);
        System.out.println(Arrays.toString(test2)); // [4, 3, 2, 1]
    }
}
```

<details>
<summary>Solution</summary>

```java
public static void reverseArray(int[] arr) {
    if (arr == null || arr.length <= 1) {
        return;  // Nothing to reverse
    }
    
    int left = 0;
    int right = arr.length - 1;
    
    while (left < right) {
        // Swap elements
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        
        left++;
        right--;
    }
}
```
</details>

### **Problem 3: Calculate Array Sum**
```java
public class Problem3 {
    public static int calculateSum(int[] arr) {
        // TODO: Return sum of all elements
        // TODO: Handle empty array
        // Time: O(n), Space: O(1)
    }
    
    public static void main(String[] args) {
        System.out.println(calculateSum(new int[]{1, 2, 3, 4})); // 10
        System.out.println(calculateSum(new int[]{-1, -2, 3})); // 0
        System.out.println(calculateSum(new int[]{}));          // 0
    }
}
```

<details>
<summary>Solution</summary>

```java
public static int calculateSum(int[] arr) {
    if (arr == null || arr.length == 0) {
        return 0;
    }
    
    int sum = 0;
    for (int num : arr) {
        sum += num;
    }
    return sum;
}
```
</details>

### **Problem 4: Check if Element Exists**
```java
public class Problem4 {
    public static boolean contains(int[] arr, int target) {
        // TODO: Return true if target exists in array
        // TODO: Return false otherwise
        // Time: O(n), Space: O(1)
    }
    
    public static void main(String[] args) {
        int[] arr = {5, 2, 8, 1, 9};
        System.out.println(contains(arr, 8));  // true
        System.out.println(contains(arr, 10)); // false
        System.out.println(contains(new int[]{}, 5)); // false
    }
}
```

<details>
<summary>Solution</summary>

```java
public static boolean contains(int[] arr, int target) {
    if (arr == null || arr.length == 0) {
        return false;
    }
    
    for (int num : arr) {
        if (num == target) {
            return true;
        }
    }
    return false;
}
```
</details>

### **Bonus Challenge: Second Largest Element**
```java
public class BonusChallenge {
    public static int findSecondLargest(int[] arr) {
        // TODO: Find the second largest element
        // TODO: Handle arrays with duplicates
        // TODO: Throw exception if array has less than 2 unique elements
        // Time: O(n), Space: O(1)
    }
    
    public static void main(String[] args) {
        System.out.println(findSecondLargest(new int[]{5, 2, 8, 1, 9})); // 8
        System.out.println(findSecondLargest(new int[]{5, 5, 5, 2}));    // 2
        // System.out.println(findSecondLargest(new int[]{5, 5, 5}));   // Exception
    }
}
```

<details>
<summary>Solution</summary>

```java
public static int findSecondLargest(int[] arr) {
    if (arr == null || arr.length < 2) {
        throw new IllegalArgumentException("Array must have at least 2 elements");
    }
    
    int first = Integer.MIN_VALUE;
    int second = Integer.MIN_VALUE;
    
    for (int num : arr) {
        if (num > first) {
            second = first;
            first = num;
        } else if (num > second && num != first) {
            second = num;
        }
    }
    
    if (second == Integer.MIN_VALUE) {
        throw new IllegalArgumentException("Array must have at least 2 unique elements");
    }
    
    return second;
}
```
</details>

---

## 📊 **Daily Progress Tracker**

### **Self-Assessment Checklist**

Rate yourself (1-5) on each concept:

| Concept | Understanding (1-5) | Can Implement? | Need Review? |
|---------|-------------------|----------------|--------------|
| Array declaration & initialization | __ | Yes/No | Yes/No |
| Array indexing (0-based) | __ | Yes/No | Yes/No |
| Array traversal (for loop) | __ | Yes/No | Yes/No |
| Array traversal (enhanced for) | __ | Yes/No | Yes/No |
| O(1) complexity recognition | __ | Yes/No | Yes/No |
| O(n) complexity recognition | __ | Yes/No | Yes/No |
| O(n²) complexity recognition | __ | Yes/No | Yes/No |
| Finding max element | __ | Yes/No | Yes/No |
| Array reversal | __ | Yes/No | Yes/No |
| Array sum calculation | __ | Yes/No | Yes/No |

### **Problems Solved Today**

| Problem | Time Taken | Solved Independently | Key Learning |
|---------|------------|---------------------|--------------|
| Find Max | ___ min | Yes/No | |
| Reverse Array | ___ min | Yes/No | |
| Calculate Sum | ___ min | Yes/No | |
| Contains Element | ___ min | Yes/No | |
| Second Largest (Bonus) | ___ min | Yes/No | |

---

## 📝 **Day 1 Summary Notes Template**

Fill this out before bed:

```markdown
## Day 1 Reflection

### Three Main Things I Learned:
1. ________________________________
2. ________________________________
3. ________________________________

### Concepts That Clicked:
- ________________________________

### Concepts That Need Review:
- ________________________________

### Mistakes I Made & Lessons:
- ________________________________

### Tomorrow's Focus Areas:
- ________________________________

### Questions to Research:
- ________________________________
```

---

## 🚦 **Common Mistakes to Avoid**

1. **ArrayIndexOutOfBoundsException**
   ```java
   // WRONG
   for (int i = 0; i <= arr.length; i++) { } // <= causes error
   
   // CORRECT
   for (int i = 0; i < arr.length; i++) { }  // < is correct
   ```

2. **Forgetting null checks**
   ```java
   // WRONG
   public static int findMax(int[] arr) {
       int max = arr[0];  // NullPointerException if arr is null
   }
   
   // CORRECT
   public static int findMax(int[] arr) {
       if (arr == null || arr.length == 0) {
           throw new IllegalArgumentException("Invalid array");
       }
       int max = arr[0];
   }
   ```

3. **Modifying array during enhanced for loop**
   ```java
   // WRONG - doesn't modify array
   for (int num : arr) {
       num = num * 2;  // Only modifies local variable
   }
   
   // CORRECT - use index-based loop
   for (int i = 0; i < arr.length; i++) {
       arr[i] = arr[i] * 2;
   }
   ```

---

## 🎯 **Tomorrow's Preview (Day 2)**

Get ready to learn:
- Dynamic arrays with ArrayList
- Array manipulation patterns (rotation, shifting)
- Prefix sum technique
- More complex two-pointer problems

---

## 💪 **End-of-Day Motivation**

You've just completed Day 1! Arrays are the foundation of nearly every data structure. Today's concepts will be used in:
- Strings (character arrays)
- HashMaps (array of buckets)
- Heaps (array representation)
- Dynamic Programming (array memoization)
- Graph adjacency matrix (2D arrays)

Every expert was once a beginner. Keep coding, keep learning!

## 🔗 **Additional Resources for Day 1**

- [Visualgo - Array Visualization](https://visualgo.net/en/array)
- [Java Arrays Documentation](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html)
- [Big O Cheat Sheet](https://www.bigocheatsheet.com/)
- Practice typing code by hand (helps memory retention)

---

**Remember**: Understanding > Speed. Take your time to truly grasp these fundamentals!
