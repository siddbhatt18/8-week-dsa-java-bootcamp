### Week 1 – Day 2  
**Theme:** Loops + Arrays Basics  
**Goal for today:**  
- Become very comfortable with `for` loops (and see `while`).  
- Learn how to declare, initialize, and iterate through arrays in Java.  
- Write simple methods that take arrays as input and return useful results (sum, max, etc.).

---

## 0. High-Level Plan (2–3 hours total)

1. Quick review of Day 1 (10–15 min)  
2. Loop practice & variations (45–60 min)  
3. Arrays: theory & syntax (30–45 min)  
4. Array exercises & methods (45–60 min)  
5. Short reflection & self-check (15–20 min)

Keep everything inside package: `week1.day2`.

---

## 1. Quick Review from Day 1 (10–15 min)

Without looking at code, answer in a notebook or text file:

1. Write the Java line to declare and initialize:
   - an `int a = 10;`
   - a `boolean isValid = false;`
2. Write the general for-loop template that prints 1 to 5.
3. Write a method header that:
   - returns an `int`
   - is called `square`
   - takes an `int n` as input

Then quickly skim your Day 1 classes (`BasicsPractice`, `ConditionalsPractice`, `LoopPractice`, `MethodsPractice`) to refresh.

---

## 2. Loop Practice & Variations (45–60 min)

Create a new file: `LoopPractice2.java` in `week1.day2`.

```java
package week1.day2;

public class LoopPractice2 {
    public static void main(String[] args) {

        // 1. Print 1 to 10
        System.out.println("Numbers 1 to 10:");
        for (int i = 1; i <= 10; i++) {
            System.out.print(i + " ");
        }
        System.out.println(); // new line

        // 2. Sum of 1 to 100
        int sum = 0;
        for (int i = 1; i <= 100; i++) {
            sum += i; // sum = sum + i
        }
        System.out.println("Sum 1 to 100 = " + sum);

        // 3. Multiplication table of 5
        System.out.println("Multiplication table of 5:");
        for (int i = 1; i <= 10; i++) {
            System.out.println("5 x " + i + " = " + (5 * i));
        }

        // 4. While loop example (countdown)
        System.out.println("Countdown from 5:");
        int n = 5;
        while (n > 0) {
            System.out.println(n);
            n--; // n = n - 1
        }
        System.out.println("Go!");
    }
}
```

Run and confirm output.

### 2.1 Write Your Own Variations

Add these to `main` (write them yourself):

**Exercise A – Print Even Numbers 2 to 20**

```java
System.out.println("Even numbers from 2 to 20:");
for (int i = 2; i <= 20; i += 2) {
    System.out.print(i + " ");
}
System.out.println();
```

**Exercise B – Factorial of a Number**

Still in `LoopPractice2.main`:

```java
int num = 5; // you can change this
int fact = 1;
for (int i = 1; i <= num; i++) {
    fact *= i; // fact = fact * i
}
System.out.println("Factorial of " + num + " = " + fact);
```

Concepts strengthened:

- Loop bounds (`i <= n`, `i < n`, etc.)
- Updating variables in the loop (`sum`, `fact`, etc.)
- Difference between `for` and `while` (for: counts; while: continue until condition fails)

---

## 3. Arrays: Basics & Syntax (30–45 min)

Arrays = fixed-length sequence of elements of the same type.

Create `ArrayBasics.java` in `week1.day2`:

```java
package week1.day2;

public class ArrayBasics {
    public static void main(String[] args) {
        // 1. Declaration + creation (default values)
        int[] arr = new int[5]; // length 5, all elements default to 0

        // Set values
        arr[0] = 10;
        arr[1] = 20;
        arr[2] = 30;
        arr[3] = 40;
        arr[4] = 50;

        // 2. Access elements
        System.out.println("First element: " + arr[0]);
        System.out.println("Last element: " + arr[arr.length - 1]);
        System.out.println("Array length: " + arr.length);

        // 3. Traversal with index-based for loop
        System.out.println("All elements with index-based for:");
        for (int i = 0; i < arr.length; i++) {
            System.out.println("Index " + i + ": " + arr[i]);
        }

        // 4. Traversal with enhanced for-each loop
        System.out.println("All elements with enhanced for:");
        for (int value : arr) {
            System.out.println(value);
        }

        // 5. Declare & initialize in one line
        int[] nums = {1, 2, 3, 4, 5};
        System.out.println("nums length = " + nums.length);
    }
}
```

Key points:

- Declaration:
  ```java
  int[] arr;     // preferred
  int arr2[];    // also valid (less common style)
  ```
- Creation with size:
  ```java
  arr = new int[5]; // indices: 0..4
  ```
- Direct initialization:
  ```java
  int[] nums = {1, 2, 3};
  ```
- Indexing is 0-based: valid indices are `0` to `length - 1`.
- `arr.length` gives the number of elements.

### 3.1 Mini Exercises (in `ArrayBasics.main`)

Add and implement:

**Exercise A – Modify & Print**

After you initialize `nums`:

```java
nums[0] = 100;
nums[nums.length - 1] = 500;

System.out.println("Modified nums:");
for (int i = 0; i < nums.length; i++) {
    System.out.println("Index " + i + ": " + nums[i]);
}
```

**Exercise B – Out-of-Bounds Experiment**

Temporarily (and deliberately) try:

```java
// Uncomment to see error:
// System.out.println(arr[5]);
```

- Run the program and observe the exception:
  - `ArrayIndexOutOfBoundsException`
- Then comment it back out.
- Lesson: never access index `< 0` or `>= arr.length`.

---

## 4. Array Methods: Sum, Max, and Basic Utilities (45–60 min)

Create `ArrayMethods.java` in `week1.day2`:

```java
package week1.day2;

public class ArrayMethods {

    // 1. Return the sum of elements in the array
    public static int sumArray(int[] arr) {
        int sum = 0;
        for (int i = 0; i < arr.length; i++) {
            sum += arr[i];
        }
        return sum;
    }

    // 2. Return the maximum element in the array
    public static int maxArray(int[] arr) {
        // Assume array has at least one element
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        return max;
    }

    // 3. (Optional) Return the minimum element in the array
    public static int minArray(int[] arr) {
        int min = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] < min) {
                min = arr[i];
            }
        }
        return min;
    }

    public static void main(String[] args) {
        int[] data = {5, 2, 9, 1, 7};

        int sum = sumArray(data);
        System.out.println("Sum of data = " + sum);

        int max = maxArray(data);
        System.out.println("Max of data = " + max);

        int min = minArray(data);
        System.out.println("Min of data = " + min);
    }
}
```

Run and ensure the outputs match your expectation.

### 4.1 New Method: Find Index of Target

Add to `ArrayMethods`:

```java
    // 4. Return index of target, or -1 if not found
    public static int findIndex(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                return i; // found at index i
            }
        }
        return -1; // not found
    }
```

In `main`:

```java
        int[] data = {5, 2, 9, 1, 7};
        // existing code...

        int idx1 = findIndex(data, 9);
        int idx2 = findIndex(data, 100);
        System.out.println("Index of 9: " + idx1);
        System.out.println("Index of 100: " + idx2);
```

Check outputs:
- Index of 9 should be the position of 9.
- Index of 100 should be -1.

This is a **linear search** – a very common pattern.

### 4.2 New Method: Reverse Into a New Array

Still in `ArrayMethods`:

```java
    // 5. Return a new array that is the reverse of arr
    public static int[] reverseArray(int[] arr) {
        int n = arr.length;
        int[] result = new int[n];
        for (int i = 0; i < n; i++) {
            result[i] = arr[n - 1 - i];
        }
        return result;
    }
```

In `main`:

```java
        int[] reversed = reverseArray(data);
        System.out.println("Reversed array:");
        for (int i = 0; i < reversed.length; i++) {
            System.out.print(reversed[i] + " ");
        }
        System.out.println();
```

Concepts reinforced:

- Array traversal patterns
- Using `arr.length`
- Creating and returning new arrays
- Thinking in indices (`n - 1 - i` pattern is very common)

---

## 5. Small Array Practice Set (20–30 min)

Create `ArrayPracticeDay2.java` in `week1.day2` and try to implement these **without** looking back at `ArrayMethods` right away. Then cross-check.

```java
package week1.day2;

public class ArrayPracticeDay2 {

    // 1. Compute average (as double)
    public static double average(int[] arr) {
        // TODO: implement
        return 0.0;
    }

    // 2. Count how many elements are greater than a given value x
    public static int countGreaterThan(int[] arr, int x) {
        // TODO: implement
        return 0;
    }

    // 3. Check if array is sorted in non-decreasing order
    public static boolean isSortedNonDecreasing(int[] arr) {
        // TODO: implement
        return false;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 2, 5, 7};

        System.out.println("Average: " + average(nums));
        System.out.println("Count > 3: " + countGreaterThan(nums, 3));
        System.out.println("Is sorted non-decreasing: " + isSortedNonDecreasing(nums));
    }
}
```

Try to fill in:

### 5.1 Suggested Implementations (Check After You Try)

```java
    public static double average(int[] arr) {
        if (arr.length == 0) return 0.0; // simple guard
        int sum = 0;
        for (int value : arr) {
            sum += value;
        }
        return (double) sum / arr.length;
    }

    public static int countGreaterThan(int[] arr, int x) {
        int count = 0;
        for (int value : arr) {
            if (value > x) {
                count++;
            }
        }
        return count;
    }

    public static boolean isSortedNonDecreasing(int[] arr) {
        // For each adjacent pair, check arr[i] <= arr[i+1]
        for (int i = 0; i + 1 < arr.length; i++) {
            if (arr[i] > arr[i + 1]) {
                return false;
            }
        }
        return true;
    }
```

If any of these felt difficult, mark them to review tomorrow.

---

## 6. Reflection & Self-Check (15–20 min)

Answer these without running code first:

1. How do you:
   - Declare an integer array `scores` of length 10?
   - Initialize an array `ints` with values `1, 3, 5` in a single line?
2. What is the difference between:
   ```java
   for (int i = 0; i < arr.length; i++) { ... }
   ```
   and
   ```java
   for (int value : arr) { ... }
   ```
   When would you prefer each?
3. Write the method header only for:
   - a method that returns `int`
   - is called `sumArray`
   - takes `int[] arr` as a parameter
4. Consider this code:
   ```java
   int[] a = {1, 2, 3};
   System.out.println(a[3]);
   ```
   - Will it compile?
   - What happens when it runs?
5. In words, describe what this loop does:
   ```java
   int max = arr[0];
   for (int i = 1; i < arr.length; i++) {
       if (arr[i] > max) {
           max = arr[i];
       }
   }
   ```

If any answer feels fuzzy, revisit the relevant code section.

---

## 7. Preview of Day 3

Tomorrow (Day 3), you will:

- Practice more array operations and patterns (prefix sums, search).
- Implement several array utility methods from scratch.
- Solve your **first full LeetCode-style problem** in Java (Two Sum) with both brute force and optimized HashMap approach.

If you’d like, I can next create a similarly detailed **Day 3 of Week 1** guide focusing on array practice and your first LeetCode problems.
