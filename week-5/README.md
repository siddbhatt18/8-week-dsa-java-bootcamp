**Week 5 Focus:**  
- Binary tree fundamentals  
- Recursion with DFS (preorder, inorder, postorder)  
- BFS with queues (level-order)  
- Classic tree problems (max depth, min depth, diameter, path sum, symmetry, invert)  

Assume ~2–3 hours/day. Keep the habit: think on paper first, then code, then reflect.

---

## Shared Setup for the Week

Create a small “utilities” file you’ll reuse (or copy into each day’s file):

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int val) {
        this.val = val;
    }
}
```

You can also write a helper to build a simple tree manually in `main` when needed.

---

## Day 1 – What Is a Binary Tree? + Recursive Traversals

### 1. Concept: Trees & Binary Trees (25–35 min)

On paper:

- Define:
  - **Tree:** nodes connected in a hierarchy, no cycles.
  - **Binary tree:** each node has at most 2 children: `left`, `right`.
- Vocabulary:
  - root, child, parent, leaf, subtree, height/depth.

Draw a simple tree:

```
      1
     / \
    2   3
   / \
  4   5
```

Discuss:
- Why arrays are not great for representing arbitrary trees.
- Why recursion fits trees naturally (a tree is made of smaller trees).

### 2. Recursive Traversal Orders (30–40 min)

On paper, for the sample tree, write the order of nodes visited for:

- **Preorder (root, left, right)**  
  - Example: `1 2 4 5 3`
- **Inorder (left, root, right)**  
  - Example: `4 2 5 1 3`
- **Postorder (left, right, root)**  
  - Example: `4 5 2 3 1`

Understand:
- Each is just a different visiting order implemented via recursion.

### 3. Coding: Basic Traversals (45–60 min)

In `Week5Day1.java`:

1. Define `TreeNode` (as above) inside the file.
2. Implement:

   ```java
   void preorder(TreeNode root) { ... }
   void inorder(TreeNode root) { ... }
   void postorder(TreeNode root) { ... }
   ```

   Simple version: print the `val` in each.

   Example template:

   ```java
   void preorder(TreeNode root) {
       if (root == null) return;
       System.out.print(root.val + " ");
       preorder(root.left);
       preorder(root.right);
   }
   ```

3. In `main`, manually build the small tree from your drawing and call each traversal to check the order.

### 4. Reflection (10–15 min)

Write:
- Which traversal order feels most intuitive to you so far?
- In your own words, why recursion works well on trees.

---

## Day 2 – Maximum Depth & Basic DFS Recursion

### 1. Quick Review (10–15 min)

- From memory, write pseudo‑code for `preorder(root)` and `inorder(root)` on paper.
- Sketch the tree from Day 1 and write its inorder traversal again.

### 2. Concept: Maximum Depth (Height) of a Binary Tree (20–30 min)

On paper:

- Problem: given the root, find the maximum depth (longest path from root to a leaf, counting nodes or edges; LeetCode uses number of nodes).
- Idea:
  - For each node, depth = 1 + max(depth of left subtree, depth of right subtree).
  - Base case: depth of `null` is 0.

Write the recurrence:
- `maxDepth(root) = 0 if root == null`
- `maxDepth(root) = 1 + max(maxDepth(root.left), maxDepth(root.right))`

### 3. Coding: Maximum Depth (45–60 min)

In `Week5Day2.java`:

1. Implement:

   ```java
   int maxDepth(TreeNode root) {
       if (root == null) return 0;
       int leftDepth = maxDepth(root.left);
       int rightDepth = maxDepth(root.right);
       return 1 + Math.max(leftDepth, rightDepth);
   }
   ```

2. Test with:
   - Empty tree (`null`) → 0
   - Single node tree → 1
   - Your Day 1 sample tree.

### 4. LeetCode: Maximum Depth of Binary Tree (Easy) (30–40 min)

- Solve LC **104. Maximum Depth of Binary Tree** using your recursive approach.
- After solving:
  - Read one other solution (iterative BFS) just to see an alternative.

### 5. Extra DFS Practice: Count Nodes (Optional, 20–30 min)

Implement:

```java
int countNodes(TreeNode root) {
    if (root == null) return 0;
    return 1 + countNodes(root.left) + countNodes(root.right);
}
```

Think:
- How is this similar to `maxDepth` structurally?

### 6. Reflection (10–15 min)

Write:
- What is the main pattern behind both `maxDepth` and `countNodes`?
- In one sentence, describe the idea of “let recursion handle the subtrees, then combine”.

---

## Day 3 – BFS with Queue: Level Order & Minimum Depth

### 1. Quick Review (10–15 min)

- Explain, in words, how the `maxDepth` recursion works.
- Sketch a tree and label depths manually.

### 2. Concept: BFS & Level Order Traversal (30–40 min)

On paper:

- BFS for trees:
  - Process level by level using a **queue**.
- Algorithm:
  1. Create a `Queue<TreeNode>`.
  2. Add root (if not null).
  3. While queue not empty:
     - For each node at current level (size of queue):
       - Pop node.
       - Process it (e.g., store value).
       - Add its children if not null.

Draw your sample tree and simulate a BFS queue:
- Levels: `[1]`, then `[2,3]`, then `[4,5]`.

### 3. Coding: Level Order Traversal (45–60 min)

In `Week5Day3.java`:

1. Implement:

   ```java
   List<List<Integer>> levelOrder(TreeNode root)
   ```

   - Use `Queue<TreeNode> queue = new LinkedList<>();`.
   - For each level, create a `List<Integer>`, push children in queue.

2. Test with your sample tree.

### 4. LeetCode: Binary Tree Level Order Traversal (Medium) (30–40 min)

- LC **102. Binary Tree Level Order Traversal**.
- Use the same code. Adapt interface.

### 5. Concept: Minimum Depth of Binary Tree (25–35 min)

On paper:

- Min depth = number of nodes along the shortest path from root to the **nearest leaf**.
- Two common approaches:
  1. DFS (similar to max depth, but careful with one‑sided children).
  2. BFS: the first leaf you encounter in BFS has the minimum depth.

Think:
- BFS approach:
  - Level order traversal.
  - As soon as you reach a node that is a leaf (`left == null && right == null`), return current depth.

### 6. Coding: Minimum Depth with BFS (Optional but recommended) (20–30 min)

Implement:

```java
int minDepth(TreeNode root)
```

- Use BFS (queue), track depth as you go.
- LeetCode has **111. Minimum Depth of Binary Tree** (you can try this after coding locally).

### 7. Reflection (10–15 min)

Write:
- Difference between DFS and BFS in trees, in your own words.
- When would BFS be more natural than DFS?

---

## Day 4 – Symmetric Tree & Invert Binary Tree

### 1. Quick Review (10–15 min)

- Re‑state BFS level order logic (queue, processing by levels).
- From memory, sketch pseudo‑code for `levelOrder`.

### 2. Concept: Symmetric Tree (Mirror) (25–35 min)

On paper:

- Problem: determine if a tree is symmetric around its center.
  - Left subtree is a mirror of right subtree.

For two subtrees `t1` and `t2` to be mirror:
- Both null → symmetric.
- One null, other not → not symmetric.
- `t1.val == t2.val` AND:
  - `t1.left` mirrors `t2.right`
  - `t1.right` mirrors `t2.left`

Write recursive helper:

```java
boolean isMirror(TreeNode t1, TreeNode t2)
```

### 3. Coding: Symmetric Tree (45–60 min)

In `Week5Day4.java`:

1. Implement:

   ```java
   boolean isSymmetric(TreeNode root) {
       if (root == null) return true;
       return isMirror(root.left, root.right);
   }

   boolean isMirror(TreeNode t1, TreeNode t2) {
       if (t1 == null && t2 == null) return true;
       if (t1 == null || t2 == null) return false;
       if (t1.val != t2.val) return false;
       return isMirror(t1.left, t2.right) && isMirror(t1.right, t2.left);
   }
   ```

2. Test with:
   - Symmetric tree like:
     ```
         1
        / \
       2   2
      / \ / \
     3  4 4  3
     ```
   - Asymmetric tree.

3. LeetCode: **101. Symmetric Tree (Easy)** – adapt and submit.

### 4. Concept: Invert/Flip Binary Tree (20–30 min)

On paper:

- Problem: invert a binary tree (swap left and right children for all nodes).
- Example:

  ```
      4            4
     / \          / \
    2   7   ->   7   2
   / \ / \      / \ / \
  1  3 6  9    9  6 3  1
  ```

- Recursive idea:
  - For each node:
    - Swap `left` and `right`.
    - Recurse on children.

### 5. Coding: Invert Binary Tree (20–30 min)

Implement:

```java
TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    TreeNode temp = root.left;
    root.left = root.right;
    root.right = temp;
    invertTree(root.left);
    invertTree(root.right);
    return root;
}
```

Test locally, then attempt LC **226. Invert Binary Tree (Easy)**.

### 6. Reflection (10–15 min)

Write:
- How are `isSymmetric` and `invertTree` similar in their recursive structure?
- What mental model of a tree helps you write these recursive functions?

---

## Day 5 – Path Sum & Root-to-Leaf Thinking

### 1. Quick Review (10–15 min)

- From memory, explain `isSymmetric` in words (mirror comparison).
- Sketch pseudo‑code for `invertTree`.

### 2. Concept: Path Sum (25–35 min)

On paper:

- LC **112. Path Sum (Easy)**:  
  Given root and an integer `targetSum`, return true if there exists a root-to-leaf path where the sum of values equals `targetSum`.

Key idea:
- Use DFS recursion:
  - Subtract current node’s value from sum.
  - Recurse down.
  - When you reach leaf: check if `sum - val == 0`.

Pseudo:

```java
boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) {
        return targetSum == root.val;
    }
    int newSum = targetSum - root.val;
    return hasPathSum(root.left, newSum) || hasPathSum(root.right, newSum);
}
```

### 3. Coding: Path Sum (45–60 min)

In `Week5Day5.java`:

1. Implement `hasPathSum`.
2. Test with small trees:
   - Example from LC description.
3. Then solve LC **112. Path Sum**.

### 4. Extra: Collect All Path Sums (Optional but good practice) (30–40 min)

Implement a method:

```java
List<List<Integer>> pathSumEquals(TreeNode root, int targetSum)
```

Goal:
- Collect all root‑to‑leaf paths where sum equals `targetSum`.

Idea:
- Use recursion + backtracking:
  - Maintain a `List<Integer> path` for current path.
  - At each node:
    - Add `root.val` to path.
    - Recurse.
    - Remove last added value after returning (backtrack).

Even if you don’t complete the full method, outline the approach and code part of it to practice backtracking within trees.

### 5. Reflection (10–15 min)

Write:
- What is the difference between:
  - Functions that compute a single boolean (e.g., `hasPathSum`).
  - Functions that collect multiple paths/results (list of lists).
- Why does backtracking (add, recurse, remove) work here?

---

## Day 6 – Diameter of Binary Tree & Combining Values in Recursion

### 1. Quick Review (10–15 min)

- Restate how `hasPathSum` works using a single example tree and sum.
- Explain why you check leaf condition separately.

### 2. Concept: Diameter of Binary Tree (30–40 min)

On paper:

- LC **543. Diameter of Binary Tree (Easy/Medium)**:
  - Diameter = length (number of edges) of the longest path between any two nodes in the tree.
- Observation:
  - For each node, the longest path **through** it is:
    - `leftHeight + rightHeight` (number of edges).
  - Diameter of tree = maximum of `leftHeight + rightHeight` over all nodes.

Plan:
- Define a recursive function that returns the **height** of a node.
- While computing height, **also update a global (or class field) `maxDiameter`**.

Pseudo:

```java
int maxDiameter = 0;

int height(TreeNode node) {
    if (node == null) return 0;
    int leftH = height(node.left);
    int rightH = height(node.right);
    // update diameter: number of edges: leftH + rightH
    maxDiameter = Math.max(maxDiameter, leftH + rightH);
    return 1 + Math.max(leftH, rightH);
}
```

Then `diameterOfBinaryTree(root)` calls `height(root)` and returns `maxDiameter`.

### 3. Coding: Diameter of Binary Tree (45–60 min)

In `Week5Day6.java`:

1. Implement `int diameterOfBinaryTree(TreeNode root)` using the above pattern.
2. Test with small trees where you can visually see longest paths.

3. Solve LC **543. Diameter of Binary Tree**.

### 4. Extra: Balanced Binary Tree (Optional, similar pattern) (20–30 min)

- LC **110. Balanced Binary Tree**:
  - A tree is height-balanced if for every node, the difference between left and right heights is at most 1.
- Idea:
  - Similar recursion:
    - Compute height.
    - If any subtree is unbalanced, propagate a flag or a special value (e.g., -1).

Even if you don’t finish coding, think about:
- How to combine multiple pieces of info (height + balanced or not) in a single recursion.

### 5. Reflection (10–15 min)

Write:
- How is `diameterOfBinaryTree` different from `maxDepth`, even though both compute heights?
- Why is it helpful to use a field (or holder object) to track global maximum?

---

## Day 7 – Consolidation: DFS + BFS on Trees

### 1. Concept Review (30–40 min)

Without looking at code, on paper:

- Write the intuitive explanation for:
  - Preorder, inorder, postorder.
  - DFS for max depth.
  - BFS for level order.
  - Symmetric tree recursion (mirror).
  - Path sum recursion.

- For each, mention:
  - Where you handle the base case.
  - What value/information gets returned upwards.

Then check against your notes and correct anything off.

### 2. Re‑implement from Memory (60–75 min)

In `Week5Review.java`, re‑implement:

1. `int maxDepth(TreeNode root)`
2. `List<List<Integer>> levelOrder(TreeNode root)`
3. `boolean isSymmetric(TreeNode root)` + `isMirror` helper
4. `TreeNode invertTree(TreeNode root)`
5. `boolean hasPathSum(TreeNode root, int targetSum)`
6. `int diameterOfBinaryTree(TreeNode root)`

For each:
- Add comments:
  - Time complexity.
  - Space complexity (stack depth for recursion, queue size for BFS).
  - 1–2 line intuition.

### 3. LeetCode Mini‑Session (60–75 min)

On LeetCode, solve or re‑solve:

1. **104. Maximum Depth of Binary Tree (Easy)**  
2. **111. Minimum Depth of Binary Tree (Easy)** – BFS version if you didn’t before  
3. **101. Symmetric Tree (Easy)**  
4. **226. Invert Binary Tree (Easy)**  
5. **543. Diameter of Binary Tree (Easy/Medium)**  

If you have extra time:
- Attempt **112. Path Sum (Easy)** again from scratch.

For each:
- Spend some time thinking before typing.
- If stuck, write out a small example tree and walk through recursion or BFS on paper.

### 4. End‑of‑Week Reflection (15–20 min)

In your notebook:

1. **Pattern Summary**
   - DFS with recursion:
     - “Let recursion solve subtrees, then combine results.”
   - BFS with a queue:
     - “Process by levels, keep track of depth if needed.”
   - Passing information down (like remaining sum) vs returning information up (like heights, booleans).

2. **Comfort Ratings (1–5):**
   - Writing simple tree recursion.
   - Using queues for BFS.
   - Combining multiple pieces of info in a recursive function (like diameter).

3. **Questions for Next Week:**
   - Example:
     - “How to apply DFS/BFS to grids and general graphs?”
     - “How to avoid recursion stack overflow on very deep trees?”
     - “How to represent trees/graphs from input in interviews?”

These will feed directly into Week 6 (heaps, more BFS/DFS, and grid/graph style problems).

---

If you’d like, I can next structure **Week 6** day‑by‑day (PriorityQueue/heap + grid BFS/DFS), again with concrete LeetCode tasks and thinking prompts.
