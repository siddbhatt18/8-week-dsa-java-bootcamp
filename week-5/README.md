Here’s your **Week 5 – Day 1 to Day 7 plan**, focused on:

- Binary Trees & Binary Search Trees (BST)
- Recursive thinking
- Fundamental tree problems on LeetCode

Assume ~1.5–2 hours per day. Keep the flow: concept → implement small pieces → LeetCode → reflect.

---

## Week 5 Focus

- Tree representation in Java (`TreeNode`)
- DFS traversals: preorder, inorder, postorder (mostly recursive)
- BFS (level-order) using a queue
- Classic tree problems: height, symmetry, path sums
- BST properties and how they simplify search / insert / LCA

---

## Day 1 – Tree & BST Basics, DFS Traversals

**Goal:** Understand what trees are, how they’re represented, and basic recursive traversals.

### 1. Concept: Trees vs BSTs (25–30 min)

In notes (no code yet):

- **Binary Tree**:
  - Each node has up to 2 children: `left`, `right`.
  - No specific ordering requirement.
- **Binary Search Tree (BST)**:
  - For each node `x`:
    - All values in `x.left` are `< x.val`
    - All values in `x.right` are `> x.val`
  - Enables O(log n) search (in a balanced tree).

Standard node definition in Java:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int val) { this.val = val; }
}
```

Tree traversal types:

- **Preorder**: root → left → right
- **Inorder**: left → root → right
- **Postorder**: left → right → root

### 2. Implement Traversals (60–75 min)

In a `TreeDemo` class, implement recursive methods:

1. **Preorder Traversal (print values)**

```java
void preorder(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val + " ");
    preorder(root.left);
    preorder(root.right);
}
```

2. **Inorder Traversal**

```java
void inorder(TreeNode root) {
    if (root == null) return;
    inorder(root.left);
    System.out.print(root.val + " ");
    inorder(root.right);
}
```

3. **Postorder Traversal**

```java
void postorder(TreeNode root) {
    if (root == null) return;
    postorder(root.left);
    postorder(root.right);
    System.out.print(root.val + " ");
}
```

Manually build a small tree and test:

```java
TreeNode root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);
```

Run preorder/inorder/postorder and write down the outputs.

### 3. Simple Property Functions (20–30 min)

Implement:

1. **Compute height (max depth) of tree**

```java
int height(TreeNode root) {
    if (root == null) return 0;
    int leftH = height(root.left);
    int rightH = height(root.right);
    return 1 + Math.max(leftH, rightH);
}
```

2. **Count nodes in a tree**

```java
int countNodes(TreeNode root) {
    if (root == null) return 0;
    return 1 + countNodes(root.left) + countNodes(root.right);
}
```

**Reflection (10–15 min)**  
- Notice how similar these recursive functions look:
  - Base case (null).
  - Recursive calls on left/right.
  - Combines results (max or sum).

---

## Day 2 – Level-Order (BFS) and Basic Tree LeetCode

**Goal:** Learn BFS using a queue and solve first few tree problems on LeetCode.

### 1. Concept: Level-Order Traversal (20–30 min)

Idea:
- Visit nodes level by level.
- Use a queue:
  - Start with root in queue.
  - While queue not empty:
    - Pop current node.
    - Push children.

Pseudocode:

```java
Queue<TreeNode> q = new LinkedList<>();
q.offer(root);
while (!q.isEmpty()) {
    TreeNode node = q.poll();
    // process node
    if (node.left != null) q.offer(node.left);
    if (node.right != null) q.offer(node.right);
}
```

### 2. Implement Level-Order Traversal (45–60 min)

1. **Simple level-order (print values)**

```java
void levelOrderPrint(TreeNode root) {
    if (root == null) return;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        TreeNode node = q.poll();
        System.out.print(node.val + " ");
        if (node.left != null) q.offer(node.left);
        if (node.right != null) q.offer(node.right);
    }
}
```

2. **Level-order by level (return list of lists)**

```java
List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) return res;

    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    while (!q.isEmpty()) {
        int size = q.size();
        List<Integer> level = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            level.add(node.val);
            if (node.left != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
        res.add(level);
    }
    return res;
}
```

### 3. LeetCode Practice (45–60 min)

1. **Maximum Depth of Binary Tree** (`#104`, Easy)
   - Use your `height` function (recursion).

2. **Same Tree** (`#100`, Easy)
   - Recursively compare:
     - Both null → true
     - One null, one not → false
     - Values equal → compare left & right.

If extra time:
3. **Binary Tree Level Order Traversal** (`#102`, Medium)
   - Use level-order function you wrote.

**Reflection (10–15 min)**  
- How did BFS (queue) feel compared to DFS (recursion)?
- Note what “per level” code pattern looks like (`int size = q.size()` loop).

---

## Day 3 – Symmetry, Invert, and Intro BST Search

**Goal:** Practice tree recursion on symmetrical structures and start using BST properties.

### 1. Invert & Symmetric Trees (40–60 min)

Implement:

1. **Invert Binary Tree** (`#226`, Easy)

```java
TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    TreeNode left = invertTree(root.left);
    TreeNode right = invertTree(root.right);
    root.left = right;
    root.right = left;
    return root;
}
```

2. **Symmetric Tree** (`#101`, Easy/Medium)

- Define helper function that checks if two subtrees are mirror images:

```java
boolean isMirror(TreeNode t1, TreeNode t2) {
    if (t1 == null && t2 == null) return true;
    if (t1 == null || t2 == null) return false;
    return (t1.val == t2.val)
        && isMirror(t1.left, t2.right)
        && isMirror(t1.right, t2.left);
}

boolean isSymmetric(TreeNode root) {
    if (root == null) return true;
    return isMirror(root.left, root.right);
}
```

### 2. BST Search & Insert (30–40 min)

In a `BSTDemo` class, implement:

1. **Search in BST** (recursive)

```java
TreeNode searchBST(TreeNode root, int val) {
    if (root == null || root.val == val) return root;
    if (val < root.val) return searchBST(root.left, val);
    else return searchBST(root.right, val);
}
```

2. **Insert into BST** (recursive)

```java
TreeNode insertIntoBST(TreeNode root, int val) {
    if (root == null) return new TreeNode(val);
    if (val < root.val) root.left = insertIntoBST(root.left, val);
    else if (val > root.val) root.right = insertIntoBST(root.right, val);
    return root;
}
```

Test:
- Build a small BST by inserting values one by one.
- Search for various values and print whether found.

### 3. LeetCode Practice (30–45 min)

1. **Invert Binary Tree** (`#226`, Easy)
2. **Symmetric Tree** (`#101`, Easy/Medium)

If time:
3. **Search in a Binary Search Tree** (`#700`, Easy)
   - Reuse your `searchBST`.

**Reflection (10–15 min)**  
- Notice how every tree/BST function starts with a null check.
- What differences do you see between generic tree recursion and BST-specific recursion?

---

## Day 4 – Validate BST & Lowest Common Ancestor (BST)

**Goal:** Use BST properties more deeply: validation and LCA.

### 1. Validate BST (45–60 min)

Two approaches; implement at least one.

**Approach 1 – Using Min/Max Bounds**

```java
boolean isValidBST(TreeNode root) {
    return isValidBST(root, null, null);
}

boolean isValidBST(TreeNode node, Integer min, Integer max) {
    if (node == null) return true;
    if (min != null && node.val <= min) return false;
    if (max != null && node.val >= max) return false;
    return isValidBST(node.left, min, node.val)
        && isValidBST(node.right, node.val, max);
}
```

**Approach 2 – Inorder Traversal**

- Inorder traversal of BST should produce a strictly increasing sequence.
- Keep track of previous value.

### 2. Lowest Common Ancestor in BST (30–45 min)

`#235` LCA of a BST:

- Given `p` and `q` in a BST:
  - If both < root.val → LCA is in left subtree.
  - If both > root.val → LCA is in right subtree.
  - Else root is LCA.

```java
TreeNode lowestCommonAncestorBST(TreeNode root, TreeNode p, TreeNode q) {
    int pv = p.val, qv = q.val;
    while (root != null) {
        if (pv < root.val && qv < root.val) {
            root = root.left;
        } else if (pv > root.val && qv > root.val) {
            root = root.right;
        } else {
            return root;
        }
    }
    return null;
}
```

### 3. LeetCode Practice (45–60 min)

1. **Validate Binary Search Tree** (`#98`, Medium)
   - Use the min/max bounds method.

2. **Lowest Common Ancestor of a BST** (`#235`, Easy/Medium)
   - Use the BST-based logic above.

If time:
3. **Search in a Binary Search Tree** (`#700`, Easy) again for speed.

**Reflection (10–15 min)**  
- Compare how BST property simplifies LCA here compared to a general binary tree (which you’ll see later if you want).
- Which `isValidBST` approach felt more intuitive?

---

## Day 5 – Path Sums & Tree Recursion Patterns

**Goal:** Understand recursive path sum problems and backtracking over tree paths.

### 1. Concept: Root-to-Leaf Paths (20–30 min)

Patterns:

- You often need to:
  - Track current sum or path.
  - Make a choice at node, recurse to children, then “undo” (backtrack) if needed.
- Classic problems:
  - Check if any path equals target sum.
  - Collect all paths with target sum.

### 2. LeetCode Practice – Path Sum (60–75 min)

1. **Path Sum** (`#112`, Easy)
   - Return true if some root-to-leaf path sums to target.
   - Recursive pattern:

```java
boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) {
        return root.val == targetSum;
    }
    int remaining = targetSum - root.val;
    return hasPathSum(root.left, remaining) || hasPathSum(root.right, remaining);
}
```

2. **Path Sum II** (`#113`, Medium)
   - Collect all root-to-leaf paths whose sum equals target.
   - Use backtracking:

```java
void dfs(TreeNode node, int target, List<Integer> path, List<List<Integer>> res) {
    if (node == null) return;
    path.add(node.val);
    if (node.left == null && node.right == null && target == node.val) {
        res.add(new ArrayList<>(path));
    } else {
        dfs(node.left, target - node.val, path, res);
        dfs(node.right, target - node.val, path, res);
    }
    path.remove(path.size() - 1); // backtrack
}
```

3. If time / energy:
   - **Sum Root to Leaf Numbers** (`#129`, Medium)  
     - Similar root-to-leaf idea, but treat path as digits of a number.

### 3. Quick Review of Past Problems (20–30 min)

Revisit (just scan code or restate logic):

- `#104 Maximum Depth of Binary Tree`
- `#101 Symmetric Tree`
- `#226 Invert Binary Tree`

**Reflection (10–15 min)**  
- Notice the recurring recursion pattern:
  - Base case null → return something simple.
  - Work at current node.
  - Recurse to children.
  - Optionally backtrack (if tracking a path list).

---

## Day 6 – Combined Practice: DFS/BFS Mix

**Goal:** Consolidate tree, BST, and BFS/DFS skills with a mixed problem set.

### 1. Quick Recap (20–30 min)

In your notebook, without code:

- Sketch pseudocode for:
  - `maxDepth` (`#104`)
  - `isSymmetric` (`#101`)
  - `isValidBST` (`#98`)
  - Level-order traversal (queue-based)

### 2. LeetCode Practice (75–105 min)

Try to solve or re-solve:

1. **Maximum Depth of Binary Tree** (`#104`, Easy)
2. **Same Tree** (`#100`, Easy)
3. **Binary Tree Level Order Traversal** (`#102`, Medium)
4. **Invert Binary Tree** (`#226`, Easy)
5. **Validate Binary Search Tree** (`#98`, Medium)

If you’re fast:
6. **Path Sum** (`#112`, Easy)

Aim for:
- ~15–20 minutes per easy problem.
- ~25–30 minutes for mediums.

### 3. Optional: Non-BST LCA (Stretch, 20–30 min)

If you want an additional challenge:

- **Lowest Common Ancestor of a Binary Tree** (`#236`, Medium)
  - General binary tree (no BST property).
  - Pattern:
    - Recurse left/right.
    - If both sides return non-null → current is LCA.
    - If one side non-null → propagate up.

Even if you just read / partially attempt, it builds intuition.

**Reflection (10–15 min)**  
- Which problems felt straightforward now vs earlier in the week?
- Where does BFS (queue) feel more natural than DFS (recursion), and vice versa?

---

## Day 7 – Review, Speed Practice, and Light Stretch

**Goal:** Tie tree & BST knowledge together and test under light time pressure.

### 1. Concept Review (30–40 min)

Write short answers:

- Difference between:
  - Binary Tree vs BST.
  - DFS vs BFS on a tree.
- For each of these, briefly describe the key idea:
  - **Max Depth** (`#104`)
  - **Symmetric Tree** (`#101`)
  - **Validate BST** (`#98`)
  - **LCA of BST** (`#235`)
  - **Path Sum** (`#112`)

Also, write down:

- What’s the **inorder** traversal of a BST and why is it useful?

### 2. Timed Re-Solves (60–90 min)

Pick 4–6 problems and give yourself **≤25 minutes each**:

Suggested set:
- `#104 Maximum Depth of Binary Tree`
- `#226 Invert Binary Tree`
- `#101 Symmetric Tree`
- `#102 Binary Tree Level Order Traversal`
- `#98 Validate Binary Search Tree`
- `#235 Lowest Common Ancestor of a BST`

Try to:
1. Spend 5–7 minutes planning (on paper).
2. Code cleanly in one pass.
3. Check logic with 1–2 small custom examples before submitting.

### 3. Stretch Problem (Optional, 30–45 min)

Choose one that you haven’t deeply solved yet:

- `#113 Path Sum II`  
- `#129 Sum Root to Leaf Numbers`  
- Or revisit `#236 LCA of a Binary Tree`

Even 30 minutes of serious thinking is useful, even if you don’t fully solve it.

**Reflection (10–15 min)**  
- Which tree pattern do you feel strongest at (depth, symmetry, BST, path sum, level-order)?
- Which still feels shaky? We can emphasize that in later review.

---

## How Week 5 Fits the Bigger Picture

By the end of Week 5, you should:

- Be comfortable with:
  - Writing recursive DFS on trees (preorder/inorder/postorder).
  - BFS with a queue for level-order.
  - Basic BST operations and using BST properties.
- Recognize key **tree problem patterns** that occur over and over (depth, symmetry, path sums, BST validation, LCA).

Next (Week 6), you’ll:

- Extend DFS/BFS ideas to **graphs** (adjacency lists, visited sets).
- Practice **grid-as-graph** problems (Number of Islands, Flood Fill).
- Learn **backtracking** for combinatorial problems (Subsets, Permutations, Combination Sum).

If you want, I can next generate a **Week 6 – Day 1–7 plan** covering graphs + backtracking.
