# Week 7: Dynamic Programming Introduction - Daily Structured Plan

## 📅 **DAY 1: DP Fundamentals & Memoization**

### 🌅 **Morning Session (45 minutes)**
#### Understanding Dynamic Programming
- **Core Concepts:**
  - What is Dynamic Programming?
  - When to use DP (overlapping subproblems + optimal substructure)
  - Top-down (Memoization) vs Bottom-up (Tabulation)
  - Identifying DP problems

#### Foundation: Recursion to DP
```java
class DPFundamentals {
    // Classic example: Fibonacci
    
    // 1. Pure Recursion - O(2^n) time, O(n) space
    public int fibRecursive(int n) {
        if (n <= 1) return n;
        return fibRecursive(n - 1) + fibRecursive(n - 2);
    }
    
    // 2. Memoization (Top-down) - O(n) time, O(n) space
    public int fibMemoization(int n) {
        Integer[] memo = new Integer[n + 1];
        return fibMemo(n, memo);
    }
    
    private int fibMemo(int n, Integer[] memo) {
        if (n <= 1) return n;
        
        // Check if already computed
        if (memo[n] != null) {
            return memo[n];
        }
        
        // Compute and store
        memo[n] = fibMemo(n - 1, memo) + fibMemo(n - 2, memo);
        return memo[n];
    }
    
    // 3. Tabulation (Bottom-up) - O(n) time, O(n) space
    public int fibTabulation(int n) {
        if (n <= 1) return n;
        
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
    
    // 4. Space Optimized - O(n) time, O(1) space
    public int fibOptimized(int n) {
        if (n <= 1) return n;
        
        int prev2 = 0;
        int prev1 = 1;
        
        for (int i = 2; i <= n; i++) {
            int current = prev1 + prev2;
            prev2 = prev1;
            prev1 = current;
        }
        
        return prev1;
    }
    
    // Visualization of recursive calls
    public void visualizeFibonacci(int n) {
        System.out.println("Computing Fibonacci(" + n + ")");
        System.out.println("Recursive calls without memoization:");
        fibWithPrint(n, 0);
    }
    
    private int fibWithPrint(int n, int depth) {
        String indent = "  ".repeat(depth);
        System.out.println(indent + "fib(" + n + ")");
        
        if (n <= 1) {
            System.out.println(indent + "└─ return " + n);
            return n;
        }
        
        int result = fibWithPrint(n - 1, depth + 1) + fibWithPrint(n - 2, depth + 1);
        System.out.println(indent + "└─ return " + result);
        return result;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Basic DP Patterns
```java
class BasicDPPatterns {
    // Climbing Stairs - Classic DP problem
    public int climbStairs(int n) {
        // Recurrence: dp[i] = dp[i-1] + dp[i-2]
        // Can reach step i from step i-1 (1 step) or i-2 (2 steps)
        
        if (n <= 2) return n;
        
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
    
    // Climbing Stairs with Memoization
    public int climbStairsMemo(int n) {
        Integer[] memo = new Integer[n + 1];
        return climbHelper(n, memo);
    }
    
    private int climbHelper(int n, Integer[] memo) {
        if (n <= 2) return n;
        
        if (memo[n] != null) return memo[n];
        
        memo[n] = climbHelper(n - 1, memo) + climbHelper(n - 2, memo);
        return memo[n];
    }
    
    // Climbing Stairs - Space Optimized
    public int climbStairsOptimized(int n) {
        if (n <= 2) return n;
        
        int oneStep = 2;
        int twoStep = 1;
        int current = 0;
        
        for (int i = 3; i <= n; i++) {
            current = oneStep + twoStep;
            twoStep = oneStep;
            oneStep = current;
        }
        
        return current;
    }
    
    // N-th Tribonacci Number
    public int tribonacci(int n) {
        if (n == 0) return 0;
        if (n <= 2) return 1;
        
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 1;
        
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2] + dp[i - 3];
        }
        
        return dp[n];
    }
    
    // Understanding State and Transitions
    public void explainDP(int n) {
        System.out.println("Dynamic Programming Explanation for Climbing Stairs");
        System.out.println("=================================================");
        System.out.println("Problem: Reach step " + n + " by taking 1 or 2 steps");
        System.out.println("\nState: dp[i] = number of ways to reach step i");
        System.out.println("Base cases: dp[1] = 1, dp[2] = 2");
        System.out.println("Transition: dp[i] = dp[i-1] + dp[i-2]");
        System.out.println("\nBuilding solution:");
        
        if (n <= 0) return;
        
        int[] dp = new int[n + 1];
        dp[1] = 1;
        if (n >= 2) dp[2] = 2;
        
        for (int i = 1; i <= Math.min(n, 2); i++) {
            System.out.printf("dp[%d] = %d\n", i, dp[i]);
        }
        
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
            System.out.printf("dp[%d] = dp[%d] + dp[%d] = %d + %d = %d\n", 
                            i, i-1, i-2, dp[i-1], dp[i-2], dp[i]);
        }
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Identifying DP Problems
```java
class IdentifyingDP {
    /*
    How to identify DP problems:
    
    1. Can be broken into overlapping subproblems
    2. Has optimal substructure (optimal solution from optimal subproblems)
    3. Keywords: "number of ways", "minimum/maximum", "longest/shortest"
    4. Making choices at each step
    5. Can't use greedy (local optimal != global optimal)
    
    Common DP patterns:
    1. Linear DP (1D array)
    2. Grid DP (2D array)
    3. Interval DP
    4. Tree DP
    5. State machine DP
    */
    
    // Example: Is this a DP problem?
    public boolean canReachEnd(int[] nums) {
        // Problem: Can you reach the last index?
        // Each element shows max jump length from that position
        
        // This can be solved with DP:
        // State: dp[i] = can reach end from index i?
        // Transition: dp[i] = true if any dp[i+1...i+nums[i]] is true
        
        int n = nums.length;
        boolean[] dp = new boolean[n];
        dp[n - 1] = true; // Already at end
        
        for (int i = n - 2; i >= 0; i--) {
            for (int j = 1; j <= nums[i] && i + j < n; j++) {
                if (dp[i + j]) {
                    dp[i] = true;
                    break;
                }
            }
        }
        
        return dp[0];
    }
}
```

### 📝 **Day 1 Checklist**
- [ ] Understand overlapping subproblems concept
- [ ] Learn memoization technique
- [ ] Master tabulation approach
- [ ] Complete Fibonacci with all approaches
- [ ] Solve Climbing Stairs problem

---

## 📅 **DAY 2: 1D Dynamic Programming**

### 🌅 **Morning Session (45 minutes)**
#### Linear DP Problems
```java
class LinearDP {
    // House Robber - Classic DP
    public int rob(int[] nums) {
        /*
        State: dp[i] = max money from houses 0 to i
        Choice: rob house i or not
        Transition: dp[i] = max(dp[i-1], dp[i-2] + nums[i])
        */
        
        if (nums.length == 0) return 0;
        if (nums.length == 1) return nums[0];
        
        int n = nums.length;
        int[] dp = new int[n];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        
        for (int i = 2; i < n; i++) {
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
        }
        
        return dp[n - 1];
    }
    
    // House Robber - Space Optimized
    public int robOptimized(int[] nums) {
        int prevMax = 0;
        int currMax = 0;
        
        for (int num : nums) {
            int temp = currMax;
            currMax = Math.max(currMax, prevMax + num);
            prevMax = temp;
        }
        
        return currMax;
    }
    
    // House Robber II (Circular)
    public int robCircular(int[] nums) {
        if (nums.length == 0) return 0;
        if (nums.length == 1) return nums[0];
        
        // Can't rob both first and last house
        // So max of: rob houses 0 to n-2, or houses 1 to n-1
        return Math.max(
            robRange(nums, 0, nums.length - 2),
            robRange(nums, 1, nums.length - 1)
        );
    }
    
    private int robRange(int[] nums, int start, int end) {
        int prevMax = 0;
        int currMax = 0;
        
        for (int i = start; i <= end; i++) {
            int temp = currMax;
            currMax = Math.max(currMax, prevMax + nums[i]);
            prevMax = temp;
        }
        
        return currMax;
    }
    
    // Delete and Earn
    public int deleteAndEarn(int[] nums) {
        /*
        Transform to House Robber problem:
        If we take number x, we get x * frequency(x) points
        But can't take x-1 or x+1
        */
        
        if (nums.length == 0) return 0;
        
        int maxNum = 0;
        for (int num : nums) {
            maxNum = Math.max(maxNum, num);
        }
        
        int[] points = new int[maxNum + 1];
        for (int num : nums) {
            points[num] += num;
        }
        
        // Now it's house robber problem on points array
        return rob(points);
    }
    
    // Maximum Subarray (Kadane's Algorithm)
    public int maxSubArray(int[] nums) {
        /*
        State: dp[i] = max sum ending at index i
        Transition: dp[i] = max(nums[i], dp[i-1] + nums[i])
        */
        
        int maxSoFar = nums[0];
        int maxEndingHere = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        
        return maxSoFar;
    }
    
    // Maximum Product Subarray
    public int maxProduct(int[] nums) {
        /*
        Need to track both max and min products
        because negative * negative = positive
        */
        
        int maxProduct = nums[0];
        int maxSoFar = nums[0];
        int minSoFar = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            int temp = maxSoFar;
            maxSoFar = Math.max(nums[i], 
                       Math.max(maxSoFar * nums[i], minSoFar * nums[i]));
            minSoFar = Math.min(nums[i], 
                       Math.min(temp * nums[i], minSoFar * nums[i]));
            
            maxProduct = Math.max(maxProduct, maxSoFar);
        }
        
        return maxProduct;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Min/Max Cost Problems
```java
class MinMaxCostDP {
    // Min Cost Climbing Stairs
    public int minCostClimbingStairs(int[] cost) {
        /*
        State: dp[i] = min cost to reach step i
        Transition: dp[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2])
        */
        
        int n = cost.length;
        int[] dp = new int[n + 1];
        
        for (int i = 2; i <= n; i++) {
            dp[i] = Math.min(
                dp[i - 1] + cost[i - 1],
                dp[i - 2] + cost[i - 2]
            );
        }
        
        return dp[n];
    }
    
    // Paint House
    public int minCost(int[][] costs) {
        if (costs.length == 0) return 0;
        
        int n = costs.length;
        int[][] dp = new int[n][3];
        
        // Base case
        dp[0][0] = costs[0][0]; // Red
        dp[0][1] = costs[0][1]; // Blue
        dp[0][2] = costs[0][2]; // Green
        
        for (int i = 1; i < n; i++) {
            dp[i][0] = costs[i][0] + Math.min(dp[i-1][1], dp[i-1][2]);
            dp[i][1] = costs[i][1] + Math.min(dp[i-1][0], dp[i-1][2]);
            dp[i][2] = costs[i][2] + Math.min(dp[i-1][0], dp[i-1][1]);
        }
        
        return Math.min(dp[n-1][0], Math.min(dp[n-1][1], dp[n-1][2]));
    }
    
    // Paint House - Space Optimized
    public int minCostOptimized(int[][] costs) {
        if (costs.length == 0) return 0;
        
        int prevRed = costs[0][0];
        int prevBlue = costs[0][1];
        int prevGreen = costs[0][2];
        
        for (int i = 1; i < costs.length; i++) {
            int currRed = costs[i][0] + Math.min(prevBlue, prevGreen);
            int currBlue = costs[i][1] + Math.min(prevRed, prevGreen);
            int currGreen = costs[i][2] + Math.min(prevRed, prevBlue);
            
            prevRed = currRed;
            prevBlue = currBlue;
            prevGreen = currGreen;
        }
        
        return Math.min(prevRed, Math.min(prevBlue, prevGreen));
    }
    
    // Jump Game II - Minimum jumps to reach end
    public int jump(int[] nums) {
        /*
        State: dp[i] = min jumps to reach index i
        Transition: dp[i] = min(dp[j] + 1) for all j that can reach i
        */
        
        int n = nums.length;
        int[] dp = new int[n];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        
        for (int i = 0; i < n - 1; i++) {
            if (dp[i] == Integer.MAX_VALUE) continue;
            
            for (int j = 1; j <= nums[i] && i + j < n; j++) {
                dp[i + j] = Math.min(dp[i + j], dp[i] + 1);
            }
        }
        
        return dp[n - 1];
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
- **Then:** [198. House Robber](https://leetcode.com/problems/house-robber/)
- **Bonus:** [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)

### 📝 **Day 2 Checklist**
- [ ] Master House Robber pattern
- [ ] Understand state transitions
- [ ] Implement space optimization
- [ ] Complete all three LeetCode problems
- [ ] Identify include/exclude patterns

---

## 📅 **DAY 3: Subsequence Problems**

### 🌅 **Morning Session (45 minutes)**
#### Longest Increasing Subsequence (LIS)
```java
class SubsequenceDP {
    // Longest Increasing Subsequence - O(n²) DP
    public int lengthOfLIS(int[] nums) {
        /*
        State: dp[i] = length of LIS ending at index i
        Transition: dp[i] = max(dp[j] + 1) for all j < i where nums[j] < nums[i]
        */
        
        if (nums.length == 0) return 0;
        
        int n = nums.length;
        int[] dp = new int[n];
        Arrays.fill(dp, 1); // Each element is a subsequence of length 1
        
        int maxLength = 1;
        
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLength = Math.max(maxLength, dp[i]);
        }
        
        return maxLength;
    }
    
    // LIS with Binary Search - O(n log n)
    public int lengthOfLISOptimized(int[] nums) {
        List<Integer> tails = new ArrayList<>();
        
        for (int num : nums) {
            int left = 0, right = tails.size();
            
            // Binary search for insertion position
            while (left < right) {
                int mid = left + (right - left) / 2;
                if (tails.get(mid) < num) {
                    left = mid + 1;
                } else {
                    right = mid;
                }
            }
            
            if (left == tails.size()) {
                tails.add(num);
            } else {
                tails.set(left, num);
            }
        }
        
        return tails.size();
    }
    
    // Print actual LIS
    public List<Integer> findLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        int[] prev = new int[n];
        Arrays.fill(dp, 1);
        Arrays.fill(prev, -1);
        
        int maxLength = 1;
        int maxIndex = 0;
        
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i] && dp[j] + 1 > dp[i]) {
                    dp[i] = dp[j] + 1;
                    prev[i] = j;
                }
            }
            
            if (dp[i] > maxLength) {
                maxLength = dp[i];
                maxIndex = i;
            }
        }
        
        // Reconstruct LIS
        List<Integer> lis = new ArrayList<>();
        int curr = maxIndex;
        while (curr != -1) {
            lis.add(0, nums[curr]);
            curr = prev[curr];
        }
        
        return lis;
    }
    
    // Longest Common Subsequence
    public int longestCommonSubsequence(String text1, String text2) {
        /*
        State: dp[i][j] = LCS of text1[0...i-1] and text2[0...j-1]
        Transition: 
        - If text1[i-1] == text2[j-1]: dp[i][j] = dp[i-1][j-1] + 1
        - Else: dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        */
        
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m + 1][n + 1];
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        
        return dp[m][n];
    }
    
    // Longest Palindromic Subsequence
    public int longestPalindromeSubseq(String s) {
        // LPS is LCS of string with its reverse
        String reversed = new StringBuilder(s).reverse().toString();
        return longestCommonSubsequence(s, reversed);
    }
    
    // Alternative approach for LPS
    public int longestPalindromeSubseqDirect(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];
        
        // Single characters are palindromes
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }
        
        // Build table for substrings of length 2 to n
        for (int len = 2; len <= n; len++) {
            for (int i = 0; i <= n - len; i++) {
                int j = i + len - 1;
                
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }
        
        return dp[0][n - 1];
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Number of Subsequences
```java
class CountSubsequences {
    // Distinct Subsequences
    public int numDistinct(String s, String t) {
        /*
        State: dp[i][j] = number of distinct subsequences of s[0...i-1] 
                         that equals t[0...j-1]
        Transition:
        - If s[i-1] == t[j-1]: dp[i][j] = dp[i-1][j-1] + dp[i-1][j]
        - Else: dp[i][j] = dp[i-1][j]
        */
        
        int m = s.length();
        int n = t.length();
        int[][] dp = new int[m + 1][n + 1];
        
        // Empty string is subsequence of any string
        for (int i = 0; i <= m; i++) {
            dp[i][0] = 1;
        }
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                dp[i][j] = dp[i - 1][j]; // Don't use s[i-1]
                
                if (s.charAt(i - 1) == t.charAt(j - 1)) {
                    dp[i][j] += dp[i - 1][j - 1]; // Use s[i-1]
                }
            }
        }
        
        return dp[m][n];
    }
    
    // Arithmetic Slices
    public int numberOfArithmeticSlices(int[] nums) {
        /*
        State: dp[i] = number of arithmetic slices ending at index i
        */
        
        if (nums.length < 3) return 0;
        
        int dp = 0;
        int sum = 0;
        
        for (int i = 2; i < nums.length; i++) {
            if (nums[i] - nums[i - 1] == nums[i - 1] - nums[i - 2]) {
                dp = dp + 1;
                sum += dp;
            } else {
                dp = 0;
            }
        }
        
        return sum;
    }
    
    // Count palindromic subsequences
    public int countPalindromicSubsequences(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];
        
        // Single characters
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }
        
        for (int len = 2; len <= n; len++) {
            for (int i = 0; i <= n - len; i++) {
                int j = i + len - 1;
                
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j] + dp[i][j - 1] + 1;
                } else {
                    dp[i][j] = dp[i + 1][j] + dp[i][j - 1] - dp[i + 1][j - 1];
                }
            }
        }
        
        return dp[0][n - 1];
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
- **Then:** [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

### 📝 **Day 3 Checklist**
- [ ] Master LIS pattern (O(n²) approach)
- [ ] Understand LCS algorithm
- [ ] Learn subsequence counting
- [ ] Complete both LeetCode problems
- [ ] Identify when to use 2D DP

---

## 📅 **DAY 4: Knapsack Problems**

### 🌅 **Morning Session (45 minutes)**
#### 0/1 Knapsack Pattern
```java
class KnapsackDP {
    // Classic 0/1 Knapsack
    public int knapsack01(int[] weights, int[] values, int capacity) {
        /*
        State: dp[i][w] = max value using first i items with weight limit w
        Transition:
        - Include item i: dp[i][w] = dp[i-1][w-weight[i]] + value[i]
        - Exclude item i: dp[i][w] = dp[i-1][w]
        */
        
        int n = weights.length;
        int[][] dp = new int[n + 1][capacity + 1];
        
        for (int i = 1; i <= n; i++) {
            for (int w = 0; w <= capacity; w++) {
                // Exclude current item
                dp[i][w] = dp[i - 1][w];
                
                // Include current item if possible
                if (weights[i - 1] <= w) {
                    dp[i][w] = Math.max(dp[i][w], 
                        dp[i - 1][w - weights[i - 1]] + values[i - 1]);
                }
            }
        }
        
        return dp[n][capacity];
    }
    
    // Space Optimized 0/1 Knapsack
    public int knapsack01Optimized(int[] weights, int[] values, int capacity) {
        int[] dp = new int[capacity + 1];
        
        for (int i = 0; i < weights.length; i++) {
            // Traverse from right to left to avoid using updated values
            for (int w = capacity; w >= weights[i]; w--) {
                dp[w] = Math.max(dp[w], dp[w - weights[i]] + values[i]);
            }
        }
        
        return dp[capacity];
    }
    
    // Partition Equal Subset Sum
    public boolean canPartition(int[] nums) {
        /*
        Can we partition array into two subsets with equal sum?
        This is 0/1 knapsack with target = totalSum/2
        */
        
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }
        
        // If total sum is odd, can't partition equally
        if (totalSum % 2 != 0) return false;
        
        int target = totalSum / 2;
        boolean[] dp = new boolean[target + 1];
        dp[0] = true; // Empty subset has sum 0
        
        for (int num : nums) {
            // Traverse from right to left
            for (int j = target; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }
        
        return dp[target];
    }
    
    // Target Sum (Add +/- signs)
    public int findTargetSumWays(int[] nums, int target) {
        /*
        Let P = sum of positive numbers, N = sum of negative numbers
        P - N = target
        P + N = totalSum
        => P = (target + totalSum) / 2
        
        Problem becomes: count subsets with sum = P
        */
        
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }
        
        // Check if valid
        if ((target + totalSum) % 2 != 0 || Math.abs(target) > totalSum) {
            return 0;
        }
        
        int P = (target + totalSum) / 2;
        return countSubsetsWithSum(nums, P);
    }
    
    private int countSubsetsWithSum(int[] nums, int sum) {
        int[] dp = new int[sum + 1];
        dp[0] = 1; // One way to make sum 0 (empty subset)
        
        for (int num : nums) {
            for (int j = sum; j >= num; j--) {
                dp[j] += dp[j - num];
            }
        }
        
        return dp[sum];
    }
    
    // Last Stone Weight II
    public int lastStoneWeightII(int[] stones) {
        /*
        Partition stones into two groups to minimize difference
        Similar to partition equal subset sum
        */
        
        int totalSum = 0;
        for (int stone : stones) {
            totalSum += stone;
        }
        
        int target = totalSum / 2;
        boolean[] dp = new boolean[target + 1];
        dp[0] = true;
        
        for (int stone : stones) {
            for (int j = target; j >= stone; j--) {
                dp[j] = dp[j] || dp[j - stone];
            }
        }
        
        // Find largest sum <= target
        for (int i = target; i >= 0; i--) {
            if (dp[i]) {
                return totalSum - 2 * i;
            }
        }
        
        return 0;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Unbounded Knapsack Pattern
```java
class UnboundedKnapsack {
    // Unbounded Knapsack (can use items multiple times)
    public int unboundedKnapsack(int[] weights, int[] values, int capacity) {
        int[] dp = new int[capacity + 1];
        
        for (int w = 1; w <= capacity; w++) {
            for (int i = 0; i < weights.length; i++) {
                if (weights[i] <= w) {
                    dp[w] = Math.max(dp[w], dp[w - weights[i]] + values[i]);
                }
            }
        }
        
        return dp[capacity];
    }
    
    // Coin Change - Minimum coins
    public int coinChange(int[] coins, int amount) {
        /*
        State: dp[i] = minimum coins needed for amount i
        Transition: dp[i] = min(dp[i - coin] + 1) for all coins
        */
        
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1); // Initialize with impossible value
        dp[0] = 0;
        
        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (coin <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        
        return dp[amount] > amount ? -1 : dp[amount];
    }
    
    // Coin Change 2 - Number of ways
    public int change(int amount, int[] coins) {
        /*
        State: dp[i] = number of ways to make amount i
        */
        
        int[] dp = new int[amount + 1];
        dp[0] = 1; // One way to make 0 (use no coins)
        
        // For each coin
        for (int coin : coins) {
            // Update all amounts that can use this coin
            for (int i = coin; i <= amount; i++) {
                dp[i] += dp[i - coin];
            }
        }
        
        return dp[amount];
    }
    
    // Perfect Squares
    public int numSquares(int n) {
        /*
        Unbounded knapsack with perfect squares as "coins"
        */
        
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j * j <= i; j++) {
                dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
            }
        }
        
        return dp[n];
    }
    
    // Integer Break
    public int integerBreak(int n) {
        /*
        State: dp[i] = maximum product for integer i
        */
        
        int[] dp = new int[n + 1];
        dp[1] = 1;
        
        for (int i = 2; i <= n; i++) {
            for (int j = 1; j < i; j++) {
                // Either use j as is, or break j further
                dp[i] = Math.max(dp[i], Math.max(j, dp[j]) * (i - j));
            }
        }
        
        return dp[n];
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [322. Coin Change](https://leetcode.com/problems/coin-change/)
- **Then:** [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

### 📝 **Day 4 Checklist**
- [ ] Understand 0/1 vs Unbounded Knapsack
- [ ] Master include/exclude decision pattern
- [ ] Learn space optimization technique
- [ ] Complete both LeetCode problems
- [ ] Recognize knapsack variations

---

## 📅 **DAY 5: String DP Problems**

### 🌅 **Morning Session (45 minutes)**
#### Edit Distance and String Matching
```java
class StringDP {
    // Edit Distance (Levenshtein Distance)
    public int minDistance(String word1, String word2) {
        /*
        State: dp[i][j] = min operations to convert word1[0...i-1] to word2[0...j-1]
        Operations: Insert, Delete, Replace
        */
        
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m + 1][n + 1];
        
        // Base cases
        for (int i = 0; i <= m; i++) {
            dp[i][0] = i; // Delete all characters
        }
        for (int j = 0; j <= n; j++) {
            dp[0][j] = j; // Insert all characters
        }
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1]; // No operation needed
                } else {
                    dp[i][j] = 1 + Math.min(
                        dp[i - 1][j],     // Delete
                        Math.min(
                            dp[i][j - 1],     // Insert
                            dp[i - 1][j - 1]  // Replace
                        )
                    );
                }
            }
        }
        
        return dp[m][n];
    }
    
    // Longest Palindromic Substring
    public String longestPalindrome(String s) {
        /*
        State: dp[i][j] = true if s[i...j] is palindrome
        */
        
        int n = s.length();
        boolean[][] dp = new boolean[n][n];
        int maxLen = 0;
        int start = 0;
        
        // Single characters
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
            maxLen = 1;
            start = i;
        }
        
        // Two characters
        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                maxLen = 2;
                start = i;
            }
        }
        
        // Substrings of length 3 to n
        for (int len = 3; len <= n; len++) {
            for (int i = 0; i <= n - len; i++) {
                int j = i + len - 1;
                
                if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                    dp[i][j] = true;
                    if (len > maxLen) {
                        maxLen = len;
                        start = i;
                    }
                }
            }
        }
        
        return s.substring(start, start + maxLen);
    }
    
    // Word Break
    public boolean wordBreak(String s, List<String> wordDict) {
        /*
        State: dp[i] = true if s[0...i-1] can be segmented
        */
        
        Set<String> wordSet = new HashSet<>(wordDict);
        int n = s.length();
        boolean[] dp = new boolean[n + 1];
        dp[0] = true; // Empty string
        
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordSet.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        
        return dp[n];
    }
    
    // Word Break II - Return all possible sentences
    public List<String> wordBreakII(String s, List<String> wordDict) {
        Map<String, List<String>> memo = new HashMap<>();
        return wordBreakHelper(s, new HashSet<>(wordDict), memo);
    }
    
    private List<String> wordBreakHelper(String s, Set<String> wordSet, 
                                        Map<String, List<String>> memo) {
        if (memo.containsKey(s)) {
            return memo.get(s);
        }
        
        List<String> result = new ArrayList<>();
        
        if (s.length() == 0) {
            result.add("");
            return result;
        }
        
        for (int i = 1; i <= s.length(); i++) {
            String prefix = s.substring(0, i);
            
            if (wordSet.contains(prefix)) {
                List<String> suffixWays = wordBreakHelper(s.substring(i), wordSet, memo);
                
                for (String suffix : suffixWays) {
                    String sentence = prefix + (suffix.isEmpty() ? "" : " " + suffix);
                    result.add(sentence);
                }
            }
        }
        
        memo.put(s, result);
        return result;
    }
    
    // Regular Expression Matching
    public boolean isMatch(String s, String p) {
        /*
        State: dp[i][j] = true if s[0...i-1] matches p[0...j-1]
        */
        
        int m = s.length();
        int n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        
        // Handle patterns like a* or a*b*
        for (int j = 2; j <= n; j++) {
            if (p.charAt(j - 1) == '*') {
                dp[0][j] = dp[0][j - 2];
            }
        }
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                char sc = s.charAt(i - 1);
                char pc = p.charAt(j - 1);
                
                if (pc == '.' || sc == pc) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (pc == '*') {
                    // Check pattern without x* (0 occurrences)
                    dp[i][j] = dp[i][j - 2];
                    
                    // Check if previous pattern char matches
                    char prevPc = p.charAt(j - 2);
                    if (prevPc == '.' || prevPc == sc) {
                        dp[i][j] = dp[i][j] || dp[i - 1][j];
                    }
                }
            }
        }
        
        return dp[m][n];
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Palindrome DP Problems
```java
class PalindromeDP {
    // Palindrome Partitioning II - Minimum cuts
    public int minCut(String s) {
        int n = s.length();
        boolean[][] isPalindrome = new boolean[n][n];
        int[] dp = new int[n];
        
        // Build palindrome table
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i; j < n; j++) {
                if (s.charAt(i) == s.charAt(j) && 
                    (j - i <= 2 || isPalindrome[i + 1][j - 1])) {
                    isPalindrome[i][j] = true;
                }
            }
        }
        
        // Calculate minimum cuts
        for (int i = 0; i < n; i++) {
            if (isPalindrome[0][i]) {
                dp[i] = 0;
            } else {
                dp[i] = i; // Maximum cuts
                for (int j = 1; j <= i; j++) {
                    if (isPalindrome[j][i]) {
                        dp[i] = Math.min(dp[i], dp[j - 1] + 1);
                    }
                }
            }
        }
        
        return dp[n - 1];
    }
    
    // Count Palindromic Substrings
    public int countSubstrings(String s) {
        int n = s.length();
        boolean[][] dp = new boolean[n][n];
        int count = 0;
        
        // Single characters
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
            count++;
        }
        
        // Two characters
        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                count++;
            }
        }
        
        // Length 3 and more
        for (int len = 3; len <= n; len++) {
            for (int i = 0; i <= n - len; i++) {
                int j = i + len - 1;
                if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                    dp[i][j] = true;
                    count++;
                }
            }
        }
        
        return count;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [139. Word Break](https://leetcode.com/problems/word-break/)
- **Then:** [72. Edit Distance](https://leetcode.com/problems/edit-distance/)
- **Challenge:** [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

### 📝 **Day 5 Checklist**
- [ ] Master Edit Distance algorithm
- [ ] Understand Word Break pattern
- [ ] Learn palindrome DP approach
- [ ] Complete all three LeetCode problems
- [ ] Recognize string DP patterns

---

## 📅 **DAY 6: Practice & Pattern Recognition**

### 🌅 **Morning Session (60 minutes)**
#### DP Pattern Summary
```java
class DPPatterns {
    /*
    COMMON DP PATTERNS:
    
    1. Linear DP (1D):
       - State: dp[i] = solution for first i elements
       - Examples: Climbing Stairs, House Robber, LIS
    
    2. Grid DP (2D):
       - State: dp[i][j] = solution for grid[0...i][0...j]
       - Examples: Unique Paths, Min Path Sum
    
    3. Interval DP:
       - State: dp[i][j] = solution for interval [i, j]
       - Examples: Longest Palindromic Substring, Burst Balloons
    
    4. Knapsack:
       - State: dp[i][w] = solution using first i items with capacity w
       - Examples: 0/1 Knapsack, Subset Sum, Coin Change
    
    5. String Matching:
       - State: dp[i][j] = solution for s1[0...i] and s2[0...j]
       - Examples: Edit Distance, LCS, Regular Expression
    
    6. Decision Making:
       - At each step, make optimal choice
       - Examples: Buy/Sell Stock, Jump Game
    
    7. State Machine:
       - Multiple states with transitions
       - Examples: Buy/Sell with Cooldown, Paint House
    */
    
    // Problem Classification Exercise
    public void classifyProblem(String problemDescription) {
        System.out.println("Problem: " + problemDescription);
        System.out.println("Ask yourself:");
        System.out.println("1. Can I break this into smaller subproblems?");
        System.out.println("2. Do subproblems overlap?");
        System.out.println("3. What is the state?");
        System.out.println("4. What is the transition?");
        System.out.println("5. What are the base cases?");
        System.out.println("6. Can I optimize space?");
    }
}
```

### 🌞 **Afternoon Session (90 minutes)**
#### Problem-Solving Marathon
```java
// Solve these problems independently:

// 1. Unique Paths
public int uniquePaths(int m, int n) {
    // Your implementation
    // Grid DP: How many ways to reach bottom-right?
}

// 2. Maximum Profit (Buy/Sell Stock)
public int maxProfit(int[] prices) {
    // Your implementation
    // Track min price and max profit
}

// 3. Decode Ways
public int numDecodings(String s) {
    // Your implementation
    // Similar to climbing stairs with conditions
}

// 4. Triangle Minimum Path Sum
public int minimumTotal(List<List<Integer>> triangle) {
    // Your implementation
    // Bottom-up or top-down DP
}
```

### 🌙 **Evening Session (45 minutes)**
#### LeetCode Challenge Problems
- **Complete these:**
  1. [62. Unique Paths](https://leetcode.com/problems/unique-paths/)
  2. [91. Decode Ways](https://leetcode.com/problems/decode-ways/)
  3. [120. Triangle](https://leetcode.com/problems/triangle/)
  4. [279. Perfect Squares](https://leetcode.com/problems/perfect-squares/)

### 📝 **Day 6 Checklist**
- [ ] Review all DP patterns learned
- [ ] Complete practice problems
- [ ] Identify pattern for each problem
- [ ] Optimize space where possible
- [ ] Document problem-solving approach

---

## 📅 **DAY 7: Week Review & Advanced Topics**

### 🌅 **Morning Session (60 minutes)**
#### Comprehensive Assessment
```java
// DP MASTERY QUIZ

/*
1. Time & Space Complexity:
- Fibonacci with memoization: Time O(?), Space O(?)
- 0/1 Knapsack: Time O(?), Space O(?)
- Edit Distance: Time O(?), Space O(?)
- LIS with binary search: Time O(?), Space O(?)

2. Identify the pattern:
Problem: "Find minimum cost to reach top of stairs"
Pattern: ?

Problem: "Count number of ways to make change"
Pattern: ?

Problem: "Find longest substring without repeating characters"
Pattern: ? (Is this even DP?)

3. Debug this code:
*/
public int rob(int[] nums) {
    int[] dp = new int[nums.length];
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);  // Bug?
    
    for (int i = 2; i < nums.length; i++) {
        dp[i] = Math.max(dp[i-1], dp[i-2] + nums[i]);
    }
    return dp[nums.length - 1];
}

/*
4. Optimize space:
Given this 2D DP solution, can you optimize to 1D?
*/
public int minPathSum(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] dp = new int[m][n];
    dp[0][0] = grid[0][0];
    
    for (int i = 1; i < m; i++) dp[i][0] = dp[i-1][0] + grid[i][0];
    for (int j = 1; j < n; j++) dp[0][j] = dp[0][j-1] + grid[0][j];
    
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + grid[i][j];
        }
    }
    return dp[m-1][n-1];
}

/*
5. When NOT to use DP:
List 3 signs that a problem shouldn't be solved with DP
*/
```

### 🌞 **Afternoon Session (90 minutes)**
#### Advanced DP Preview
```java
class AdvancedDPConcepts {
    // Burst Balloons (Interval DP)
    public int maxCoins(int[] nums) {
        int n = nums.length;
        int[] balloons = new int[n + 2];
        balloons[0] = balloons[n + 1] = 1;
        
        for (int i = 0; i < n; i++) {
            balloons[i + 1] = nums[i];
        }
        
        int[][] dp = new int[n + 2][n + 2];
        
        for (int len = 1; len <= n; len++) {
            for (int left = 1; left <= n - len + 1; left++) {
                int right = left + len - 1;
                
                for (int k = left; k <= right; k++) {
                    int coins = balloons[left - 1] * balloons[k] * balloons[right + 1];
                    coins += dp[left][k - 1] + dp[k + 1][right];
                    dp[left][right] = Math.max(dp[left][right], coins);
                }
            }
        }
        
        return dp[1][n];
    }
    
    // Buy/Sell Stock with Cooldown (State Machine DP)
    public int maxProfitCooldown(int[] prices) {
        if (prices.length <= 1) return 0;
        
        int hold = -prices[0];
        int sold = 0;
        int rest = 0;
        
        for (int i = 1; i < prices.length; i++) {
            int prevHold = hold;
            int prevSold = sold;
            int prevRest = rest;
            
            hold = Math.max(prevHold, prevRest - prices[i]);
            sold = prevHold + prices[i];
            rest = Math.max(prevRest, prevSold);
        }
        
        return Math.max(sold, rest);
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Week 7 Complete Reference
```java
// WEEK 7 DP MASTERY REFERENCE

/* ========== DP RECIPE ========== */
// 1. Define state (what parameters uniquely identify subproblem)
// 2. Define transition (how to compute state from smaller states)
// 3. Define base cases
// 4. Determine computation order
// 5. Optimize space if possible

/* ========== STATE DEFINITION ========== */
// Linear: dp[i] = solution for array[0...i]
// 2D: dp[i][j] = solution for str1[0...i], str2[0...j]
// Interval: dp[i][j] = solution for range [i, j]
// Knapsack: dp[i][w] = solution with items[0...i] and capacity w

/* ========== COMMON TRANSITIONS ========== */
// Max/Min: dp[i] = max/min(dp[i-1], dp[i-2] + nums[i])
// Count: dp[i] = dp[i-1] + dp[i-2]
// Boolean: dp[i] = dp[i-1] || dp[i-2]
// 2D: dp[i][j] = f(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])

/* ========== SPACE OPTIMIZATION ========== */
// 2D to 1D: When only need previous row
// 1D to O(1): When only need few previous values
// Rolling array: Use array[i % 2] for alternating rows

/* ========== TIME COMPLEXITY ========== */
// 1D DP: Usually O(n) or O(n²)
// 2D DP: Usually O(m*n)
// Interval DP: Usually O(n³)
// State * Transition cost

/* ========== TOP-DOWN VS BOTTOM-UP ========== */
// Top-down (Memoization):
//   - Natural recursive thinking
//   - Only solves needed subproblems
//   - Stack overflow risk
//
// Bottom-up (Tabulation):
//   - Iterative, no stack overflow
//   - Solves all subproblems
//   - Often easier to optimize space

/* ========== COMMON MISTAKES ========== */
// 1. Wrong state definition
// 2. Missing base cases
// 3. Incorrect transition
// 4. Array index out of bounds
// 5. Integer overflow
// 6. Not initializing DP array properly

/* ========== INTERVIEW APPROACH ========== */
// 1. Start with brute force recursion
// 2. Identify overlapping subproblems
// 3. Add memoization
// 4. Convert to bottom-up if needed
// 5. Optimize space
// 6. Explain complexity
```

### 📝 **Day 7 Final Checklist**
- [ ] Complete assessment quiz
- [ ] Solve at least 15 DP problems total
- [ ] Master state definition
- [ ] Understand space optimization
- [ ] Ready for Week 8: Integration

---

## 🎯 **End of Week 7 Milestones**

### You Should Now Be Able To:
✅ Identify when to use Dynamic Programming  
✅ Define state and transitions correctly  
✅ Implement both memoization and tabulation  
✅ Optimize space complexity  
✅ Solve classic DP problems  
✅ Recognize common DP patterns  

### Problems Completed (Minimum):
- ✅ Climbing Stairs
- ✅ House Robber
- ✅ Longest Increasing Subsequence
- ✅ Coin Change
- ✅ Partition Equal Subset Sum
- ✅ Edit Distance
- ✅ Word Break
- ✅ Unique Paths

### Core Patterns Mastered:
1. **Linear DP** - Single array problems
2. **Knapsack** - Include/exclude decisions
3. **Subsequence** - LIS, LCS patterns
4. **String DP** - Edit distance, matching
5. **Grid DP** - Path problems

### Skills Developed:
- 🎯 Breaking problems into subproblems
- 🎯 Identifying overlapping subproblems
- 🎯 State and transition formulation
- 🎯 Space-time optimization
- 🎯 Pattern recognition

### Prepare for Week 8:
- Integration of all concepts
- Mixed problem types
- Interview-style questions
- Time-constrained practice

## 💪 **Week 7 Reflection Questions**
1. What makes DP different from divide & conquer?
2. Which pattern was most challenging?
3. How do you decide between top-down vs bottom-up?
4. Can you explain memoization to someone?
5. What's your approach to formulating state?

## 🎉 **Incredible Achievement!**
Dynamic Programming is often considered the most challenging topic in coding interviews, and you've conquered it! Your ability to break complex problems into manageable subproblems, recognize patterns, and optimize solutions demonstrates advanced algorithmic thinking. The mental model you've developed for DP will serve you throughout your programming career. Week 8 will integrate everything you've learned, preparing you for real interview scenarios. You're almost at the finish line - keep pushing!
