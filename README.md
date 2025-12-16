Below is an 8‑week, 80/20‑style roadmap in Java. It focuses on the “vital few” DSA ideas that power most LeetCode problems:

- Arrays & Strings  
- Hashing (HashMap/HashSet)  
- Two Pointers & Sliding Window  
- Basic Sorting & Binary Search  
- Stacks & Queues  
- Linked Lists  
- Trees & Binary Search Trees  
- Basic Recursion & Backtracking  
- Intro to Graphs (BFS/DFS)  
- Basic Dynamic Programming patterns  

You’ll code every day (even 30–60 minutes) and use LeetCode as your practice ground.  

**Legend for LeetCode:**  
- E = Easy, M = Medium, H = Hard  
- I’ll list only a handful of representative problems per topic; you can add more later.

---

## Week 1 – Java Foundations + Arrays & Strings

**Goal:** Become comfortable writing Java code, loops, conditionals, and handling arrays/strings. Start simple LeetCode problems.

### Core Concepts (20% that matters)
- Java syntax essentials:
  - `main` method, input/output (basic `System.out.println`)
  - Data types, variables, `if/else`, `for`, `while`
  - Methods: parameters, return types, overloading
- Arrays:
  - Declaration, initialization, iteration
  - Common patterns: sum, max/min, frequency counts
- Strings:
  - `String`, `StringBuilder`
  - Character access, conversion, splitting, joining

### Study Plan

**Days 1–2** – Java basics & setup  
- Install JDK + IDE (IntelliJ IDEA Community or VS Code with Java plugin).  
- Learn:
  - How to write and run a simple class with `public static void main(String[] args)`.  
  - Basic I/O, loops, methods.

**Days 3–4** – Arrays  
- 1D arrays: `int[] arr = new int[n];`  
- Traversals, prefix sums idea (running totals).  
- In-place updates, basic operations (reverse, rotate conceptually).

**Days 5–7** – Strings  
- Immutable nature of `String`; when to use `StringBuilder`.  
- Lowercasing, trimming, splitting, character frequency (e.g., with `int[26]` or `HashMap<Character, Integer>`).

### Suggested LeetCode (Week 1)

**Arrays/Strings (Beginner)**  
1. **Two Sum (1, E)**  
   - Type: Array + HashMap  
   - Reinforces: Array traversal, hash maps, thinking about complements.

2. **Best Time to Buy and Sell Stock (121, E)**  
   - Type: Array, tracking min and max profit  
   - Reinforces: One-pass scan, maintaining state (min-so-far, max-profit).

3. **Contains Duplicate (217, E)**  
   - Type: Array + HashSet  
   - Reinforces: Using `HashSet`, detecting duplicates efficiently.

4. **Valid Anagram (242, E)**  
   - Type: String + frequency counting  
   - Reinforces: Counting characters using array or `HashMap`.

5. **Reverse String (344, E)**  
   - Type: String + Two Pointers (intro)  
   - Reinforces: Index manipulation, in-place modification of char array.

---

## Week 2 – Hashing, Two Pointers & Sliding Window

**Goal:** Master hash map/set usage and core pointer patterns used in many LC problems.

### Core Concepts
- HashMap/HashSet:
  - Insert, lookup, remove; complexity O(1) average
  - When to choose map vs set
- Two Pointers:
  - Left/right indices moving towards each other (or along the array)
- Sliding Window:
  - Maintain a “window” (subarray/substring) satisfying a condition
  - Expand/shrink pattern

### Study Plan

**Days 1–2** – HashMap & HashSet in Java  
- `HashMap<K, V>`: `put`, `get`, `containsKey`, `remove`, iteration over `entrySet`.  
- `HashSet<E>`: `add`, `contains`, `remove`.

**Days 3–4** – Two Pointers patterns  
- Opposite ends: e.g., array reversed, sum to target in **sorted** array.  
- Same direction: fast/slow pointers to detect conditions (e.g., removing duplicates, cycle detection conceptually).

**Days 5–7** – Sliding Window  
- Fixed window size vs variable window size.  
- General pattern:
  - Expand `right`
  - While condition is violated, shrink `left`
  - Track best answer (length, count, etc.)

### Suggested LeetCode (Week 2)

**Hashing / Two Pointers / Sliding Window**

1. **Valid Palindrome (125, E)**  
   - Type: Two Pointers (string)  
   - Reinforces: Left/right pointers, character checks, ignoring non-alphanumeric.

2. **Move Zeroes (283, E)**  
   - Type: Two Pointers (array)  
   - Reinforces: In-place array manipulation, slow/fast pointer logic.

3. **Two Sum II – Input array is sorted (167, E)**  
   - Type: Two Pointers on sorted array  
   - Reinforces: Using sorted property, converging pointers.

4. **Longest Substring Without Repeating Characters (3, M)**  
   - Type: Sliding Window + HashSet/Map  
   - Reinforces: Variable-size window, tracking seen characters.

5. **Minimum Size Subarray Sum (209, M)**  
   - Type: Sliding Window (array)  
   - Reinforces: Shrink/expand pattern while maintaining sum condition.

---

## Week 3 – Sorting Basics & Binary Search

**Goal:** Understand basic sorting ideas and use binary search patterns confidently.

### Core Concepts
- Sorting:
  - Use `Arrays.sort()` & `Collections.sort()`
  - Understand O(n log n) idea and stability in a rough sense.
- Binary Search:
  - Classic search for target in sorted array
  - Variants: first/last occurrence, lower/upper bound, condition-based search.

### Study Plan

**Days 1–2** – Sorting  
- Sort primitives: `Arrays.sort(int[])`.  
- Sort objects: `Arrays.sort(arr, Comparator.comparingInt(...))`.  
- Recognize when to sort first then use two pointers / binary search.

**Days 3–5** – Classic Binary Search  
- Implement `binarySearch(int[] nums, int target)`.  
- Handle mid calculation carefully: `mid = left + (right - left) / 2`.  
- On each step, decide which half to keep.

**Days 6–7** – Variants of Binary Search  
- Find leftmost/rightmost index of target.  
- “Search on answer” pattern: monotonic property (e.g., smallest capacity that works, minimum days).

### Suggested LeetCode (Week 3)

**Binary Search & Sorting**

1. **Binary Search (704, E)**  
   - Type: Basic binary search  
   - Reinforces: Template, boundaries, loop invariants.

2. **First Bad Version (278, E)**  
   - Type: Binary search on boolean condition  
   - Reinforces: “Search on condition,” minimizing index that satisfies predicate.

3. **Search Insert Position (35, E)**  
   - Type: Binary search variant  
   - Reinforces: Returning insertion index when target not found.

4. **Find Peak Element (162, M)**  
   - Type: Binary search on array “shape”  
   - Reinforces: Using relative comparisons instead of exact target.

5. **Search in Rotated Sorted Array (33, M)**  
   - Type: Binary search with rotation logic  
   - Reinforces: Handling modified sorted arrays, conditional splits.

---

## Week 4 – Stacks & Queues + Linked Lists (Basics)

**Goal:** Learn stack/queue ADTs and train with linked list operations.

### Core Concepts
- Stack:
  - LIFO; implemented via `Stack` or `Deque` (`ArrayDeque` is preferred).  
- Queue:
  - FIFO; `Queue` interface (e.g., `LinkedList`, `ArrayDeque`).
- Linked Lists:
  - Node structure: `ListNode { int val; ListNode next; }`
  - Insertion, deletion, traversal
  - Dummy head pattern to simplify edge cases

### Study Plan

**Days 1–3** – Stack & Queue  
- Implement basic stack push/pop/peek.  
- Implement queue add/poll/peek.  
- Understand typical use cases: parentheses checking, undo, BFS.

**Days 4–7** – Linked Lists  
- Singly linked lists: insert at head/tail, delete, find.  
- Fast/slow pointer techniques (middle, cycle).

### Suggested LeetCode (Week 4)

**Stacks**

1. **Valid Parentheses (20, E)**  
   - Type: Stack  
   - Reinforces: Pushing opening brackets, matching closing one.

2. **Min Stack (155, E)**  
   - Type: Stack with auxiliary min tracking  
   - Reinforces: Keeping extra info in stack; design.

3. **Daily Temperatures (739, M)**  
   - Type: Monotonic Stack  
   - Reinforces: Using stack to find “next greater” element pattern.

**Linked Lists**

4. **Reverse Linked List (206, E)**  
   - Type: Linked list pointer manipulation  
   - Reinforces: Iterative reversal; understanding `prev`, `curr`, `next`.

5. **Merge Two Sorted Lists (21, E)**  
   - Type: Linked list merging  
   - Reinforces: Dummy head pattern, merging in sorted order.

6. **Linked List Cycle (141, E)**  
   - Type: Fast/slow pointers  
   - Reinforces: Two-pointer cycle detection.

7. **Remove Nth Node From End of List (19, M)**  
   - Type: Two pointers + linked list  
   - Reinforces: Dummy node, offset pointers, careful edge handling.

---

## Week 5 – Trees & Binary Search Trees

**Goal:** Comfortably traverse trees (DFS/BFS) and use BST properties.

### Core Concepts
- Tree basics:
  - `TreeNode { int val; TreeNode left; TreeNode right; }`
  - Depth-first search (preorder, inorder, postorder, recursive first)
- Binary Search Tree (BST):
  - Left < root < right
  - Search, insert, find min/max
- Tree height, leaf, path concepts.

### Study Plan

**Days 1–3** – Tree Traversals  
- Recursive DFS: preorder, inorder, postorder.  
- Practice writing these from memory.

**Days 4–5** – BFS on Trees  
- Use a queue to traverse level by level.  
- Understand when BFS is better (e.g., level-based problems).

**Days 6–7** – BST Basics  
- Implement search in BST, insert, find min/max.  
- Leverage sorted property in recursion.

### Suggested LeetCode (Week 5)

**Trees / BST**

1. **Maximum Depth of Binary Tree (104, E)**  
   - Type: DFS (recursive)  
   - Reinforces: Basic recursion, returning aggregated results.

2. **Balanced Binary Tree (110, E)**  
   - Type: DFS + height computation  
   - Reinforces: Postorder traversal, combining child info.

3. **Symmetric Tree (101, E)**  
   - Type: Recursive tree comparison  
   - Reinforces: Mirror comparisons, recursion with multiple arguments.

4. **Binary Tree Level Order Traversal (102, M)**  
   - Type: BFS with queue  
   - Reinforces: Level-by-level traversal, grouping results.

5. **Validate Binary Search Tree (98, M)**  
   - Type: DFS with bounds (min/max) or inorder traversal  
   - Reinforces: Using value constraints through recursive calls.

6. **Lowest Common Ancestor of a BST (235, E/M)**  
   - Type: BST property exploitation  
   - Reinforces: Structural reasoning based on value comparisons.

---

## Week 6 – Recursion & Backtracking (Intro) + More Tree Practice

**Goal:** Get comfortable with recursion and basic backtracking. Still very common in LC.

### Core Concepts
- Recursion:
  - Base case, recursive case
  - Call stack concept, avoiding infinite recursion
- Backtracking:
  - Decision tree: choose → explore → unchoose
  - Generating subsets, permutations, combinations

### Study Plan

**Days 1–2** – Recursion basics  
- Factorial, Fibonacci (for learning, not performance).  
- Simple recursion on arrays/strings (e.g., recursively reverse a string).

**Days 3–5** – Backtracking patterns  
- Template:
  ```java
  void backtrack(State state) {
      if (goal) { record solution; return; }
      for (choice in choices) {
          make choice;
          backtrack(updatedState);
          undo choice;
      }
  }
  ```

**Days 6–7** – Tree-related recursion / backtracking  
- Path-based problems, sum paths, etc.

### Suggested LeetCode (Week 6)

**Backtracking / Recursion**

1. **Subsets (78, M)**  
   - Type: Backtracking (power set)  
   - Reinforces: Choose/not-choose pattern, recursion depth.

2. **Permutations (46, M)**  
   - Type: Backtracking with swapping / visited array  
   - Reinforces: Generating all permutations, managing visited state.

3. **Combinations (77, M)**  
   - Type: Backtracking with start index  
   - Reinforces: Controlling duplicates via ordering, pruning.

**Tree + Recursion**

4. **Path Sum (112, E)**  
   - Type: Recursive tree DFS  
   - Reinforces: Passing cumulative sum through recursion.

5. **Path Sum II (113, M)**  
   - Type: Tree + backtracking  
   - Reinforces: Building and unwinding path lists.

---

## Week 7 – Graphs (BFS/DFS) + Intro to Dynamic Programming

**Goal:** Learn how to represent graphs and do BFS/DFS; see basic DP (1D).

### Core Concepts
- Graph representation:
  - Adjacency list using `Map<Integer, List<Integer>>` or `List<List<Integer>>`
  - Directed vs undirected, cycles
- Graph traversal:
  - BFS with queue (shortest path in unweighted graph)
  - DFS recursive or stack-based
- Dynamic Programming (DP):
  - Overlapping subproblems, optimal substructure
  - Memoization vs tabulation
  - 1D DP examples

### Study Plan

**Days 1–3** – Graph BFS/DFS  
- Build adjacency list from edge list.  
- BFS on graph to find shortest path (in edges).  
- DFS to count connected components.

**Days 4–7** – Basic DP  
- Classic 1D DP problems: Fibonacci with memo, climbing stairs, house robber.

### Suggested LeetCode (Week 7)

**Graphs**

1. **Number of Islands (200, M)**  
   - Type: DFS/BFS on grid  
   - Reinforces: Grid as graph, visited set, counting connected components.

2. **Max Area of Island (695, M)**  
   - Type: DFS grid  
   - Reinforces: Similar to above, plus returning area counts.

3. **Clone Graph (133, M)**  
   - Type: Graph BFS/DFS with HashMap  
   - Reinforces: Graph traversal and mapping original-to-clone nodes.

**Dynamic Programming**

4. **Climbing Stairs (70, E)**  
   - Type: 1D DP (Fibonacci-like)  
   - Reinforces: Recurrence `dp[i] = dp[i-1] + dp[i-2]`.

5. **House Robber (198, M)**  
   - Type: 1D DP  
   - Reinforces: “Take or skip” pattern: `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`.

6. **Maximum Subarray (53, E/M)**  
   - Type: Kadane’s Algorithm (DP-ish)  
   - Reinforces: Local vs global maximum, simple iterative DP.

---

## Week 8 – Classic DP Patterns & Mixed Practice

**Goal:** Solidify DP & revisit all earlier topics with mixed sets of LC problems.

### Core Concepts
- Common DP patterns:
  - 1D linear DP (already seen)
  - 2D DP for sequences or grids
  - “Knapsack-like” state transitions
- Integrating multiple concepts:
  - E.g., sliding window + hash, tree + recursion + DP.

### Study Plan

**Days 1–3** – 2D / Grid DP  
- Understand table definition: `dp[i][j]` meaning.  
- Transitions from neighboring cells.

**Days 4–5** – Sequence DP / Edit-based problems  
- Define `dp[i][j]` as operation counts or lengths.

**Days 6–7** – Mixed review  
- Pick a couple of problems mixing arrays, trees, graphs, DP.

### Suggested LeetCode (Week 8)

**DP**

1. **Unique Paths (62, M)**  
   - Type: 2D grid DP  
   - Reinforces: Counting paths with simple transitions.

2. **Coin Change (322, M)**  
   - Type: 1D/2D unbounded knapsack-like DP  
   - Reinforces: Minimization DP, impossible states (`Integer.MAX_VALUE` style).

3. **Edit Distance (72, H – stretch)**  
   - Type: 2D DP on strings  
   - Reinforces: Defining dp on prefixes, multiple operations (insert/delete/replace).

**Mixed Review (choose based on interest)**

4. **Product of Array Except Self (238, M)**  
   - Type: Arrays, prefix/suffix  
   - Reinforces: Constant space trick, left-right passes.

5. **Kth Smallest Element in a BST (230, M)**  
   - Type: BST + inorder traversal  
   - Reinforces: Inorder = sorted order for BST.

6. **Course Schedule (207, M)**  
   - Type: Graph + Topological sort  
   - Reinforces: Detecting cycles in directed graph with BFS or DFS.

---

## How to Work Through Problems (for All Weeks)

Use this general workflow for each LeetCode problem:

1. **Read & Restate:**  
   - Paraphrase problem in your own words.  
   - Identify input/output types and constraints.

2. **Classify the Pattern:**  
   - Ask: “Is this array, string, tree, graph?”  
   - Then: “Which pattern: two pointers, sliding window, BFS, DP, etc.?”

3. **Brainstorm & Choose Approach:**  
   - Start with a brute force idea.  
   - Then think: “How can I use a known pattern to improve?”

4. **Write Pseudocode First:**  
   - Keep it short: loops, key variables, conditions.

5. **Implement in Java:**  
   - Only then write actual Java code.  
   - Pay attention to off-by-one and null checks.

6. **Test Small Cases Manually:**  
   - Use very small inputs and walk through step-by-step.

7. **Analyze Complexity:**  
   - Time: O(n), O(n log n), etc.  
   - Space: extra arrays, recursion depth, hash maps.

8. **Review & Generalize:**  
   - Ask: “What pattern did this use?”  
   - Add to your mental library: e.g., “This is another sliding window variant.”

---

## Weekly Time Allocation (Guideline)

Assuming ~10–12 hours/week:

- ~3–4 hours: Learning concepts (videos, reading, notes).  
- ~6–8 hours: Solving problems (3–5 problems per session, 4–5 days/week).  

On tough problems, spend 30–45 minutes thinking before looking at hints or solutions. When you do look, re-implement from memory after a short break.

---

If you’d like, next I can:  
- Turn this into a day‑by‑day checklist, or  
- Suggest specific Java learning resources to pair with each week.
