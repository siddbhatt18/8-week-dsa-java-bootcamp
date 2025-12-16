Here is your **Day 1–Day 7 plan for Week 5**, focused on:

- Binary Trees (representation + traversal)
- Depth-First Search (DFS) & Breadth-First Search (BFS) on trees
- Binary Search Trees (BSTs) and their properties
- Core LeetCode tree problems

Assume ~2–3 hours per day and adjust as needed.

---

## Shared Setup for Week 5

Create a package for this week, e.g.:

```java
package week5;

public class TreeNode {
    public int val;
    public TreeNode left;
    public TreeNode right;
    public TreeNode(int val) { this.val = val; }
}
```

You can either:
- Put `TreeNode` in its own file and import it in each class, or
- Define an inner `TreeNode` class inside each solution class (LeetCode-style).  
For learning, having a shared `TreeNode` is convenient.

---

## Day 1 – Tree Basics & Recursive DFS Traversals

**Goals:**
- Understand what a binary tree is.
- Learn and implement recursive traversals: preorder, inorder, postorder.

### 1. Concept Primer (20–30 min)

Key ideas:
- **Binary tree**: each node has up to 2 children (`left`, `right`).
- **Traversal orders**:
  - Preorder: `root → left → right`
  - Inorder: `left → root → right`
  - Postorder: `left → right → root`
- Recursion fits trees naturally: each subtree is itself a tree.

### 2. Implement Basic Tree Construction & Traversal (60–75 min)

Create: `week5.day1.TreeTraversalsDemo`.

**Tasks:**

1. Manually build a small tree:

   ```java
   //        1
   //       / \
   //      2   3
   //     / \
   //    4   5

   TreeNode root = new TreeNode(1);
   root.left = new TreeNode(2);
   root.right = new TreeNode(3);
   root.left.left = new TreeNode(4);
   root.left.right = new TreeNode(5);
   ```

2. Implement:

   ```java
   public static void preorder(TreeNode root) {
       if (root == null) return;
       System.out.print(root.val + " ");
       preorder(root.left);
       preorder(root.right);
   }

   public static void inorder(TreeNode root) {
       if (root == null) return;
       inorder(root.left);
       System.out.print(root.val + " ");
       inorder(root.right);
   }

   public static void postorder(TreeNode root) {
       if (root == null) return;
       postorder(root.left);
       postorder(root.right);
       System.out.print(root.val + " ");
   }
   ```

3. Call each traversal on the example tree and print results.

**Concepts reinforced:**
- Tree structure.
- Recursive thinking and base case (`if (root == null) return;`).

### 3. Simple Recursive Utilities (30–45 min)

In the same class or a new one `TreeUtils`:

1. `int countNodes(TreeNode root)` – returns total nodes.
2. `int sumNodes(TreeNode root)` – returns sum of all values.
3. `int maxNode(TreeNode root)` – returns max value (assume non-empty).

These warm you up for recursive LeetCode problems.

---

## Day 2 – Tree Depth & Basic DFS Problems

**Goals:**
- Compute height/depth of a tree.
- Solve simple tree DFS LeetCode problems.

### 1. Maximum Depth (Height) of a Tree (30–45 min)

Create: `week5.day2.MaxDepthDemo`.

Implement:

```java
public static int maxDepth(TreeNode root) {
    if (root == null) return 0;
    int left = maxDepth(root.left);
    int right = maxDepth(root.right);
    return Math.max(left, right) + 1;
}
```

Test on the tree from Day 1.

### 2. LeetCode: Maximum Depth of Binary Tree (104, Easy) (30–45 min)

Create: `week5.day2.LC104MaxDepth`.

- Use the same logic as above.
- Add explanation comments:
  - “Depth of node = 1 + max(depth of left, depth of right)”.
- Time: O(n), Space: O(h) where h is height (recursion stack).

### 3. LeetCode: Balanced Binary Tree (110, Easy) (45–60 min)

Create: `week5.day2.LC110BalancedBinaryTree`.

Definition: A height-balanced tree is where the depth of two subtrees of every node never differ by more than 1.

**Approach:**
- Postorder recursion that returns height; return `-1` if subtree is unbalanced:
  ```java
  private int check(TreeNode root) {
      if (root == null) return 0;
      int left = check(root.left);
      if (left == -1) return -1;
      int right = check(root.right);
      if (right == -1) return -1;
      if (Math.abs(left - right) > 1) return -1;
      return Math.max(left, right) + 1;
  }

  public boolean isBalanced(TreeNode root) {
      return check(root) != -1;
  }
  ```

Concepts reinforced:
- Postorder traversal: calculate from children up.
- Early pruning and special sentinel return values.

### 4. Quick Review (15–20 min)

- Explain to yourself:
  - Preorder/inorder/postorder in words.
  - Why depth computation is naturally recursive.

---

## Day 3 – Symmetry & Path-Based Tree Problems

**Goals:**
- Compare mirrored trees.
- Handle simple path-sum style DFS problems.

### 1. LeetCode: Symmetric Tree (101, Easy) (45–60 min)

Create: `week5.day3.LC101SymmetricTree`.

Tree is symmetric if left subtree is mirror of right subtree.

**Approach:**
- Write helper `isMirror(TreeNode t1, TreeNode t2)`:
  - Both null → true.
  - One null, one not → false.
  - Values differ → false.
  - Recursively check:
    - `isMirror(t1.left, t2.right)` and `isMirror(t1.right, t2.left)`.

Concepts reinforced:
- Recursion with two nodes at a time.
- Mirror logic.

### 2. LeetCode: Path Sum (112, Easy) (45–60 min)

Create: `week5.day3.LC112PathSum`.

Given `targetSum`, return true if there exists a root-to-leaf path where sum of values is `targetSum`.

**Approach (recursive):**

```java
public boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) {
        return targetSum == root.val;
    }
    int remaining = targetSum - root.val;
    return hasPathSum(root.left, remaining) || hasPathSum(root.right, remaining);
}
```

Concepts reinforced:
- Passing partial results (remaining sum) down recursion.
- Root-to-leaf path detection.

### 3. Optional: LeetCode – Sum of Left Leaves (404, Easy) (30–45 min)

Create: `week5.day3.LC404SumOfLeftLeaves`.

- Recursively collect values of left leaf nodes.

---

## Day 4 – BFS on Trees: Level Order Traversal

**Goals:**
- Learn BFS on trees using a queue.
- Solve level-based tree problems.

### 1. Concept Primer: BFS on Trees (20–30 min)

- Use `Queue<TreeNode>` (e.g., `ArrayDeque`).
- Level-order traversal:
  - Enqueue root.
  - While queue not empty:
    - Pop node.
    - Enqueue its children.
- For level grouping, track queue size at each level.

### 2. Implement Simple Level-Order Print (30–45 min)

Create: `week5.day4.LevelOrderDemo`.

Implement:

```java
public static void levelOrderPrint(TreeNode root) {
    if (root == null) return;
    Queue<TreeNode> queue = new ArrayDeque<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            System.out.print(node.val + " ");
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        System.out.println(); // new line per level
    }
}
```

Concepts reinforced:
- BFS pattern with queue.
- Processing nodes level by level.

### 3. LeetCode: Binary Tree Level Order Traversal (102, Medium) (45–60 min)

Create: `week5.day4.LC102LevelOrderTraversal`.

Similar to above, but return `List<List<Integer>>`.

Steps:
- Initialize `List<List<Integer>> result = new ArrayList<>();`
- Use BFS with queue.
- For each level:
  - Create `List<Integer> level = new ArrayList<>();`
  - Fill it with current level nodes.
  - Add to result.

### 4. Optional: Binary Tree Level Order Traversal II (107, Medium) (30–45 min)

Create: `week5.day4.LC107LevelOrderBottom`.

- Same as 102, but bottom-up (reverse result at the end or insert at index 0).

---

## Day 5 – Binary Search Tree (BST) Basics

**Goals:**
- Understand BST property.
- Implement search/insert in BST.
- Use BST property for LeetCode problems.

### 1. Concept Primer: BSTs (20–30 min)

BST property:
- For any node:
  - All nodes in left subtree have values `< node.val`.
  - All nodes in right subtree have values `> node.val`.
- Inorder traversal of BST → sorted ascending sequence.

Typical operations:
- Search, insert, delete (we’ll do search & insert for now).

### 2. Implement BST Search & Insert (45–60 min)

Create: `week5.day5.BSTBasics`.

Implement:

1. Search (recursive):

   ```java
   public static boolean searchBST(TreeNode root, int target) {
       if (root == null) return false;
       if (root.val == target) return true;
       if (target < root.val) return searchBST(root.left, target);
       else return searchBST(root.right, target);
   }
   ```

2. Insert:

   ```java
   public static TreeNode insertBST(TreeNode root, int val) {
       if (root == null) return new TreeNode(val);
       if (val < root.val) root.left = insertBST(root.left, val);
       else if (val > root.val) root.right = insertBST(root.right, val);
       // ignoring duplicates for now
       return root;
   }
   ```

Test:
- Build a BST from an array `{5, 3, 7, 2, 4, 6, 8}` by repeated insert.
- Test search for several values.

### 3. LeetCode: Validate Binary Search Tree (98, Medium) (45–60 min)

Create: `week5.day5.LC98ValidateBST`.

Two common approaches:

**Approach A – Inorder traversal produces ascending sequence:**
- Use a global/field variable to track previous value; ensure current > previous.

**Approach B – Bounds (recommended to understand):**

```java
public boolean isValidBST(TreeNode root) {
    return helper(root, null, null);
}

private boolean helper(TreeNode node, Integer lower, Integer upper) {
    if (node == null) return true;
    int val = node.val;
    if (lower != null && val <= lower) return false;
    if (upper != null && val >= upper) return false;
    return helper(node.left, lower, val) && helper(node.right, val, upper);
}
```

Concepts reinforced:
- Carrying constraints down recursion (min/max bounds).
- Using BST property correctly.

### 4. Optional: Search in a Binary Search Tree (700, Easy) (20–30 min)

Create: `week5.day5.LC700SearchBST`.

- Very similar to the search method you wrote.

---

## Day 6 – BST & Tree Practice: LCA, Kth Smallest, More Paths

**Goals:**
- Practice more BST-specific reasoning.
- Reinforce tree recursion on paths.

### 1. LeetCode: Lowest Common Ancestor of a BST (235, Easy/Medium) (45–60 min)

Create: `week5.day6.LC235LCAofBST`.

**Approach (exploit BST property):**

For nodes `p` and `q`:

- If both `p.val` and `q.val` < `root.val` → LCA is in left subtree.
- If both > `root.val` → LCA is in right subtree.
- Otherwise (they split or one equals root) → root is LCA.

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    int pv = p.val, qv = q.val;
    TreeNode curr = root;
    while (curr != null) {
        if (pv < curr.val && qv < curr.val) {
            curr = curr.left;
        } else if (pv > curr.val && qv > curr.val) {
            curr = curr.right;
        } else {
            return curr;
        }
    }
    return null;
}
```

Concepts reinforced:
- Moving down BST based on value comparisons.

### 2. LeetCode: Kth Smallest Element in a BST (230, Medium) (45–60 min)

Create: `week5.day6.LC230KthSmallest`.

**Idea:**
- Inorder traversal of BST yields sorted order.
- Perform inorder and count nodes until k.

Implementation sketch:
- Use a global counter and result variable, or
- Use a helper that returns after finding kth.

Concepts reinforced:
- Using inorder traversal result property.
- Managing state across recursion (counter).

### 3. LeetCode: Path Sum II (113, Medium) – Optional Stretch (45–60 min)

Create: `week5.day6.LC113PathSumII`.

**Approach:**
- Similar to Path Sum I, but record all root-to-leaf paths where sum matches.
- Use backtracking:
  - Maintain `List<Integer> path`.
  - On visiting a node, add its value.
  - If leaf and sum matches, add a copy of `path` to result list.
  - Recurse left/right.
  - Remove last element (backtrack).

Concepts reinforced:
- Combining recursion with backtracking.
- Managing mutable lists in recursion.

---

## Day 7 – Integration, Review, and Self-Test

**Goals:**
- Solidify tree & BST concepts.
- Re-solve key problems independently.
- Ensure traversals/DFS/BFS are intuitive.

### 1. Written Concept Check (20–30 min)

Without code, write answers to:

1. What are preorder, inorder, and postorder traversals, in words?
2. Describe BFS level-order traversal using a queue.
3. State the BST property.
4. Explain why inorder on a BST gives a sorted sequence.

Then:
- Sketch pseudocode for:
  - `maxDepth(TreeNode root)`
  - `isValidBST(TreeNode root)` (either bounds or inorder)

### 2. Re-solve Core Problems From Scratch (60–90 min)

In new files (no copy-paste), solve at least **5** of these:

1. **Maximum Depth of Binary Tree (104, Easy)**  
2. **Balanced Binary Tree (110, Easy)**  
3. **Symmetric Tree (101, Easy)**  
4. **Binary Tree Level Order Traversal (102, Medium)**  
5. **Path Sum (112, Easy)**  
6. **Validate Binary Search Tree (98, Medium)**  
7. **Lowest Common Ancestor of a BST (235, Easy/Medium)**  
8. **Kth Smallest Element in a BST (230, Medium)** (stretch)

For each:
- Write 3–5 lines of pseudocode first.
- After coding, note:
  - Pattern: DFS recursive / BFS with queue / BST property.
  - Time complexity: typically O(n).
  - Space: O(h) for recursion, plus any extra structures.

### 3. Reflection & Prep for Week 6 (15–30 min)

Ask yourself:

1. Which traversal is most intuitive? Least intuitive?
2. Do I know when to use:
   - DFS recursion vs BFS with queue?
   - Pure tree DFS vs backtracking (e.g., Path Sum II)?
3. Does the BST property feel natural now (can I use it without thinking too hard)?

Note any problem types that felt confusing; they’re prime candidates to revisit before you start **Week 6**, where you’ll dive more into:

- Recursion & Backtracking patterns (beyond trees)
- More complex tree path/combination problems
- General backtracking on arrays/strings (subsets, permutations, combinations)

If you want, next I can:
- Generate a **Day 1–7 plan for Week 6 (Recursion & Backtracking)**, or
- Provide a one-page **Tree & BST cheat sheet** with code templates and pattern summaries.
