Below is an 8‑week, Java‑focused Data Structures & Algorithms study plan built around the 80/20 rule: we’ll focus on the “vital few” concepts that yield most of the benefit and are heavily represented on LeetCode.

**Assumptions**
- You know basic Java syntax (variables, loops, methods, classes).  
- You can spend ~1.5–2 hours per day, 5–6 days a week.  
- Goal: Be able to **understand problems, pick the right data structure / pattern, and implement solutions in Java**.

---

## Overview of the 8 Weeks (80/20 Focus)

**You’ll mainly master:**
1. Arrays & Strings (+ Two Pointers, Sliding Window)
2. Hash-based structures (HashMap, HashSet)
3. Linked Lists
4. Stack & Queue
5. Binary Search (on arrays, answers, boundaries)
6. Basic Sorting & Complexity
7. Trees & Binary Search Trees (BST)
8. Graph basics (BFS/DFS)
9. Recursion & Backtracking
10. Dynamic Programming (fundamentals)

We’ll mix **learning + coding** every week. For each topic, you’ll see:
- Core concept(s)
- What to study/implement
- LeetCode problems (approx. easy → medium → a bit harder)
- Key ideas reinforced

---

# Week 1 – Foundations, Arrays & Strings

### Goals
- Be comfortable with time/space complexity.
- Get fluent in Java array & String manipulation.
- Start reading and solving simple LeetCode problems.

---

### 1.1 Core Theory (Day 1–2)
**Study:**
- Big‑O notation:
  - Common complexities: O(1), O(log n), O(n), O(n log n), O(n²)
  - How loops and nested loops affect complexity
- Java basics you’ll use often:
  - Arrays (`int[]`, `int[][]`)
  - Strings (`String`, `StringBuilder`)
  - For/while loops, enhanced for loop
  - Basic I/O not required for LeetCode, but know how to write a `main` method

**Practice (No-code or light-code):**
- Look at pseudo-code and estimate time complexity.
- Write small functions: reverse array, count characters, etc.

---

### 1.2 Arrays & Strings (Day 3–6)

**Concepts:**
- Traversing arrays
- In-place modification vs creating new arrays
- Basic String operations: substring, charAt, length, toCharArray
- Two Pointers (intro: left/right index moving towards center or along array)

**Implement yourself (from scratch):**
- Reverse an array
- Reverse a string
- Find max/min in an array
- Check if a string is palindrome (two pointers)

---

### 1.3 LeetCode Practice – Arrays & Strings (Day 3–7)

Start from easy to build confidence. Focus on understanding the **why** of solutions.

**Beginner – Arrays & Strings**
1. **Two Sum** (`#1`, Easy)  
   - Key Ideas: HashMap for complement lookup, time complexity O(n).
2. **Best Time to Buy and Sell Stock** (`#121`, Easy)  
   - Key Ideas: One pass, track min price and max profit.
3. **Valid Palindrome** (`#125`, Easy)  
   - Key Ideas: Two pointers, character checks.
4. **Merge Sorted Array** (`#88`, Easy)  
   - Key Ideas: Merge two sorted arrays from the back using pointers.

**Stretch / Medium Intro:**
5. **Longest Substring Without Repeating Characters** (`#3`, Medium)  
   - Key Ideas: Sliding window, HashSet/HashMap.
6. **Container With Most Water** (`#11`, Medium)  
   - Key Ideas: Two pointers, area calculation.

---

### Key Reinforcements This Week
- Big‑O reasoning.
- Basic array/string processing.
- Two Pointers intro.
- Getting used to LeetCode interface and reading constraints.

---

# Week 2 – Hashing + More Two Pointers & Sliding Window

### Goals
- Understand and use `HashMap`, `HashSet`.
- Solidify Two Pointers and Sliding Window patterns (core LeetCode patterns).

---

### 2.1 HashMap & HashSet in Java (Day 1–2)

**Study:**
- `HashMap<K,V>` operations: put, get, containsKey, remove, iteration.
- `HashSet<E>` operations: add, contains, remove.
- Hashing conceptually: average O(1), worst O(n).

**Implement:**
- Frequency count: given an array, return map of `value → count`.
- First non-repeating character in a string using HashMap.

---

### 2.2 Two Pointers & Sliding Window (Day 3–4)

**Concepts:**
- Two Pointers:
  - Opposite ends of array (e.g., sum, palindrome).
  - Same direction pointers (fast/slow for linked lists; next week).
- Sliding Window:
  - Fixed window size.
  - Variable window size (expand when condition not met, shrink when it is).

---

### 2.3 LeetCode Practice – Hash & Sliding Window (Day 3–7)

**Beginner / Easy:**
1. **Valid Anagram** (`#242`, Easy)  
   - HashMap or array for char counts.
2. **Contains Duplicate** (`#217`, Easy)  
   - HashSet to detect duplicates.
3. **Group Anagrams** (`#49`, Medium but very common)  
   - Map from “signature” (sorted string or char count) → list of words.

**Sliding Window / Two Pointers:**
4. **Longest Substring Without Repeating Characters** (`#3`, Medium, revisit)  
   - Use sliding window and HashMap for char indices.
5. **Minimum Size Subarray Sum** (`#209`, Medium)  
   - Variable sliding window for minimal length.
6. **Move Zeroes** (`#283`, Easy)  
   - Two pointers to shift non-zero elements forward.

**Stretch:**
7. **Permutation in String** (`#567`, Medium)  
   - Sliding window + frequency arrays.

---

### Key Reinforcements This Week
- HashMap / HashSet become “go-to” tools.
- Sliding Window as a reusable template.
- Recognize patterns in problems (duplicates, subarray length, substring uniqueness).

---

# Week 3 – Linked Lists, Stack & Queue, Fast/Slow Pointers

### Goals
- Understand pointers/references in Java.
- Manipulate linked lists (head, next pointers).
- Use stacks/queues to solve typical problems.

---

### 3.1 Linked List Basics (Day 1–3)

**Study:**
- Singly Linked List structure (`ListNode { int val; ListNode next; }`).
- How references work (no copying nodes, just pointers).
- Common operations: insert at head, delete node, reverse list.

**Implement yourself:**
- Define `ListNode` class.
- Build a linked list from array.
- Reverse linked list iteratively.

---

### 3.2 Stacks & Queues (Day 3–4)

**Study:**
- Stack (LIFO): `push`, `pop`, `peek`. Use `java.util.Stack` or `Deque`.
- Queue (FIFO): `offer`, `poll`, `peek`. Use `LinkedList` or `ArrayDeque`.

**Implement / Use:**
- Use a stack to reverse a string.
- Use a queue to simulate a simple line (enqueue/dequeue).

---

### 3.3 Fast & Slow Pointers (Day 4–5)

- Typical uses: detect cycles, find middle node.
- Move fast pointer 2 steps, slow pointer 1 step.

---

### 3.4 LeetCode Practice – Linked List & Stack/Queue (Day 5–7)

**Linked List – Starter:**
1. **Reverse Linked List** (`#206`, Easy)  
   - Iterative reverse; practice pointer manipulation.
2. **Merge Two Sorted Lists** (`#21`, Easy)  
   - Merge like merge step in merge sort using pointers.
3. **Middle of the Linked List** (`#876`, Easy)  
   - Fast/slow pointer pattern.

**Cycle & More:**
4. **Linked List Cycle** (`#141`, Easy)  
   - Fast/slow pointers to detect cycle.
5. **Remove Nth Node From End of List** (`#19`, Medium)  
   - Two pointers; distance between them is `n`.

**Stack / Queue:**
6. **Valid Parentheses** (`#20`, Easy)  
   - Use stack to validate bracket sequence.
7. **Min Stack** (`#155`, Easy/Medium)  
   - Stack that supports `getMin()` in O(1).

**Stretch:**
8. **Palindrome Linked List** (`#234`, Easy/Medium)  
   - Find middle, reverse second half, compare.

---

### Key Reinforcements This Week
- Comfort with references/pointers in Java.
- Implementing common linked list operations.
- Using stack/queue as generic tools for various problems.

---

# Week 4 – Binary Search, Sorting, & Problem Patterns

### Goals
- Master binary search implementations and patterns.
- Understand basic sorting and where it appears in problems.
- Apply binary search not only on arrays but also on solution space (answers).

---

### 4.1 Sorting & Complexity (Day 1–2)

**Study:**
- Basic sorting algorithms concepts:
  - Selection sort, insertion sort (for understanding).
  - Quick sort and merge sort (high-level idea).
- Java built-in sorting:
  - `Arrays.sort()`, `Collections.sort()` and time complexity O(n log n).
- When sorting helps:
  - Two pointers on sorted array.
  - Greedy choices.

---

### 4.2 Binary Search (Day 2–4)

**Patterns:**
- Classic binary search (find target in sorted array).
- Variants:
  - Find leftmost or rightmost occurrence.
  - Search insert position.
  - Binary search on answer (e.g., minimal capacity, minimal time).

---

### 4.3 LeetCode Practice – Binary Search & Sorting (Day 4–7)

**Binary Search Basics:**
1. **Binary Search** (`#704`, Easy)  
   - Implement standard binary search.
2. **Search Insert Position** (`#35`, Easy)  
   - Variant returning index where target would be inserted.
3. **First Bad Version** (`#278`, Easy)  
   - Binary search on an abstract condition.

**On Rotated Arrays:**
4. **Search in Rotated Sorted Array** (`#33`, Medium)  
   - Recognize which half is sorted and adjust binary search.

**Binary Search on Answer:**
5. **Koko Eating Bananas** (`#875`, Medium)  
   - Binary search on eating speed (answer space).
6. **Capacity To Ship Packages Within D Days** (`#1011`, Medium)  
   - Binary search on capacity; check feasibility.

**Sorting + Two Pointers:**
7. **3Sum** (`#15`, Medium)  
   - Sort + two pointers pattern.
8. **Merge Intervals** (`#56`, Medium)  
   - Sort by start time + merge overlapping.

---

### Key Reinforcements This Week
- Binary search templates: careful with `mid`, `left`, `right` updates.
- Recognize when problem asks for “min/max feasible value” → often binary search on answer.
- Using sorting to simplify problems.

---

# Week 5 – Trees & Binary Search Trees (BST)

### Goals
- Understand tree structure, traversal methods.
- Use recursion comfortably.
- Solve common tree problems (height, traversal, path sums).

---

### 5.1 Tree Basics (Day 1–2)

**Study:**
- Binary tree vs Binary Search Tree (BST).
- Node definition: `TreeNode { int val; TreeNode left; TreeNode right; }`.
- Traversals:
  - Preorder (root-left-right)
  - Inorder (left-root-right)
  - Postorder (left-right-root)
  - Level-order (BFS using queue)

**Implement:**
- Recursive traversals (print values).
- Compute tree height.

---

### 5.2 BST Properties (Day 3)

- Inorder traversal of BST is sorted.
- Searching/inserting in BST (recursive & iterative).

---

### 5.3 LeetCode Practice – Trees (Day 3–7)

**Tree Basics (Easy):**
1. **Maximum Depth of Binary Tree** (`#104`, Easy)  
   - Simple recursion.
2. **Same Tree** (`#100`, Easy)  
   - Recursively compare structure and values.
3. **Invert Binary Tree** (`#226`, Easy)  
   - Swap left/right recursively.

**Traversal / BFS:**
4. **Binary Tree Level Order Traversal** (`#102`, Medium)  
   - Use queue (BFS) to traverse level by level.
5. **Symmetric Tree** (`#101`, Easy/Medium)  
   - Recursive mirror check or BFS.

**BST-specific:**
6. **Validate Binary Search Tree** (`#98`, Medium)  
   - Use min/max bounds or inorder traversal.
7. **Lowest Common Ancestor of a BST** (`#235`, Easy/Medium)  
   - Use BST property; move left/right depending on values.

**Path / Sum-type (Stretch):**
8. **Path Sum** (`#112`, Easy)  
   - Recursion with remaining sum.
9. **Path Sum II** (`#113`, Medium)  
   - Track current path; backtracking.

---

### Key Reinforcements This Week
- Recursion pattern: base case + recursive calls.
- Moving from “printing traversal” to solving more complex tree queries.
- Understanding how BST property simplifies logic.

---

# Week 6 – Graph Basics & More Recursion / Backtracking

### Goals
- Understand graphs as adjacency lists.
- Learn BFS/DFS patterns and when to use each.
- Get exposure to backtracking (for combinatorial problems).

---

### 6.1 Graph Fundamentals (Day 1–3)

**Study:**
- Graph representations:
  - Adjacency list using `List<List<Integer>>` or `Map<Integer, List<Integer>>`.
- Directed vs undirected graphs.
- BFS:
  - Use queue, track visited.
- DFS:
  - Recursive or using stack, track visited.

**Implement small examples:**
- Simple BFS/DFS on a small graph.

---

### 6.2 Backtracking Basics (Day 3–4)

**Concepts:**
- Decision tree: choose/add → recurse → un-choose/remove.
- Use arrays or lists to build candidates.
- Base case: when combination/permutation length is enough or sum is met.

---

### 6.3 LeetCode Practice – Graph & Backtracking (Day 4–7)

**Graph / BFS / DFS:**
1. **Number of Islands** (`#200`, Medium)  
   - Grid as implicit graph, DFS/BFS to mark visited.
2. **Max Area of Island** (`#695`, Medium)  
   - Very similar; count size.
3. **Flood Fill** (`#733`, Easy/Medium)  
   - DFS/BFS from a starting pixel.
4. **Clone Graph** (`#133`, Medium, stretch)  
   - Use HashMap to clone nodes using DFS/BFS.

**Backtracking:**
5. **Subsets** (`#78`, Medium)  
   - Generate all subsets using recursion.
6. **Combination Sum** (`#39`, Medium)  
   - Backtracking with remaining sum.
7. **Permutations** (`#46`, Medium)  
   - Backtracking with used/not-used markers.

---

### Key Reinforcements This Week
- Recognizing grid problems as graph problems.
- Using DFS/BFS templates.
- Understanding typical backtracking “template”:  
  choose → recurse → un-choose.

---

# Week 7 – Dynamic Programming (DP) Fundamentals

### Goals
- Understand overlapping subproblems and optimal substructure.
- Learn bottom-up DP on 1D & 2D arrays.
- Solve common DP problems: sequences, knapsack-like, grid paths.

---

### 7.1 DP Concepts (Day 1–2)

**Study:**
- When DP applies:
  - Problem can be broken into subproblems whose solutions can be reused.
- Approaches:
  - Top-down with memoization (recursion + HashMap/array).
  - Bottom-up tabulation.
- Typical DP states: `dp[i]`, `dp[i][j]` etc.

---

### 7.2 Classic DP Problems (Day 2–7)

**Start with simple 1D DP:**
1. **Climbing Stairs** (`#70`, Easy)  
   - `dp[i] = dp[i-1] + dp[i-2]`.
2. **House Robber** (`#198`, Medium)  
   - `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`.

**Subsequence/string DP:**
3. **Longest Increasing Subsequence** (`#300`, Medium)  
   - `dp[i]` = LIS ending at `i`; O(n²) DP approach.
4. **Longest Common Subsequence** (`#1143`, Medium)  
   - 2D DP; `dp[i][j]` based on `text1[i-1]` and `text2[j-1]`.

**Grid DP:**
5. **Unique Paths** (`#62`, Medium)  
   - `dp[i][j] = dp[i-1][j] + dp[i][j-1]`.
6. **Minimum Path Sum** (`#64`, Medium)  
   - Similar but with costs.

**Stretch:**
7. **Coin Change** (`#322`, Medium)  
   - `dp[amount]` = min coins to make that amount.

---

### Key Reinforcements This Week
- Turning a recursive idea into DP state and recurrence.
- Starting from base cases and building up.
- Distinguishing between subsequence, substring, combination problems.

---

# Week 8 – Integration, Patterns, and Timed Practice

### Goals
- Combine all concepts.
- Practice recognizing problem patterns quickly.
- Simulate “interview-style” LeetCode sessions.

---

### 8.1 Pattern Review (Day 1–3)

Revisit each “big pattern” with 1–2 representative problems:

1. **Two Pointers / Sliding Window**
   - Re-solve (without looking at previous code)  
     - `#3 Longest Substring Without Repeating Characters`  
     - `#11 Container With Most Water`  

2. **HashMap / HashSet**
   - Re-solve:  
     - `#1 Two Sum`  
     - `#49 Group Anagrams`

3. **Linked List**
   - Re-solve:  
     - `#206 Reverse Linked List`  
     - `#141 Linked List Cycle` / `#19 Remove Nth Node from End`

4. **Binary Search**
   - Re-solve:  
     - `#704 Binary Search`  
     - `#33 Search in Rotated Sorted Array`  
     - `#875 Koko Eating Bananas`

5. **Tree / BST**
   - Re-solve:  
     - `#104 Maximum Depth of Binary Tree`  
     - `#98 Validate BST`  

6. **Graph / DFS/BFS**
   - Re-solve:  
     - `#200 Number of Islands`

7. **Backtracking**
   - Re-solve:  
     - `#78 Subsets` or `#46 Permutations`

8. **DP**
   - Re-solve:  
     - `#70 Climbing Stairs`  
     - `#198 House Robber`

---

### 8.2 New Mixed Problems (Day 3–6)

Pick 1–2 per day; try to solve in **<40 minutes** each:

1. **Medium Mix:**
   - `#56 Merge Intervals` (sort + merge)  
   - `#215 Kth Largest Element in an Array` (heap or quickselect, stretch)  
   - `#79 Word Search` (backtracking on a grid)  
   - `#49 Group Anagrams` (hashing, if not solid)

2. **Harder Medium / Light Hard (Stretch):**
   - `#560 Subarray Sum Equals K` (prefix sums + HashMap)  
   - `#322 Coin Change` (DP, if you skipped it before)  
   - `#207 Course Schedule` (graph + topological sort concept, stretch)

---

### 8.3 Simulated “Interview Day” (Day 7)

- Pick 2 problems you **haven’t** done, ideally from:
  - Arrays/Strings
  - Trees/Graphs
  - DP

For each:
1. Spend 5–10 minutes only on reading and designing:
   - Restate the problem in your own words.
   - Identify which pattern it might be.
   - Write out example(s) by hand.
2. Then code without switching tabs to the solution.
3. After coding, compare to the discussion / solution:
   - What was different?
   - Did you choose the right data structure / pattern?
   - Where did you get stuck?

---

# How to Think & Learn Independently

1. **Always try on your own first (15–25 min)** before reading hints.
2. When stuck, ask yourself:
   - Is there a pattern I know (two pointers, sliding window, hashing, recursion, DP)?
   - Can I reduce the problem to a simpler known problem?
3. After reading a solution, **implement from scratch again later in the week**.
4. Keep a **“pattern notebook”**:
   - For each solved problem, note:
     - Problem type (array, tree, DP, etc.)
     - Pattern used
     - Time/space complexity
     - A 1–2 line summary of the key idea

---

# Summary of the 20% Core You’re Mastering

If you complete this plan, you’ll be solid on:

- **Data Structures:** arrays, strings, HashMap/HashSet, linked lists, stack, queue, binary trees/BST, basic graphs.
- **Patterns:** two pointers, sliding window, fast/slow pointers, binary search (on arrays & answers), recursion, DFS/BFS, backtracking, foundational DP.
- **Java skills:** implementing these patterns idiomatically with Java collections and classes.

If you’d like, I can next:
- Turn this into a weekly checklist (with boxes and daily tasks), or  
- Provide skeleton Java templates for each major pattern (binary search, BFS, DP, etc.) for you to fill in.
