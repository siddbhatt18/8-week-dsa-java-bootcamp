### Week 1 – Day 1  
**Theme:** Environment Setup + Java Syntax Foundations  
**Goal for today:**  
- Set up your Java dev environment.  
- Understand the structure of a basic Java program.  
- Get comfortable with variables, data types, conditionals, and very simple I/O.  
- Write and run a few small programs on your own.

---

## 0. Prerequisites & Mindset (5–10 min)

- You do **not** need prior Java experience.
- Today is about:
  - Installing tools
  - Running your first programs
  - Writing basic Java code independently

Keep the pace: if something feels slow, that’s normal for Day 1.

---

## 1. Environment Setup (30–45 min)

### 1.1 Install Java (JDK)

1. Install **JDK 17 or later**:
   - Go to: https://adoptium.net or Oracle’s JDK page.
   - Download the installer for your OS (Windows/Mac/Linux).
   - Follow the installer steps (next/next/finish).
2. Verify installation:
   - Open a terminal / command prompt:
     - On Windows: `Win + R` → type `cmd`  
     - On Mac: open Terminal
   - Run:
     ```bash
     java -version
     ```
   - You should see something like:
     ```
     openjdk version "17.0.x" ...
     ```

### 1.2 Install IDE

Using **IntelliJ IDEA Community** (recommended):

1. Download from: https://www.jetbrains.com/idea/download
2. Install and open IntelliJ.
3. Create a new project:
   - Click **New Project**
   - Select **Java**
   - Use the JDK you installed (e.g., 17)
   - Project name: `dsa-java-learning`
   - Finish.

### 1.3 Create Your First Class

1. In IntelliJ:
   - Right-click `src` → **New → Package** → name: `week1.day1`
   - Right-click `week1.day1` → **New → Java Class** → name: `HelloWorld`
2. Paste and run:

```java
package week1.day1;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, DSA in Java!");
    }
}
```

- Click the green “Run” arrow next to `main`.
- Confirm: console prints `Hello, DSA in Java!`.

If something fails, spend time troubleshooting here. Running code successfully is critical.

---

## 2. Java Program Structure & Types (45–60 min)

### 2.1 Understand Basic Structure

Key components:

```java
public class HelloWorld {
    public static void main(String[] args) {
        // This is where the program starts
        System.out.println("Hello!");
    }
}
```

- `public class HelloWorld` — class definition, file name must match class.
- `public static void main(String[] args)` — entry point of the program.
- Inside `main` is where you write the code that runs first.

### 2.2 Primitive Types & Variables

Create `BasicsPractice.java`:

```java
package week1.day1;

public class BasicsPractice {
    public static void main(String[] args) {
        // Step 1: Declare variables
        int age = 25;
        long bigNumber = 1_000_000_000L;
        double height = 1.75;
        boolean isStudent = true;
        char grade = 'A';

        // Step 2: Print them
        System.out.println("Age: " + age);
        System.out.println("Big number: " + bigNumber);
        System.out.println("Height: " + height);
        System.out.println("Is student: " + isStudent);
        System.out.println("Grade: " + grade);

        // Step 3: Reassign and print
        age = 30;
        System.out.println("Updated age: " + age);
    }
}
```

Run and observe:

- Understand that **variables store values** you can read or change.
- Primitive types you must know:
  - `int` – integers in typical LC problems
  - `long` – large integers
  - `double` – decimal numbers
  - `boolean` – `true` / `false`
  - `char` – single character

### 2.3 Simple Expressions & Operators

Extend `BasicsPractice.main` with:

```java
int a = 10;
int b = 3;

System.out.println("a + b = " + (a + b));
System.out.println("a - b = " + (a - b));
System.out.println("a * b = " + (a * b));
System.out.println("a / b = " + (a / b));   // integer division
System.out.println("a % b = " + (a % b));   // remainder (mod)
```

Mentally predict outputs before running:
- `a / b` will be `3` (not `3.3333`), because both are `int`.

---

## 3. Conditionals (`if/else`) (30–45 min)

Create `ConditionalsPractice.java`:

```java
package week1.day1;

public class ConditionalsPractice {
    public static void main(String[] args) {
        int number = 7;

        if (number % 2 == 0) {
            System.out.println(number + " is Even");
        } else {
            System.out.println(number + " is Odd");
        }

        int age = 20;
        if (age >= 18) {
            System.out.println("Adult");
        } else {
            System.out.println("Minor");
        }

        int score = 85;
        if (score >= 90) {
            System.out.println("Grade: A");
        } else if (score >= 80) {
            System.out.println("Grade: B");
        } else {
            System.out.println("Grade: C or lower");
        }
    }
}
```

Key ideas:

- Condition in parentheses `()` must be boolean (`true`/`false`).
- Common comparisons:
  - `==` (equal), `!=` (not equal), `>`, `<`, `>=`, `<=`
- Logical operators:
  - `&&` (and), `||` (or), `!` (not)

**Mini Exercise 1 (write and run yourself):**  
In `ConditionalsPractice.main`, add:

- A variable `int temperature = 30;`
- If `temperature > 25`, print `"Hot"`, else print `"Cold"`.

---

## 4. Intro to Loops (`for`) (30–45 min)

You’ll use loops constantly, so start early.

Create `LoopPractice.java`:

```java
package week1.day1;

public class LoopPractice {
    public static void main(String[] args) {
        // For loop: print 1 to 5
        for (int i = 1; i <= 5; i++) {
            System.out.println("i = " + i);
        }

        // Sum from 1 to 10
        int sum = 0;
        for (int i = 1; i <= 10; i++) {
            sum = sum + i;  // or sum += i;
        }
        System.out.println("Sum from 1 to 10 = " + sum);
    }
}
```

Understand the `for` loop structure:

```java
for (initialization; condition; update) {
    // body
}
```

- Initialization: runs once (e.g., `int i = 1`)
- Condition: checked each time before body (loop runs while `true`)
- Update: runs after each iteration (e.g., `i++`)

**Mini Exercise 2:**  
In `LoopPractice.main`:

- Print all even numbers from 2 to 20 using a `for` loop.

---

## 5. Methods (Functions) Basics (30–45 min)

Methods let you **reuse** logic and keep code organized.

Create `MethodsPractice.java`:

```java
package week1.day1;

public class MethodsPractice {

    // Method that takes two ints and returns their sum
    public static int add(int x, int y) {
        return x + y;
    }

    // Method that takes an int and returns its square
    public static int square(int n) {
        return n * n;
    }

    // Method that returns true if n is positive, else false
    public static boolean isPositive(int n) {
        return n > 0;
    }

    public static void main(String[] args) {
        int result1 = add(3, 5);
        System.out.println("add(3, 5) = " + result1);

        int result2 = square(4);
        System.out.println("square(4) = " + result2);

        System.out.println("isPositive(10) = " + isPositive(10));
        System.out.println("isPositive(-3) = " + isPositive(-3));
    }
}
```

Key parts of a method:

```java
public static <return_type> <name>(<parameters>) {
    // body
    return <value_of_return_type>;
}
```

- `public static` — for now, use this pattern so you can call methods from `main`.
- Return types:
  - `int`, `boolean`, etc.
  - If a method returns nothing, use `void`.

**Mini Exercise 3:**  
Inside `MethodsPractice`:

1. Add a method:
   ```java
   public static int max(int a, int b) {
       // return the larger of a and b
   }
   ```
2. Call it from `main` and print:
   - `max(10, 20)`
   - `max(-5, -2)`

---

## 6. Small End‑of‑Day Tasks (30–45 min)

These are meant to reinforce everything from today.

### Task A – Even/Odd Checker as a Method

Create `EvenOddMethod.java`:

```java
package week1.day1;

public class EvenOddMethod {

    public static boolean isEven(int n) {
        return n % 2 == 0;
    }

    public static void main(String[] args) {
        int x = 7;
        if (isEven(x)) {
            System.out.println(x + " is even");
        } else {
            System.out.println(x + " is odd");
        }

        int y = 12;
        if (isEven(y)) {
            System.out.println(y + " is even");
        } else {
            System.out.println(y + " is odd");
        }
    }
}
```

You’ve combined:
- Methods
- Conditionals
- Arithmetic operators

### Task B – Simple “Calculator” in `main`

In a new file `SimpleCalculator.java`:

```java
package week1.day1;

public class SimpleCalculator {

    public static void main(String[] args) {
        int a = 8;
        int b = 2;

        System.out.println("a = " + a + ", b = " + b);
        System.out.println("a + b = " + (a + b));
        System.out.println("a - b = " + (a - b));
        System.out.println("a * b = " + (a * b));
        System.out.println("a / b = " + (a / b));
    }
}
```

Change `a` and `b` to see different results.

---

## 7. Quick Self‑Check (10–15 min)

Without looking at your code, answer (on paper or in a note):

1. How do you write the `main` method signature in Java?
2. How do you declare:
   - An integer variable named `count` with initial value 0?
   - A boolean variable named `flag` with value `true`?
3. What does this print?
   ```java
   int x = 5;
   int y = 2;
   System.out.println(x / y);
   System.out.println(x % y);
   ```
4. Write a simple `if/else` that prints `"Positive"` if `n > 0`, otherwise `"Non-positive"`.
5. Write the skeleton of a method that:
   - Is called `triple`
   - Takes an `int n`
   - Returns `3 * n`

If you struggle with any of these, revisit the corresponding section.

---

## 8. What’s Next (Preview of Day 2)

On **Day 2**, you will:

- Deepen loop practice (especially `for` and `while`).
- Learn how to create and use **arrays** in Java.
- Write methods that take arrays as parameters (e.g., sum, max).

If you’d like, I can now generate a similar detailed, structured guide for **Day 2 of Week 1**, focusing on loops and array basics.
