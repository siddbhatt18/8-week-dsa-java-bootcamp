# Week 5: Binary Trees & Tree Traversal - Daily Structured Plan

## 📅 **DAY 1: Binary Tree Fundamentals & Traversals**

### 🌅 **Morning Session (45 minutes)**
#### Understanding Binary Trees
- **Core Concepts:**
  - Tree terminology (root, leaf, parent, child, height, depth)
  - Binary tree vs Binary Search Tree
  - Complete vs Full vs Perfect binary trees
  - Tree representation and properties

#### Tree Node Implementation & Basic Operations:
```java
// Basic TreeNode structure
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    
    TreeNode() {}
    
    TreeNode(int val) {
        this.val = val;
    }
    
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

// Tree basics and terminology
class TreeBasics {
    // Build tree from array (level order)
    public TreeNode buildTree(Integer[] arr) {
        if (arr.length == 0 || arr[0] == null) return null;
        
        TreeNode root = new TreeNode(arr[0]);
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int i = 1;
        
        while (!queue.isEmpty() && i < arr.length) {
            TreeNode current = queue.poll();
            
            // Add left child
            if (i < arr.length && arr[i] != null) {
                current.left = new TreeNode(arr[i]);
                queue.offer(current.left);
            }
            i++;
            
            // Add right child
            if (i < arr.length && arr[i] != null) {
                current.right = new TreeNode(arr[i]);
                queue.offer(current.right);
            }
            i++;
        }
        
        return root;
    }
    
    // Count nodes in tree
    public int countNodes(TreeNode root) {
        if (root == null) return 0;
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
    
    // Calculate tree height
    public int height(TreeNode root) {
        if (root == null) return -1; // or 0 depending on definition
        return 1 + Math.max(height(root.left), height(root.right));
    }
    
    // Check if leaf node
    public boolean isLeaf(TreeNode node) {
        return node != null && node.left == null && node.right == null;
    }
    
    // Count leaf nodes
    public int countLeaves(TreeNode root) {
        if (root == null) return 0;
        if (isLeaf(root)) return 1;
        return countLeaves(root.left) + countLeaves(root.right);
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### DFS Traversals (Recursive)
```java
class DFSTraversals {
    // Inorder Traversal (Left -> Root -> Right)
    // For BST: gives sorted order
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        inorderHelper(root, result);
        return result;
    }
    
    private void inorderHelper(TreeNode node, List<Integer> result) {
        if (node == null) return;
        
        inorderHelper(node.left, result);   // Process left subtree
        result.add(node.val);                // Process root
        inorderHelper(node.right, result);  // Process right subtree
    }
    
    // Preorder Traversal (Root -> Left -> Right)
    // Used for: copying tree, prefix expression
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        preorderHelper(root, result);
        return result;
    }
    
    private void preorderHelper(TreeNode node, List<Integer> result) {
        if (node == null) return;
        
        result.add(node.val);                // Process root
        preorderHelper(node.left, result);   // Process left subtree
        preorderHelper(node.right, result);  // Process right subtree
    }
    
    // Postorder Traversal (Left -> Right -> Root)
    // Used for: deleting tree, postfix expression
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        postorderHelper(root, result);
        return result;
    }
    
    private void postorderHelper(TreeNode node, List<Integer> result) {
        if (node == null) return;
        
        postorderHelper(node.left, result);   // Process left subtree
        postorderHelper(node.right, result);  // Process right subtree
        result.add(node.val);                 // Process root
    }
    
    // Traversal with detailed logging
    public void demonstrateTraversals(TreeNode root) {
        System.out.println("Tree Traversal Demonstration");
        System.out.println("============================");
        
        // Inorder
        System.out.print("Inorder (L-Root-R): ");
        inorderPrint(root);
        System.out.println();
        
        // Preorder
        System.out.print("Preorder (Root-L-R): ");
        preorderPrint(root);
        System.out.println();
        
        // Postorder
        System.out.print("Postorder (L-R-Root): ");
        postorderPrint(root);
        System.out.println();
    }
    
    private void inorderPrint(TreeNode node) {
        if (node == null) return;
        inorderPrint(node.left);
        System.out.print(node.val + " ");
        inorderPrint(node.right);
    }
    
    private void preorderPrint(TreeNode node) {
        if (node == null) return;
        System.out.print(node.val + " ");
        preorderPrint(node.left);
        preorderPrint(node.right);
    }
    
    private void postorderPrint(TreeNode node) {
        if (node == null) return;
        postorderPrint(node.left);
        postorderPrint(node.right);
        System.out.print(node.val + " ");
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### DFS Traversals (Iterative)
```java
class IterativeTraversals {
    // Iterative Inorder
    public List<Integer> inorderIterative(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode current = root;
        
        while (current != null || !stack.isEmpty()) {
            // Go to leftmost node
            while (current != null) {
                stack.push(current);
                current = current.left;
            }
            
            // Current is null here
            current = stack.pop();
            result.add(current.val);
            current = current.right;
        }
        
        return result;
    }
    
    // Iterative Preorder
    public List<Integer> preorderIterative(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.add(node.val);
            
            // Push right first so left is processed first
            if (node.right != null) stack.push(node.right);
            if (node.left != null) stack.push(node.left);
        }
        
        return result;
    }
    
    // Iterative Postorder (using two stacks)
    public List<Integer> postorderIterative(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        
        Stack<TreeNode> stack1 = new Stack<>();
        Stack<TreeNode> stack2 = new Stack<>();
        
        stack1.push(root);
        
        // First stack: Root -> Right -> Left
        while (!stack1.isEmpty()) {
            TreeNode node = stack1.pop();
            stack2.push(node);
            
            if (node.left != null) stack1.push(node.left);
            if (node.right != null) stack1.push(node.right);
        }
        
        // Second stack gives postorder
        while (!stack2.isEmpty()) {
            result.add(stack2.pop().val);
        }
        
        return result;
    }
}
```

### 📝 **Day 1 Checklist**
- [ ] Understand tree terminology and properties
- [ ] Implement tree node structure
- [ ] Master recursive DFS traversals (in/pre/post)
- [ ] Implement iterative traversals
- [ ] Understand when to use each traversal type

---

## 📅 **DAY 2: BFS and Level Order Traversal**

### 🌅 **Morning Session (45 minutes)**
#### Level Order Traversal (BFS)
```java
class BFSTraversal {
    // Basic level order traversal
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            List<Integer> currentLevel = new ArrayList<>();
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                currentLevel.add(node.val);
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            
            result.add(currentLevel);
        }
        
        return result;
    }
    
    // Zigzag level order traversal
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        boolean leftToRight = true;
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            LinkedList<Integer> currentLevel = new LinkedList<>();
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                
                if (leftToRight) {
                    currentLevel.addLast(node.val);
                } else {
                    currentLevel.addFirst(node.val);
                }
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            
            result.add(currentLevel);
            leftToRight = !leftToRight;
        }
        
        return result;
    }
    
    // Level order bottom (reverse order)
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        LinkedList<List<Integer>> result = new LinkedList<>();
        if (root == null) return result;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            List<Integer> currentLevel = new ArrayList<>();
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                currentLevel.add(node.val);
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            
            result.addFirst(currentLevel);  // Add to beginning
        }
        
        return result;
    }
    
    // Find level with maximum sum
    public int maxLevelSum(TreeNode root) {
        if (root == null) return 0;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        int maxSum = Integer.MIN_VALUE;
        int maxLevel = 1;
        int currentLevel = 1;
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            int levelSum = 0;
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                levelSum += node.val;
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            
            if (levelSum > maxSum) {
                maxSum = levelSum;
                maxLevel = currentLevel;
            }
            
            currentLevel++;
        }
        
        return maxLevel;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Advanced BFS Applications
```java
class AdvancedBFS {
    // Right side view of tree
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                
                // Add the last node of each level
                if (i == levelSize - 1) {
                    result.add(node.val);
                }
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
        }
        
        return result;
    }
    
    // Left side view of tree
    public List<Integer> leftSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                
                // Add the first node of each level
                if (i == 0) {
                    result.add(node.val);
                }
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
        }
        
        return result;
    }
    
    // Find bottom left value
    public int findBottomLeftValue(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int bottomLeft = root.val;
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                
                if (i == 0) {
                    bottomLeft = node.val;  // First node of each level
                }
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
        }
        
        return bottomLeft;
    }
    
    // Average of levels
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> result = new ArrayList<>();
        if (root == null) return result;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            double levelSum = 0;
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                levelSum += node.val;
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            
            result.add(levelSum / levelSize);
        }
        
        return result;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
- **Then:** [103. Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

### 📝 **Day 2 Checklist**
- [ ] Master level order traversal pattern
- [ ] Implement zigzag traversal
- [ ] Understand queue usage in BFS
- [ ] Complete level order traversal problem
- [ ] Solve zigzag traversal variation

---

## 📅 **DAY 3: Tree Properties and Recursion Patterns**

### 🌅 **Morning Session (45 minutes)**
#### Basic Tree Properties
```java
class TreeProperties {
    // Maximum depth of binary tree
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        
        return 1 + Math.max(leftDepth, rightDepth);
    }
    
    // Minimum depth of binary tree
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        
        // If one subtree is null, return the other
        if (root.left == null) return 1 + minDepth(root.right);
        if (root.right == null) return 1 + minDepth(root.left);
        
        // Both subtrees exist
        return 1 + Math.min(minDepth(root.left), minDepth(root.right));
    }
    
    // Check if balanced
    public boolean isBalanced(TreeNode root) {
        return checkHeight(root) != -1;
    }
    
    private int checkHeight(TreeNode node) {
        if (node == null) return 0;
        
        int leftHeight = checkHeight(node.left);
        if (leftHeight == -1) return -1;  // Left subtree not balanced
        
        int rightHeight = checkHeight(node.right);
        if (rightHeight == -1) return -1;  // Right subtree not balanced
        
        // Check if current node is balanced
        if (Math.abs(leftHeight - rightHeight) > 1) return -1;
        
        return 1 + Math.max(leftHeight, rightHeight);
    }
    
    // Diameter of binary tree
    public int diameterOfBinaryTree(TreeNode root) {
        int[] diameter = new int[1];  // Use array to pass by reference
        height(root, diameter);
        return diameter[0];
    }
    
    private int height(TreeNode node, int[] diameter) {
        if (node == null) return 0;
        
        int leftHeight = height(node.left, diameter);
        int rightHeight = height(node.right, diameter);
        
        // Update diameter if path through current node is longer
        diameter[0] = Math.max(diameter[0], leftHeight + rightHeight);
        
        return 1 + Math.max(leftHeight, rightHeight);
    }
    
    // Check if symmetric
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        return isMirror(root.left, root.right);
    }
    
    private boolean isMirror(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) return true;
        if (t1 == null || t2 == null) return false;
        
        return (t1.val == t2.val) 
            && isMirror(t1.left, t2.right) 
            && isMirror(t1.right, t2.left);
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Tree Comparison and Modification
```java
class TreeOperations {
    // Check if two trees are same
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        
        return p.val == q.val 
            && isSameTree(p.left, q.left) 
            && isSameTree(p.right, q.right);
    }
    
    // Check if subtree
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (root == null) return false;
        
        if (isSameTree(root, subRoot)) return true;
        
        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
    }
    
    // Invert binary tree
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        
        // Swap left and right children
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        
        // Recursively invert subtrees
        invertTree(root.left);
        invertTree(root.right);
        
        return root;
    }
    
    // Merge two binary trees
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if (root1 == null) return root2;
        if (root2 == null) return root1;
        
        // Merge nodes
        root1.val += root2.val;
        
        // Recursively merge subtrees
        root1.left = mergeTrees(root1.left, root2.left);
        root1.right = mergeTrees(root1.right, root2.right);
        
        return root1;
    }
    
    // Flatten tree to linked list (preorder)
    public void flatten(TreeNode root) {
        if (root == null) return;
        
        flattenHelper(root);
    }
    
    private TreeNode flattenHelper(TreeNode node) {
        if (node == null) return null;
        
        // For leaf node
        if (node.left == null && node.right == null) {
            return node;
        }
        
        // Recursively flatten left subtree
        TreeNode leftTail = flattenHelper(node.left);
        
        // Recursively flatten right subtree
        TreeNode rightTail = flattenHelper(node.right);
        
        // Connect flattened subtrees
        if (leftTail != null) {
            leftTail.right = node.right;
            node.right = node.left;
            node.left = null;
        }
        
        return rightTail != null ? rightTail : leftTail;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- **Then:** [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
- **Bonus:** [100. Same Tree](https://leetcode.com/problems/same-tree/)

### 📝 **Day 3 Checklist**
- [ ] Calculate tree depth/height efficiently
- [ ] Check tree balance and symmetry
- [ ] Master tree comparison patterns
- [ ] Complete max depth problem
- [ ] Solve invert tree problem

---

## 📅 **DAY 4: Path Problems and DFS Applications**

### 🌅 **Morning Session (45 minutes)**
#### Path Sum Problems
```java
class PathProblems {
    // Has path sum
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        
        // Check if leaf node with target sum
        if (root.left == null && root.right == null) {
            return targetSum == root.val;
        }
        
        // Recursively check subtrees
        return hasPathSum(root.left, targetSum - root.val) 
            || hasPathSum(root.right, targetSum - root.val);
    }
    
    // Find all root-to-leaf paths with sum
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> currentPath = new ArrayList<>();
        pathSumHelper(root, targetSum, currentPath, result);
        return result;
    }
    
    private void pathSumHelper(TreeNode node, int targetSum, 
                               List<Integer> currentPath, 
                               List<List<Integer>> result) {
        if (node == null) return;
        
        currentPath.add(node.val);
        
        // Check if leaf node with target sum
        if (node.left == null && node.right == null && targetSum == node.val) {
            result.add(new ArrayList<>(currentPath));
        }
        
        // Explore subtrees
        pathSumHelper(node.left, targetSum - node.val, currentPath, result);
        pathSumHelper(node.right, targetSum - node.val, currentPath, result);
        
        // Backtrack
        currentPath.remove(currentPath.size() - 1);
    }
    
    // Path sum III (paths don't need to start at root or end at leaf)
    public int pathSum3(TreeNode root, int targetSum) {
        if (root == null) return 0;
        
        // Count paths from current node + paths in subtrees
        return pathsFromNode(root, targetSum) 
            + pathSum3(root.left, targetSum) 
            + pathSum3(root.right, targetSum);
    }
    
    private int pathsFromNode(TreeNode node, long targetSum) {
        if (node == null) return 0;
        
        int count = 0;
        if (node.val == targetSum) count++;
        
        count += pathsFromNode(node.left, targetSum - node.val);
        count += pathsFromNode(node.right, targetSum - node.val);
        
        return count;
    }
    
    // Maximum path sum (can start and end anywhere)
    public int maxPathSum(TreeNode root) {
        int[] maxSum = {Integer.MIN_VALUE};
        maxPathSumHelper(root, maxSum);
        return maxSum[0];
    }
    
    private int maxPathSumHelper(TreeNode node, int[] maxSum) {
        if (node == null) return 0;
        
        // Get max sum from left and right subtrees
        int leftMax = Math.max(0, maxPathSumHelper(node.left, maxSum));
        int rightMax = Math.max(0, maxPathSumHelper(node.right, maxSum));
        
        // Update global max with path through current node
        maxSum[0] = Math.max(maxSum[0], leftMax + rightMax + node.val);
        
        // Return max path sum including current node
        return node.val + Math.max(leftMax, rightMax);
    }
    
    // All root-to-leaf paths
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        if (root != null) {
            dfsPath(root, "", result);
        }
        return result;
    }
    
    private void dfsPath(TreeNode node, String path, List<String> result) {
        if (node.left == null && node.right == null) {
            result.add(path + node.val);
            return;
        }
        
        if (node.left != null) {
            dfsPath(node.left, path + node.val + "->", result);
        }
        if (node.right != null) {
            dfsPath(node.right, path + node.val + "->", result);
        }
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Ancestor and LCA Problems
```java
class AncestorProblems {
    // Lowest Common Ancestor in Binary Tree
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) {
            return root;
        }
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        // If both left and right are non-null, root is LCA
        if (left != null && right != null) {
            return root;
        }
        
        // Otherwise return non-null node
        return left != null ? left : right;
    }
    
    // LCA in Binary Search Tree (optimized)
    public TreeNode lowestCommonAncestorBST(TreeNode root, TreeNode p, TreeNode q) {
        while (root != null) {
            if (p.val < root.val && q.val < root.val) {
                root = root.left;
            } else if (p.val > root.val && q.val > root.val) {
                root = root.right;
            } else {
                return root;  // Split point or one node is root
            }
        }
        return null;
    }
    
    // Distance between two nodes
    public int findDistance(TreeNode root, int p, int q) {
        TreeNode lca = findLCA(root, p, q);
        return distanceFromNode(lca, p, 0) + distanceFromNode(lca, q, 0);
    }
    
    private TreeNode findLCA(TreeNode root, int p, int q) {
        if (root == null) return null;
        
        if (root.val == p || root.val == q) return root;
        
        TreeNode left = findLCA(root.left, p, q);
        TreeNode right = findLCA(root.right, p, q);
        
        if (left != null && right != null) return root;
        return left != null ? left : right;
    }
    
    private int distanceFromNode(TreeNode node, int target, int dist) {
        if (node == null) return -1;
        
        if (node.val == target) return dist;
        
        int left = distanceFromNode(node.left, target, dist + 1);
        if (left != -1) return left;
        
        return distanceFromNode(node.right, target, dist + 1);
    }
    
    // Sum of left leaves
    public int sumOfLeftLeaves(TreeNode root) {
        return sumOfLeftLeavesHelper(root, false);
    }
    
    private int sumOfLeftLeavesHelper(TreeNode node, boolean isLeft) {
        if (node == null) return 0;
        
        // Check if left leaf
        if (node.left == null && node.right == null && isLeft) {
            return node.val;
        }
        
        return sumOfLeftLeavesHelper(node.left, true) 
             + sumOfLeftLeavesHelper(node.right, false);
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [112. Path Sum](https://leetcode.com/problems/path-sum/)
- **Then:** [113. Path Sum II](https://leetcode.com/problems/path-sum-ii/)
- **Challenge:** [437. Path Sum III](https://leetcode.com/problems/path-sum-iii/)

### 📝 **Day 4 Checklist**
- [ ] Master path sum patterns
- [ ] Implement backtracking for paths
- [ ] Understand LCA algorithm
- [ ] Complete Path Sum I and II
- [ ] Attempt Path Sum III

---

## 📅 **DAY 5: Binary Search Trees (BST)**

### 🌅 **Morning Session (45 minutes)**
#### BST Properties and Validation
```java
class BSTOperations {
    // Validate BST
    public boolean isValidBST(TreeNode root) {
        return validate(root, null, null);
    }
    
    private boolean validate(TreeNode node, Integer min, Integer max) {
        if (node == null) return true;
        
        // Check current node
        if (min != null && node.val <= min) return false;
        if (max != null && node.val >= max) return false;
        
        // Recursively validate subtrees with updated bounds
        return validate(node.left, min, node.val) 
            && validate(node.right, node.val, max);
    }
    
    // Alternative: Using inorder traversal
    public boolean isValidBSTInorder(TreeNode root) {
        List<Integer> inorder = new ArrayList<>();
        inorderTraversal(root, inorder);
        
        // Check if inorder is sorted
        for (int i = 1; i < inorder.size(); i++) {
            if (inorder.get(i) <= inorder.get(i - 1)) {
                return false;
            }
        }
        return true;
    }
    
    private void inorderTraversal(TreeNode node, List<Integer> result) {
        if (node == null) return;
        
        inorderTraversal(node.left, result);
        result.add(node.val);
        inorderTraversal(node.right, result);
    }
    
    // Search in BST
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null || root.val == val) {
            return root;
        }
        
        if (val < root.val) {
            return searchBST(root.left, val);
        } else {
            return searchBST(root.right, val);
        }
    }
    
    // Insert into BST
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        
        if (val < root.val) {
            root.left = insertIntoBST(root.left, val);
        } else {
            root.right = insertIntoBST(root.right, val);
        }
        
        return root;
    }
    
    // Delete from BST
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return null;
        
        if (key < root.val) {
            root.left = deleteNode(root.left, key);
        } else if (key > root.val) {
            root.right = deleteNode(root.right, key);
        } else {
            // Node to delete found
            
            // Case 1: No children
            if (root.left == null && root.right == null) {
                return null;
            }
            
            // Case 2: One child
            if (root.left == null) return root.right;
            if (root.right == null) return root.left;
            
            // Case 3: Two children
            // Find inorder successor (min in right subtree)
            TreeNode minNode = findMin(root.right);
            root.val = minNode.val;
            root.right = deleteNode(root.right, minNode.val);
        }
        
        return root;
    }
    
    private TreeNode findMin(TreeNode node) {
        while (node.left != null) {
            node = node.left;
        }
        return node;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Advanced BST Operations
```java
class AdvancedBST {
    // Kth smallest element in BST
    public int kthSmallest(TreeNode root, int k) {
        int[] count = {0};
        int[] result = {0};
        inorderK(root, k, count, result);
        return result[0];
    }
    
    private void inorderK(TreeNode node, int k, int[] count, int[] result) {
        if (node == null) return;
        
        inorderK(node.left, k, count, result);
        
        count[0]++;
        if (count[0] == k) {
            result[0] = node.val;
            return;
        }
        
        inorderK(node.right, k, count, result);
    }
    
    // Convert sorted array to BST
    public TreeNode sortedArrayToBST(int[] nums) {
        return buildBST(nums, 0, nums.length - 1);
    }
    
    private TreeNode buildBST(int[] nums, int left, int right) {
        if (left > right) return null;
        
        int mid = left + (right - left) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        
        root.left = buildBST(nums, left, mid - 1);
        root.right = buildBST(nums, mid + 1, right);
        
        return root;
    }
    
    // Convert BST to greater tree
    public TreeNode convertBST(TreeNode root) {
        int[] sum = {0};
        reverseInorder(root, sum);
        return root;
    }
    
    private void reverseInorder(TreeNode node, int[] sum) {
        if (node == null) return;
        
        // Process right subtree first
        reverseInorder(node.right, sum);
        
        // Update node value
        sum[0] += node.val;
        node.val = sum[0];
        
        // Process left subtree
        reverseInorder(node.left, sum);
    }
    
    // Closest value in BST
    public int closestValue(TreeNode root, double target) {
        int closest = root.val;
        
        while (root != null) {
            if (Math.abs(root.val - target) < Math.abs(closest - target)) {
                closest = root.val;
            }
            
            root = target < root.val ? root.left : root.right;
        }
        
        return closest;
    }
    
    // Range sum of BST
    public int rangeSumBST(TreeNode root, int low, int high) {
        if (root == null) return 0;
        
        if (root.val < low) {
            return rangeSumBST(root.right, low, high);
        }
        if (root.val > high) {
            return rangeSumBST(root.left, low, high);
        }
        
        // root.val is in range
        return root.val 
            + rangeSumBST(root.left, low, high) 
            + rangeSumBST(root.right, low, high);
    }
    
    // BST iterator
    class BSTIterator {
        private Stack<TreeNode> stack;
        
        public BSTIterator(TreeNode root) {
            stack = new Stack<>();
            pushLeft(root);
        }
        
        private void pushLeft(TreeNode node) {
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
        }
        
        public int next() {
            TreeNode node = stack.pop();
            pushLeft(node.right);
            return node.val;
        }
        
        public boolean hasNext() {
            return !stack.isEmpty();
        }
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
- **Then:** [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

### 📝 **Day 5 Checklist**
- [ ] Understand BST properties
- [ ] Implement BST validation
- [ ] Master BST insertion/deletion
- [ ] Complete validate BST problem
- [ ] Solve kth smallest element

---

## 📅 **DAY 6: Practice & Complex Tree Problems**

### 🌅 **Morning Session (60 minutes)**
#### Tree Construction Problems
```java
class TreeConstruction {
    // Build tree from preorder and inorder
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        Map<Integer, Integer> inorderMap = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        
        int[] preIdx = {0};
        return build(preorder, inorderMap, preIdx, 0, inorder.length - 1);
    }
    
    private TreeNode build(int[] preorder, Map<Integer, Integer> inorderMap,
                          int[] preIdx, int inStart, int inEnd) {
        if (inStart > inEnd) return null;
        
        int rootVal = preorder[preIdx[0]++];
        TreeNode root = new TreeNode(rootVal);
        
        int inIdx = inorderMap.get(rootVal);
        
        root.left = build(preorder, inorderMap, preIdx, inStart, inIdx - 1);
        root.right = build(preorder, inorderMap, preIdx, inIdx + 1, inEnd);
        
        return root;
    }
    
    // Build tree from postorder and inorder
    public TreeNode buildTreePost(int[] inorder, int[] postorder) {
        Map<Integer, Integer> inorderMap = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        
        int[] postIdx = {postorder.length - 1};
        return buildPost(postorder, inorderMap, postIdx, 0, inorder.length - 1);
    }
    
    private TreeNode buildPost(int[] postorder, Map<Integer, Integer> inorderMap,
                              int[] postIdx, int inStart, int inEnd) {
        if (inStart > inEnd) return null;
        
        int rootVal = postorder[postIdx[0]--];
        TreeNode root = new TreeNode(rootVal);
        
        int inIdx = inorderMap.get(rootVal);
        
        // Build right subtree first for postorder
        root.right = buildPost(postorder, inorderMap, postIdx, inIdx + 1, inEnd);
        root.left = buildPost(postorder, inorderMap, postIdx, inStart, inIdx - 1);
        
        return root;
    }
    
    // Serialize and deserialize binary tree
    public class Codec {
        // Encodes a tree to a single string
        public String serialize(TreeNode root) {
            StringBuilder sb = new StringBuilder();
            serializeHelper(root, sb);
            return sb.toString();
        }
        
        private void serializeHelper(TreeNode node, StringBuilder sb) {
            if (node == null) {
                sb.append("null,");
                return;
            }
            
            sb.append(node.val).append(",");
            serializeHelper(node.left, sb);
            serializeHelper(node.right, sb);
        }
        
        // Decodes your encoded data to tree
        public TreeNode deserialize(String data) {
            Queue<String> queue = new LinkedList<>(Arrays.asList(data.split(",")));
            return deserializeHelper(queue);
        }
        
        private TreeNode deserializeHelper(Queue<String> queue) {
            String val = queue.poll();
            if (val.equals("null")) return null;
            
            TreeNode root = new TreeNode(Integer.parseInt(val));
            root.left = deserializeHelper(queue);
            root.right = deserializeHelper(queue);
            
            return root;
        }
    }
}
```

### 🌞 **Afternoon Session (90 minutes)**
#### Problem-Solving Session
**Solve these independently:**

```java
// 1. Count complete tree nodes
public int countNodes(TreeNode root) {
    // Your implementation
    // Hint: Use properties of complete tree for O(log n)^2
}

// 2. Populate next right pointers
public Node connect(Node root) {
    // Your implementation
    // Connect each node to its next right node
}

// 3. Find duplicate subtrees
public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
    // Your implementation
    // Use serialization and HashMap
}

// 4. Maximum width of binary tree
public int widthOfBinaryTree(TreeNode root) {
    // Your implementation
    // Use level order with position tracking
}
```

### 🌙 **Evening Session (45 minutes)**
#### LeetCode Challenge Problems
- **Complete:**
  1. [105. Construct Binary Tree from Preorder and Inorder](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
  2. [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
  3. [662. Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/)

### 📝 **Day 6 Checklist**
- [ ] Master tree construction from traversals
- [ ] Implement serialization/deserialization
- [ ] Complete tree construction problem
- [ ] Solve width of binary tree
- [ ] Practice mixed difficulty problems

---

## 📅 **DAY 7: Week Review & Advanced Applications**

### 🌅 **Morning Session (60 minutes)**
#### Comprehensive Review
```java
// TREE PATTERNS MASTERSHEET

class TreePatternsMaster {
    /* ========== TRAVERSAL PATTERNS ========== */
    
    // Pattern 1: Recursive DFS
    void recursiveDFS(TreeNode node) {
        if (node == null) return;  // Base case
        
        // Preorder: process here
        recursiveDFS(node.left);
        // Inorder: process here
        recursiveDFS(node.right);
        // Postorder: process here
    }
    
    // Pattern 2: Iterative with Stack
    void iterativeWithStack(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        // Traversal logic with stack
    }
    
    // Pattern 3: Level Order with Queue
    void levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                // Process level
            }
        }
    }
    
    /* ========== RECURSION PATTERNS ========== */
    
    // Pattern 1: Top-Down (Preorder style)
    void topDown(TreeNode node, int accumulated) {
        if (node == null) return;
        
        accumulated += node.val;  // Use parent info
        topDown(node.left, accumulated);
        topDown(node.right, accumulated);
    }
    
    // Pattern 2: Bottom-Up (Postorder style)
    int bottomUp(TreeNode node) {
        if (node == null) return 0;
        
        int left = bottomUp(node.left);
        int right = bottomUp(node.right);
        
        return Math.max(left, right) + 1;  // Use children info
    }
    
    // Pattern 3: Global Variable/Parameter
    int maxVal = Integer.MIN_VALUE;
    
    void withGlobal(TreeNode node) {
        if (node == null) return;
        
        maxVal = Math.max(maxVal, node.val);
        withGlobal(node.left);
        withGlobal(node.right);
    }
    
    /* ========== BST PATTERNS ========== */
    
    // Pattern 1: Inorder gives sorted sequence
    // Pattern 2: Binary search property for O(h) operations
    // Pattern 3: Range queries using BST property
    
    /* ========== PATH PATTERNS ========== */
    
    // Pattern 1: Root to leaf paths
    void rootToLeaf(TreeNode node, List<Integer> path) {
        if (node == null) return;
        
        path.add(node.val);
        
        if (node.left == null && node.right == null) {
            // Process complete path
        }
        
        rootToLeaf(node.left, new ArrayList<>(path));
        rootToLeaf(node.right, new ArrayList<>(path));
    }
    
    // Pattern 2: Any path (not necessarily root to leaf)
    int anyPath(TreeNode node) {
        if (node == null) return 0;
        
        int leftGain = Math.max(anyPath(node.left), 0);
        int rightGain = Math.max(anyPath(node.right), 0);
        
        // Update global max with path through node
        // Return max gain if continue path through node
        return node.val + Math.max(leftGain, rightGain);
    }
}
```

### 🌞 **Afternoon Session (90 minutes)**
#### Knowledge Assessment & Advanced Problems
```java
// SELF-ASSESSMENT QUIZ

/*
1. Time Complexity Analysis:
- DFS traversal: O(?)
- BFS traversal: O(?)
- Building tree from traversals: O(?)
- BST search/insert/delete average: O(?)
- BST search/insert/delete worst: O(?)

2. Space Complexity:
- Recursive DFS call stack: O(?)
- Iterative DFS with stack: O(?)
- BFS with queue: O(?)

3. Debug this code:
*/
public boolean isValidBST(TreeNode root) {
    return validate(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
}

private boolean validate(TreeNode node, int min, int max) {
    if (node == null) return true;
    
    if (node.val <= min || node.val >= max) return false;  // Bug?
    
    return validate(node.left, min, node.val) 
        && validate(node.right, node.val, max);
}

/*
4. Choose best approach:
Problem: Find all nodes at distance K from target
a) BFS from target
b) Convert to graph then BFS
c) Mark parents then BFS
d) DFS with distance tracking

5. Tree vs Graph:
What makes tree algorithms generally simpler than graph algorithms?
*/

// Advanced Challenge: Morris Traversal (O(1) space)
class MorrisTraversal {
    public List<Integer> inorderMorris(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        TreeNode current = root;
        
        while (current != null) {
            if (current.left == null) {
                result.add(current.val);
                current = current.right;
            } else {
                // Find predecessor
                TreeNode predecessor = current.left;
                while (predecessor.right != null && predecessor.right != current) {
                    predecessor = predecessor.right;
                }
                
                if (predecessor.right == null) {
                    // Make connection
                    predecessor.right = current;
                    current = current.left;
                } else {
                    // Restore tree and process current
                    predecessor.right = null;
                    result.add(current.val);
                    current = current.right;
                }
            }
        }
        
        return result;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Week 5 Complete Reference
```java
// WEEK 5 TREE MASTERY CHECKLIST

/* ========== MUST-KNOW ALGORITHMS ========== */
// ✓ DFS Traversals (in/pre/post - recursive & iterative)
// ✓ BFS/Level Order Traversal
// ✓ Tree height/depth calculation
// ✓ Path sum variations
// ✓ LCA finding
// ✓ BST validation
// ✓ Tree construction from traversals
// ✓ Serialization/Deserialization

/* ========== KEY INSIGHTS ========== */
// 1. Most tree problems solved with recursion
// 2. Think of each node as root of subtree
// 3. Bottom-up for using child info
// 4. Top-down for using parent info
// 5. BST inorder = sorted sequence
// 6. Level order = BFS with queue
// 7. Path problems often need backtracking
// 8. Global variables useful for optimization problems

/* ========== COMPLEXITY REFERENCE ========== */
// Standard traversals: O(n) time, O(h) space
// Level order: O(n) time, O(w) space (w = max width)
// Balanced tree height: O(log n)
// Worst case tree height: O(n)

/* ========== COMMON PITFALLS ========== */
// 1. Forgetting null checks
// 2. Not handling single node trees
// 3. Integer overflow in BST validation
// 4. Modifying tree during traversal incorrectly
// 5. Not considering both subtrees in recursive solutions

/* ========== INTERVIEW APPROACH ========== */
// 1. Clarify if BST or general binary tree
// 2. Ask about duplicate values
// 3. Consider both recursive and iterative
// 4. Draw examples to visualize
// 5. Think about edge cases (null, single node, skewed)
```

### 📝 **Day 7 Final Checklist**
- [ ] Review all traversal methods
- [ ] Complete self-assessment quiz
- [ ] Solve at least 15 tree problems total
- [ ] Create personal notes/patterns
- [ ] Ready for Week 6: Graphs

---

## 🎯 **End of Week 5 Milestones**

### You Should Now Be Able To:
✅ Implement all tree traversals (recursive/iterative)  
✅ Solve path-related problems efficiently  
✅ Work with BST properties  
✅ Calculate tree properties (height, diameter, etc.)  
✅ Construct trees from traversals  
✅ Apply appropriate recursion patterns  

### Problems Completed (Minimum):
- ✅ Maximum Depth of Binary Tree
- ✅ Invert Binary Tree
- ✅ Same Tree
- ✅ Binary Tree Level Order Traversal
- ✅ Validate Binary Search Tree
- ✅ Kth Smallest Element in BST
- ✅ Path Sum I & II
- ✅ Lowest Common Ancestor

### Core Patterns Mastered:
1. **DFS Traversals** - In/Pre/Post order
2. **BFS/Level Order** - Queue-based traversal
3. **Recursion Patterns** - Top-down vs Bottom-up
4. **Path Problems** - Backtracking and sum tracking
5. **BST Operations** - Search, insert, delete, validate

### Skills Developed:
- 🎯 Recursive thinking and base cases
- 🎯 Tree property calculations
- 🎯 Path tracking and backtracking
- 🎯 BST-specific optimizations
- 🎯 Tree construction and serialization

### Prepare for Week 6:
- Graphs extend tree concepts
- Multiple paths between nodes
- Cycle detection becomes important
- Review BFS/DFS as they're crucial for graphs

## 💪 **Week 5 Reflection Questions**
1. Which traversal method do you find most intuitive?
2. How comfortable are you with recursion now?
3. What's the trickiest tree problem you solved?
4. Can you explain LCA algorithm to someone?
5. How do BSTs optimize certain operations?

## 🎉 **Fantastic Progress!**
Trees are the gateway to understanding graphs and advanced data structures. Your mastery of recursion, tree traversals, and path problems has prepared you for more complex algorithms. The ability to think recursively and break problems into subproblems is a fundamental skill that extends beyond trees. You're now ready to tackle graphs, which build upon everything you've learned about trees but add the complexity of cycles and multiple paths. Keep up the excellent work!
