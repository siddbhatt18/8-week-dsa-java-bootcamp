Below is an 8‑week, Java‑focused DSA roadmap built around the “80‑20” principle: we’ll focus on the small set of concepts and patterns that unlock a large portion of LeetCode (and interview) problems.

**Assumptions:**
- You know basic Java syntax (variables, loops, methods, classes). If not, spend 1–2 days upfront reviewing.
- Time: ~1.5–2 hours/day, 5–6 days/week. Adjust pace as needed.
- Tools: IntelliJ/Eclipse or VS Code, LeetCode, and a notebook for hand‑writing ideas.

---

## Overview of the Core 20%

These are the “high‑leverage” topics we’ll hit repeatedly:

1. **Arrays & Strings + Two Pointers + Prefix sums**
2. **Hashing (HashMap, HashSet)**
3. **Stacks & Queues + Monotonic stacks/queues**
4. **Linked Lists**
5. **Binary Search (on array & on answer)**
6. **Basic Sorting + custom comparators**
7. **Trees & Binary Search Trees (DFS, BFS, recursion)**
8. **Heaps / PriorityQueue**
9. **Basic Dynamic Programming (1D and simple 2D)**
10. **Backtracking (combinations, permutations, subsets)**

We’ll spiral through these, reinforcing patterns via targeted LeetCode problems.

---

## Week 1 – Foundations: Arrays, Strings, and Big‑O

**Goals:**
- Understand time/space complexity at a practical level.
- Get comfortable with Java collections basics.
- Solve beginner array/string problems using brute force, then improve.

### Concepts to Learn

1. **Big‑O (Practically)**
   - O(1), O(n), O(n log n), O(n²).
   - How nested loops, sorting, and recursion affect complexity.
   - Be able to roughly estimate complexity of a method.

2. **Java Essentials for DSA**
   - `int[]`, `String`, `StringBuilder`.
   - `ArrayList`, basic `List` operations (`add`, `get`, `size`).
   - Enhanced for‑loops vs index loops.

3. **Core Array & String Techniques**
   - Traversal with indices.
   - In‑place modification.
   - Two pointers (start/end).
   - Sliding window (fixed and expanding/contracting windows).

### Daily Structure (example)
- Day 1–2: Big‑O, array iteration, simple problems.
- Day 3–4: Strings, two pointers, sliding window basics.
- Day 5–6: Mixed practice + review.

### LeetCode Problems (Week 1)

#### Arrays – Basics
- **Two Sum** (Easy) – *HashMap, iteration*  
  Concepts: array traversal, hash map, complement idea (value → index).
- **Best Time to Buy and Sell Stock** (Easy) – *Single pass*  
  Concepts: running minimum, max profit in one pass.

#### Strings – Basics & Two Pointers
- **Valid Palindrome** (Easy) – *Two pointers, filtering chars*  
  Concepts: char checks, left/right pointers, ignoring non‑alphanumeric.
- **Implement strStr()** (Easy) – *Substring search, brute force*  
  Concepts: nested loops, string substring, time complexity awareness.

#### Intro Sliding Window
- **Maximum Subarray** (Kadane’s Algorithm) (Medium on LC, conceptually Easy‑Med)  
  Concepts: running sum, reset when negative, O(n) dynamic thinking.
- **Longest Substring Without Repeating Characters** (Medium)  
  Concepts: sliding window, `HashSet` or `HashMap`, left/right pointers.

---

## Week 2 – Hashing + More Two Pointers/Sliding Window

**Goals:**
- Be fluent with `HashMap` and `HashSet`.
- Solve classic frequency and window problems.

### Concepts to Learn

1. **HashMap & HashSet**
   - Common operations: `put`, `get`, `containsKey`, `contains`, `remove`.
   - Counting frequencies (char counts, number counts).
   - Maps vs sets: when to use which.

2. **Patterns With Hashing**
   - Frequency tables (`int[26]` vs `HashMap<Character,Integer>`).
   - Checking anagrams.
   - Using map to store indices for prefix or running conditions.

3. **Sliding Window, cont.**
   - Expanding window until invalid, then shrinking from left.
   - Windows for “at most K” / “exactly K”.

### LeetCode Problems (Week 2)

#### Hashing & Frequency
- **Valid Anagram** (Easy)  
  Concepts: char counting with array/map, comparison of counts.
- **Two Sum II – Input array is sorted** (Easy)  
  Concepts: two pointers on sorted array; contrast vs HashMap approach.
- **Contains Duplicate** (Easy)  
  Concepts: `HashSet` to detect duplicates.

#### Classic Sliding Window
- **Minimum Size Subarray Sum** (Medium)  
  Concepts: sliding window to find minimal length, while loop for shrinking.
- **Longest Repeating Character Replacement** (Medium)  
  Concepts: window, tracking max frequency in current window, `HashMap`.

#### Bonus/Stretch
- **Group Anagrams** (Medium)  
  Concepts: hashing canonical key (sorted string or counts), map of key → list.

---

## Week 3 – Linked Lists, Stack & Queue Fundamentals

**Goals:**
- Pointer manipulation in singly linked lists.
- Understand how stacks/queues work and solve typical problems with them.

### Concepts to Learn

1. **Linked Lists in Java**
   - Custom `ListNode` class (`int val; ListNode next;`).
   - Traversal, insertion, deletion conceptually (you’ll mostly manipulate via problems).
   - Dummy nodes to simplify edge cases.
   - Fast & slow pointers (Floyd’s cycle detection idea).

2. **Stacks**
   - LIFO concept.
   - Java: `Deque<Integer>` as stack (`push`, `pop`, `peek`).
   - Typical uses: parentheses matching, next greater element, undo operations.

3. **Queues**
   - FIFO concept.
   - Java: `Queue<Integer>` with `LinkedList` or `ArrayDeque`.
   - Level‑order traversals (trees later), simple BFS patterns.

### LeetCode Problems (Week 3)

#### Linked Lists
- **Reverse Linked List** (Easy)  
  Concepts: iterative pointer reversal, optionally recursive version.
- **Merge Two Sorted Lists** (Easy)  
  Concepts: two pointers, dummy head, merging logic.
- **Linked List Cycle** (Easy)  
  Concepts: fast & slow pointers, cycle detection.

#### Stack & Parentheses
- **Valid Parentheses** (Easy)  
  Concepts: stack for matching opening/closing brackets.
- **Min Stack** (Medium)  
  Concepts: designing stack with extra data (track current min), composition of two stacks or store pairs.

#### Optional
- **Palindrome Linked List** (Easy/Medium)  
  Concepts: find middle, reverse second half, compare both halves.

---

## Week 4 – Binary Search + Sorting + More Stacks

**Goals:**
- Master binary search patterns on arrays.
- Gain intuition for when to apply binary search, including “search on answer”.
- Understand standard sorting and when to use custom comparators.

### Concepts to Learn

1. **Binary Search Basics**
   - Template for searching in sorted array (iterative).
   - Handling `left`, `right`, `mid` without infinite loops.
   - Variants: first occurrence, last occurrence.
   - Edge cases (off‑by‑one).

2. **Binary Search on Answer / Condition**
   - Search for smallest `x` that satisfies a condition (`check(x)` function).
   - Using monotonic property (false…false, true…true).

3. **Sorting**
   - `Arrays.sort`, `Collections.sort`.
   - Custom comparator for objects (`(a, b) -> Integer.compare(a[0], b[0])`).
   - How sorting helps with greedy/two pointer solutions.

4. **Monotonic Stack (Intro)**
   - Stack that’s increasing or decreasing.
   - Used for “next greater/smaller element” type problems.

### LeetCode Problems (Week 4)

#### Classic Binary Search
- **Binary Search** (Easy)  
  Concepts: basic template implementation.
- **Search Insert Position** (Easy)  
  Concepts: variant where we return insertion index.
- **First Bad Version** (Easy)  
  Concepts: searching boundary using `isBadVersion` API.

#### Binary Search on Answer
- **Find Minimum in Rotated Sorted Array** (Medium)  
  Concepts: binary search with extra logic, rotated array properties.
- **Search in Rotated Sorted Array** (Medium)  
  Concepts: decide which half is sorted, search accordingly.

#### Sorting + Two Pointers
- **Merge Intervals** (Medium)  
  Concepts: sort by start time, iterate and merge overlapping intervals.
- **3Sum** (Medium)  
  Concepts: sort array + two pointers, skipping duplicates.

#### Monotonic Stack Intro
- **Daily Temperatures** (Medium)  
  Concepts: use stack of indices to find next greater temperature.

---

## Week 5 – Trees & Basic Graph‑like Traversals

**Goals:**
- Learn binary tree traversals (pre/in/post‑order) via recursion.
- Understand BFS vs DFS, and use them for typical problems.

### Concepts to Learn

1. **Binary Tree Basics**
   - `TreeNode` class structure.
   - Recursive DFS traversals: preorder (root‑left‑right), inorder, postorder.
   - Height, size, leaves.

2. **BFS on Trees (Level Order)**
   - Using `Queue<TreeNode>`.
   - Level by level operations.

3. **Depth‑First Search (DFS) Patterns**
   - Recursive helper methods.
   - Returning values from recursion (min depth, max depth, balanced, etc.).

### LeetCode Problems (Week 5)

#### DFS (Recursive)
- **Maximum Depth of Binary Tree** (Easy)  
  Concepts: recursion, base case, returning 1 + max(left, right).
- **Path Sum** (Easy)  
  Concepts: recursion with running sum, leaf checks.
- **Diameter of Binary Tree** (Easy/Medium)  
  Concepts: returning height while updating global diameter.

#### BFS
- **Binary Tree Level Order Traversal** (Medium)  
  Concepts: BFS with queue, tracking levels.
- **Minimum Depth of Binary Tree** (Easy)  
  Concepts: BFS to find first leaf, contrasting with DFS approach.

#### Additional Patterns
- **Symmetric Tree** (Easy)  
  Concepts: recursion with two pointers (left subtree vs right subtree).
- **Invert Binary Tree** (Easy)  
  Concepts: simple recursive swapping.

---

## Week 6 – Heaps (PriorityQueue) + More Tree/BFS

**Goals:**
- Use `PriorityQueue` for top‑K, smallest/largest elements, and greedy strategies.
- Apply BFS/DFS to slightly more complex problems (e.g., grids).

### Concepts to Learn

1. **PriorityQueue in Java**
   - Min‑heap by default.
   - For max‑heap: use comparator (`new PriorityQueue<>((a, b) -> b - a)`).
   - Operations: `offer`, `poll`, `peek`.

2. **Typical Heap Uses**
   - Top‑K (largest/smallest).
   - Merging sorted lists.
   - Dijkstra‑like patterns (just conceptually).

3. **Grid BFS/DFS (Graph‑like Thinking)**
   - 2D grid as implicit graph.
   - Directions array `int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};`.
   - Visited tracking.

### LeetCode Problems (Week 6)

#### Priority Queue
- **Kth Largest Element in an Array** (Medium)  
  Concepts: maintain min‑heap of size k or use quickselect; start with heap.
- **Top K Frequent Elements** (Medium)  
  Concepts: frequency map + heap or bucket sort.
- **Merge k Sorted Lists** (Hard, but good practice)  
  Concepts: `PriorityQueue` storing current node from each list.

#### Grid / BFS‑DFS
- **Number of Islands** (Medium)  
  Concepts: DFS/BFS on grid, visited marking.
- **Rotting Oranges** (Medium)  
  Concepts: multi‑source BFS, tracking time layers.

---

## Week 7 – Dynamic Programming (1D & Simple 2D)

**Goals:**
- Learn to identify when DP is appropriate (overlapping subproblems, optimal substructure).
- Implement basic 1D and simple 2D DP problems.

### Concepts to Learn

1. **DP Fundamentals**
   - Recursion with memoization vs bottom‑up tabulation.
   - Define state: `dp[i] = ...`.
   - Base cases, transitions, iteration order.
   - Space optimization where possible.

2. **Common Patterns**
   - Linear DP (house robber, climbing stairs).
   - Partition / knapsack‑like intuition (smaller subset here).
   - Grid DP (paths in grid).

### LeetCode Problems (Week 7)

#### 1D DP
- **Climbing Stairs** (Easy)  
  Concepts: Fibonacci‑like DP, `dp[i] = dp[i-1] + dp[i-2]`.
- **House Robber** (Medium)  
  Concepts: `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`.
- **Coin Change** (Medium)  
  Concepts: combinations to reach amount, unbounded coins.

#### 2D / Grid DP
- **Unique Paths** (Medium)  
  Concepts: `dp[i][j] = dp[i-1][j] + dp[i][j-1]`, boundaries.
- **Minimum Path Sum** (Medium)  
  Concepts: cumulative sums, `dp[i][j] = grid[i][j] + min(top, left)`.

#### Optional
- **Longest Increasing Subsequence** (Medium) – start with O(n²) DP  
  Concepts: nested loops DP, then later you can learn O(n log n) method.

---

## Week 8 – Backtracking & Combining Patterns

**Goals:**
- Learn a generic backtracking template.
- Tackle combination/permutation/subset type problems.
- Attempt some harder problems that mix multiple patterns.

### Concepts to Learn

1. **Backtracking Template**
   - General pattern:
     ```java
     void backtrack(params...) {
         if (end condition) {
             add current path to result;
             return;
         }
         for (choice in choices) {
             make choice;
             backtrack(...);
             undo choice;
         }
     }
     ```
   - Using a `List<Integer>` as current path, deep copying results.

2. **Typical Backtracking Problems**
   - Subsets, combinations, permutations.
   - Choosing or not choosing an element at each step.
   - Avoiding duplicates via sorting and skipping.

3. **Mixing Concepts**
   - Using recursion with pruning.
   - Combining backtracking with sorting or hashing.

### LeetCode Problems (Week 8)

#### Classic Backtracking
- **Subsets** (Medium)  
  Concepts: each element either taken or not, power set generation.
- **Permutations** (Medium)  
  Concepts: using `boolean[] used` to track used elements.
- **Combination Sum** (Medium)  
  Concepts: choosing from candidates, reusing elements, target sum.

#### Handling Duplicates
- **Subsets II** (Medium)  
  Concepts: sort input, skip duplicates when `nums[i] == nums[i-1]`.
- **Combination Sum II** (Medium)  
  Concepts: similar to above but no reuse of elements, skip duplicates.

#### Mixed / Challenge Problems
Pick 2–3 from these to push yourself:
- **Word Search** (Medium) – grid DFS + backtracking.
- **Validate Binary Search Tree** (Medium) – recursion + inorder traversal.
- **Course Schedule** (Medium) – graph + DFS/BFS (cycle detection).

---

## How to Study Each Day

1. **Pick 1–2 Topics Only**
   - Read or watch a short explanation (e.g., 20–30 minutes).
   - Write a small Java snippet that uses the concept (e.g., simple stack experiment).

2. **Solve 2–4 LeetCode Problems**
   - Try **alone first** for 20–30 minutes/problem:
     - Restate the problem in your own words.
     - Think: “Have I seen a similar pattern?” (array + hash? sliding window? etc.)
     - If stuck: think about brute force first, then how to optimize.
   - Then check a solution:
     - Compare approach, note differences in a notebook.
     - Re‑implement from memory once.

3. **End‑of‑Week Review**
   - Re‑implement from scratch 3–5 representative problems without looking.
   - Summarize patterns in your own words (e.g., “Sliding window problems usually ask for substring/subarray with some property…”).

---

## Key Patterns to Keep in Mind

As you work, constantly ask: *“Which pattern fits?”* Most LeetCode problems you’ll encounter early on fall into these:

- **Array + Two Pointers / Sliding Window**
- **Array/String + HashMap/HashSet**
- **Linked List with Fast/Slow Pointers or Reversal**
- **Stack for parentheses / next greater / expression evaluation**
- **Binary Search on sorted list or on answer**
- **Tree DFS/BFS (recursive or queue)**
- **Heap for top‑K / merging**
- **1D/2D DP for “max/min ways/cost” type problems**
- **Backtracking for combinations/permutations/subsets**

If you identify the pattern correctly, the implementation becomes much easier.

---

If you tell me:
- your current Java level, and  
- how many hours per week you realistically have,

I can adjust this 8‑week plan into a more precise daily schedule (and tailor problem counts) so it fits you exactly.
