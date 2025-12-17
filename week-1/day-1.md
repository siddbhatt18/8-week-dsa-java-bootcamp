### Day 1 (Week 1) – Java Setup & Core Foundations

**High‑level goals for Day 1**

1. Set up your Java environment and verify you can run code.  
2. Learn the absolute core Java syntax you’ll use in LeetCode:  
   - `main` method, printing output  
   - variables & primitive types  
   - `if/else`  
3. Practice by writing a few tiny programs so the syntax feels natural.

Target time: ~2–3 hours.  
If you have less time, do the tasks marked with ⭐ first.

---

## 0. Mindset & Workspace (5–10 min)

**Objective:** Put yourself in a “daily coding” mode.

- Decide:
  - What time of day you’ll usually code (e.g., 8–9 pm).
  - Where you’ll code (desk, quiet space).
- Create a folder on your machine: `~/dsa-java` (or `C:\dsa-java` on Windows).  
- Keep a simple text file or notes app titled **“DSA Learning Log”** where you’ll note:
  - What you practiced each day.
  - Any “aha” moments or confusions.

---

## 1. Environment Setup (30–45 min) ⭐

**Objective:** Install tools and run your first Java program.

### 1.1 Install Java (JDK)

- Install **JDK 17 or later**:
  - From Oracle (JDK) or AdoptOpenJDK (Temurin).
- After installation, verify in terminal / Command Prompt:
  ```bash
  java -version
  ```
  You should see something like `17.x` printed.

### 1.2 Install IDE

Use **one IDE** and stick to it:

- Recommended: **IntelliJ IDEA Community Edition** (free).  
  Alternative: VS Code + Java extension.

### 1.3 Create Your Project & First Class

In IntelliJ:

1. Create **New Project** → Language: Java → JDK: 17+ → Name: `dsa-java`.
2. Inside `src`, create a package: `week1.day1`.
3. Create a new Java class: `HelloWorld`.

Paste:

```java
package week1.day1;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, DSA in Java!");
    }
}
```

- Click **Run**.  
  - Expected output: `Hello, DSA in Java!`

If it runs, your tooling is ready.

**Checkpoint:**  
You can create a class, write a `main` method, and run it.

---

## 2. Java Syntax Foundations (60–75 min) ⭐

**Objective:** Understand and practice core building blocks:

- Variables & types  
- Basic operators  
- `if/else` logic  
- Printing results

Create a new class: `week1.day1.BasicsPractice`.

### 2.1 Variables & Types (20–25 min)

Learn/recall the key **primitive types**:

- `int` – integers (e.g., 1, 10, -5)
- `long` – large integers
- `double` – decimals (e.g., 3.14)
- `boolean` – `true` or `false`
- `char` – single character (e.g., `'a'`)
- `String` – sequence of characters (not primitive, but essential)

Example in `main`:

```java
public static void main(String[] args) {
    int age = 25;
    double height = 1.75;
    boolean isStudent = true;
    char initial = 'A';
    String name = "Alice";

    System.out.println("Age: " + age);
    System.out.println("Height: " + height);
    System.out.println("Is student? " + isStudent);
    System.out.println("Initial: " + initial);
    System.out.println("Name: " + name);
}
```

**Mini‑Exercise A:**

In `BasicsPractice.main`:

1. Declare:
   ```java
   int a = 10;
   int b = 3;
   ```
2. Print:
   - `a + b`
   - `a - b`
   - `a * b`
   - `a / b`  (integer division)
   - `a % b`  (remainder)

Expected:  
- `10 / 3` → `3`  
- `10 % 3` → `1`

This gets you used to arithmetic operators.

### 2.2 Conditionals (if/else) (20–25 min)

Example:

```java
int age = 20;

if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Minor");
}
```

**Mini‑Exercise B: Even or Odd**

Still in `BasicsPractice`:

1. Hardcode an integer:
   ```java
   int n = 17;  // try other numbers too
   ```
2. If `n` is divisible by 2, print `"Even"`, else `"Odd"`.

Skeleton:

```java
int n = 17;
if (n % 2 == 0) {
    System.out.println("Even");
} else {
    System.out.println("Odd");
}
```

**Mini‑Exercise C: Score to Grade (simple)**

- Hardcode an integer `score` between 0 and 100.
- Print:
  - `"Pass"` if `score >= 50`
  - `"Fail"` otherwise

Optional extension:
- If `score >= 80`: `"Grade A"`  
- Else if `score >= 60`: `"Grade B"`  
- Else `"Grade C"`  

This builds comfort with chained `if/else if/else`.

---

## 3. Methods (Functions) in Java (30–40 min) ⭐

**Objective:** Learn to define and call your own methods.  
This is critical: every LeetCode solution will be a method.

Create a new class: `week1.day1.MethodsPractice`.

### 3.1 Understanding Method Signature

Typical form:

```java
public static ReturnType methodName(ParameterType1 p1, ParameterType2 p2) {
    // body
    return someValue; // if ReturnType is not void
}
```

Example (add two numbers):

```java
public class MethodsPractice {

    public static void main(String[] args) {
        int result = add(3, 5);
        System.out.println("3 + 5 = " + result);
    }

    public static int add(int x, int y) {
        return x + y;
    }
}
```

### 3.2 Method Exercises

**Exercise 1: `square` method**

Add to `MethodsPractice`:

```java
public static int square(int n) {
    // return n multiplied by itself
    return n * n;
}
```

In `main`:

```java
int s1 = square(4);  // expect 16
int s2 = square(-3); // expect 9
System.out.println("square(4) = " + s1);
System.out.println("square(-3) = " + s2);
```

**Exercise 2: `isPositive` method**

```java
public static boolean isPositive(int n) {
    // return true if n > 0, else false
    return n > 0;
}
```

In `main`:

```java
System.out.println("isPositive(5): " + isPositive(5));   // true
System.out.println("isPositive(0): " + isPositive(0));   // false
System.out.println("isPositive(-2): " + isPositive(-2)); // false
```

**Exercise 3: Combine methods**

Add:

```java
public static int sumOfSquares(int a, int b) {
    return square(a) + square(b);
}
```

In `main`:

```java
int ss = sumOfSquares(2, 3); // 4 + 9 = 13
System.out.println("sumOfSquares(2, 3) = " + ss);
```

This shows how methods can call other methods, just like in LeetCode where helper functions call one another.

---

## 4. Structured Practice Block (30–40 min)

**Objective:** Solidify what you learned with slightly more “problem‑like” tasks.

Stay in `MethodsPractice` or create `week1.day1.PracticeSet1`.

### Problem 1: Absolute Value

Write a method:

```java
public static int absolute(int n) {
    // if n is negative, return -n; otherwise return n
}
```

Test in `main` with `-5`, `0`, `7`.

### Problem 2: Max of Two

```java
public static int max(int a, int b) {
    // return bigger of a and b
}
```

Test: `max(3, 10)`, `max(-1, -5)`.

### Problem 3: Compare Two Numbers Verbally

Write:

```java
public static void compare(int a, int b) {
    // print "a is greater", "b is greater", or "a and b are equal"
}
```

In `main`:

```java
compare(5, 3);
compare(2, 2);
compare(-1, 10);
```

Focus on:

- Writing a clear method signature.
- Using `if`, `else if`, `else`.
- Calling the method from `main`.

---

## 5. Quick Self‑Check & Reflection (10–15 min) ⭐

**Objective:** Lock in what you learned and identify anything unclear.

In your **DSA Learning Log**, answer briefly:

1. Can I:
   - Write the signature of a `main` method from memory?
   - Declare an `int` and a `String` without looking it up?
   - Write a simple `if/else` to check if a number is even?

2. Write (from memory, in your notes or a scratch file) the skeleton of a Java program:

```java
public class Test {
    public static void main(String[] args) {
        int x = 10;
        if (x > 0) {
            System.out.println("Positive");
        } else {
            System.out.println("Non-positive");
        }
    }
}
```

Try to do it without copying; then compare to correct syntax.

3. Note **one thing that confused you today** (e.g., `static`, `main` arguments, etc.).  
   - This will guide what you quickly review tomorrow before moving on.

---

## Optional Stretch (If You Have Extra Time)

If you finished early and feel comfortable:

1. Watch a short 10–15 min video on “Java basics” (variables, if/else, methods).  
2. Try writing a **guessing game** (no input, just hardcoded):
   - Hardcode `int secret = 7;`
   - Hardcode `int guess = 5;`
   - If guess < secret → print `"Too low"`, if > → `"Too high"`, else `"Correct"`.

This mimics simple logic flow you’ll later use in more complex problems.

---

## Summary of Day 1 Deliverables

By the end of Day 1, you should have:

- Project `dsa-java` with:
  - `week1.day1.HelloWorld`
  - `week1.day1.BasicsPractice`
  - `week1.day1.MethodsPractice` (or similar)
- You can:
  - Run Java code from the IDE.
  - Declare variables and print them.
  - Use `if/else` to make decisions.
  - Write and call simple methods (e.g., `square`, `isPositive`).

If you want, next I can create a similarly detailed **Day 2 plan** (loops + intro to arrays) customized to how Day 1 felt for you.
