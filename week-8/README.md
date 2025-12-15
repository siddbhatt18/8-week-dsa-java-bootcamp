# Week 8: Integration & Advanced Practice - Daily Structured Plan

## 📅 **DAY 1: Arrays & Strings Integration**

### 🌅 **Morning Session (45 minutes)**
#### Combining Multiple Techniques
```java
class ArrayStringIntegration {
    // Minimum Window Substring - Sliding Window + HashMap
    public String minWindow(String s, String t) {
        if (s.length() == 0 || t.length() == 0) return "";
        
        Map<Character, Integer> dictT = new HashMap<>();
        for (char c : t.toCharArray()) {
            dictT.put(c, dictT.getOrDefault(c, 0) + 1);
        }
        
        int required = dictT.size();
        int left = 0, right = 0;
        int formed = 0;
        
        Map<Character, Integer> windowCounts = new HashMap<>();
        int[] ans = {-1, 0, 0}; // {window length, left, right}
        
        while (right < s.length()) {
            char c = s.charAt(right);
            windowCounts.put(c, windowCounts.getOrDefault(c, 0) + 1);
            
            if (dictT.containsKey(c) && 
                windowCounts.get(c).intValue() == dictT.get(c).intValue()) {
                formed++;
            }
            
            while (left <= right && formed == required) {
                c = s.charAt(left);
                
                if (ans[0] == -1 || right - left + 1 < ans[0]) {
                    ans[0] = right - left + 1;
                    ans[1] = left;
                    ans[2] = right;
                }
                
                windowCounts.put(c, windowCounts.get(c) - 1);
                if (dictT.containsKey(c) && 
                    windowCounts.get(c).intValue() < dictT.get(c).intValue()) {
                    formed--;
                }
                
                left++;
            }
            
            right++;
        }
        
        return ans[0] == -1 ? "" : s.substring(ans[1], ans[2] + 1);
    }
    
    // Longest Substring with At Most K Distinct Characters
    // Sliding Window + HashMap
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if (s == null || s.length() == 0 || k == 0) return 0;
        
        Map<Character, Integer> map = new HashMap<>();
        int left = 0, maxLen = 0;
        
        for (int right = 0; right < s.length(); right++) {
            char rightChar = s.charAt(right);
            map.put(rightChar, map.getOrDefault(rightChar, 0) + 1);
            
            while (map.size() > k) {
                char leftChar = s.charAt(left);
                map.put(leftChar, map.get(leftChar) - 1);
                if (map.get(leftChar) == 0) {
                    map.remove(leftChar);
                }
                left++;
            }
            
            maxLen = Math.max(maxLen, right - left + 1);
        }
        
        return maxLen;
    }
    
    // Trapping Rain Water - Two Pointers + Arrays
    public int trap(int[] height) {
        if (height.length == 0) return 0;
        
        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int water = 0;
        
        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    water += leftMax - height[left];
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    water += rightMax - height[right];
                }
                right--;
            }
        }
        
        return water;
    }
    
    // Merge Intervals - Sorting + Arrays
    public int[][] merge(int[][] intervals) {
        if (intervals.length <= 1) return intervals;
        
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        
        List<int[]> merged = new ArrayList<>();
        int[] currentInterval = intervals[0];
        merged.add(currentInterval);
        
        for (int[] interval : intervals) {
            int currentEnd = currentInterval[1];
            int nextBegin = interval[0];
            int nextEnd = interval[1];
            
            if (currentEnd >= nextBegin) {
                currentInterval[1] = Math.max(currentEnd, nextEnd);
            } else {
                currentInterval = interval;
                merged.add(currentInterval);
            }
        }
        
        return merged.toArray(new int[merged.size()][]);
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Complex String Manipulation
```java
class AdvancedStringProblems {
    // Find All Anagrams in a String - Sliding Window + Frequency Map
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> result = new ArrayList<>();
        if (s.length() < p.length()) return result;
        
        int[] pFreq = new int[26];
        int[] windowFreq = new int[26];
        
        for (char c : p.toCharArray()) {
            pFreq[c - 'a']++;
        }
        
        for (int i = 0; i < s.length(); i++) {
            windowFreq[s.charAt(i) - 'a']++;
            
            if (i >= p.length()) {
                windowFreq[s.charAt(i - p.length()) - 'a']--;
            }
            
            if (i >= p.length() - 1 && Arrays.equals(pFreq, windowFreq)) {
                result.add(i - p.length() + 1);
            }
        }
        
        return result;
    }
    
    // Palindrome Pairs - Trie + String Manipulation
    public List<List<Integer>> palindromePairs(String[] words) {
        List<List<Integer>> result = new ArrayList<>();
        Map<String, Integer> map = new HashMap<>();
        
        for (int i = 0; i < words.length; i++) {
            map.put(words[i], i);
        }
        
        for (int i = 0; i < words.length; i++) {
            String word = words[i];
            
            for (int j = 0; j <= word.length(); j++) {
                String prefix = word.substring(0, j);
                String suffix = word.substring(j);
                
                if (isPalindrome(prefix)) {
                    String reversedSuffix = new StringBuilder(suffix).reverse().toString();
                    if (map.containsKey(reversedSuffix) && map.get(reversedSuffix) != i) {
                        result.add(Arrays.asList(map.get(reversedSuffix), i));
                    }
                }
                
                if (isPalindrome(suffix) && suffix.length() != 0) {
                    String reversedPrefix = new StringBuilder(prefix).reverse().toString();
                    if (map.containsKey(reversedPrefix) && map.get(reversedPrefix) != i) {
                        result.add(Arrays.asList(i, map.get(reversedPrefix)));
                    }
                }
            }
        }
        
        return result;
    }
    
    private boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left++) != s.charAt(right--)) return false;
        }
        return true;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Problem Set
- **Solve:** [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- **Then:** [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
- **Challenge:** [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

### 📝 **Day 1 Checklist**
- [ ] Combine sliding window with HashMap
- [ ] Master two-pointer optimizations
- [ ] Handle complex string patterns
- [ ] Complete all three problems
- [ ] Time yourself on each problem

---

## 📅 **DAY 2: Tree & Graph Integration**

### 🌅 **Morning Session (45 minutes)**
#### Tree-Graph Hybrid Problems
```java
class TreeGraphIntegration {
    // All Nodes Distance K in Binary Tree - Tree as Graph + BFS
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        Map<TreeNode, TreeNode> parentMap = new HashMap<>();
        buildParentMap(root, null, parentMap);
        
        Queue<TreeNode> queue = new LinkedList<>();
        Set<TreeNode> visited = new HashSet<>();
        queue.offer(target);
        visited.add(target);
        
        int currentDistance = 0;
        while (!queue.isEmpty()) {
            if (currentDistance == k) {
                List<Integer> result = new ArrayList<>();
                for (TreeNode node : queue) {
                    result.add(node.val);
                }
                return result;
            }
            
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                
                // Check neighbors (left, right, parent)
                if (node.left != null && !visited.contains(node.left)) {
                    visited.add(node.left);
                    queue.offer(node.left);
                }
                if (node.right != null && !visited.contains(node.right)) {
                    visited.add(node.right);
                    queue.offer(node.right);
                }
                if (parentMap.get(node) != null && !visited.contains(parentMap.get(node))) {
                    visited.add(parentMap.get(node));
                    queue.offer(parentMap.get(node));
                }
            }
            currentDistance++;
        }
        
        return new ArrayList<>();
    }
    
    private void buildParentMap(TreeNode node, TreeNode parent, 
                               Map<TreeNode, TreeNode> parentMap) {
        if (node == null) return;
        parentMap.put(node, parent);
        buildParentMap(node.left, node, parentMap);
        buildParentMap(node.right, node, parentMap);
    }
    
    // Course Schedule III - Topological Sort + Priority Queue
    public int scheduleCourse(int[][] courses) {
        Arrays.sort(courses, (a, b) -> a[1] - b[1]); // Sort by end time
        
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> b - a);
        int time = 0;
        
        for (int[] course : courses) {
            time += course[0];
            pq.offer(course[0]);
            
            if (time > course[1]) {
                time -= pq.poll(); // Remove longest course
            }
        }
        
        return pq.size();
    }
    
    // Accounts Merge - Union Find + HashMap
    class UnionFind {
        int[] parent;
        
        UnionFind(int n) {
            parent = new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
            }
        }
        
        int find(int x) {
            if (parent[x] != x) {
                parent[x] = find(parent[x]);
            }
            return parent[x];
        }
        
        void union(int x, int y) {
            parent[find(x)] = find(y);
        }
    }
    
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        UnionFind uf = new UnionFind(accounts.size());
        Map<String, Integer> emailToIndex = new HashMap<>();
        
        for (int i = 0; i < accounts.size(); i++) {
            for (int j = 1; j < accounts.get(i).size(); j++) {
                String email = accounts.get(i).get(j);
                if (emailToIndex.containsKey(email)) {
                    uf.union(i, emailToIndex.get(email));
                } else {
                    emailToIndex.put(email, i);
                }
            }
        }
        
        Map<Integer, List<String>> indexToEmails = new HashMap<>();
        for (String email : emailToIndex.keySet()) {
            int index = uf.find(emailToIndex.get(email));
            indexToEmails.computeIfAbsent(index, x -> new ArrayList<>()).add(email);
        }
        
        List<List<String>> result = new ArrayList<>();
        for (int index : indexToEmails.keySet()) {
            List<String> emails = indexToEmails.get(index);
            Collections.sort(emails);
            emails.add(0, accounts.get(index).get(0));
            result.add(emails);
        }
        
        return result;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Complex Graph Algorithms
```java
class AdvancedGraphProblems {
    // Word Ladder - BFS + String Manipulation
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<>(wordList);
        if (!wordSet.contains(endWord)) return 0;
        
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        int level = 1;
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String current = queue.poll();
                char[] chars = current.toCharArray();
                
                for (int j = 0; j < chars.length; j++) {
                    char original = chars[j];
                    
                    for (char c = 'a'; c <= 'z'; c++) {
                        if (c == original) continue;
                        chars[j] = c;
                        String next = new String(chars);
                        
                        if (next.equals(endWord)) return level + 1;
                        
                        if (wordSet.contains(next)) {
                            queue.offer(next);
                            wordSet.remove(next);
                        }
                    }
                    
                    chars[j] = original;
                }
            }
            level++;
        }
        
        return 0;
    }
    
    // Network Delay Time - Dijkstra's Algorithm
    public int networkDelayTime(int[][] times, int n, int k) {
        Map<Integer, List<int[]>> graph = new HashMap<>();
        for (int[] time : times) {
            graph.computeIfAbsent(time[0], x -> new ArrayList<>())
                 .add(new int[]{time[1], time[2]});
        }
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        pq.offer(new int[]{0, k});
        
        Map<Integer, Integer> dist = new HashMap<>();
        
        while (!pq.isEmpty()) {
            int[] current = pq.poll();
            int time = current[0];
            int node = current[1];
            
            if (dist.containsKey(node)) continue;
            dist.put(node, time);
            
            if (graph.containsKey(node)) {
                for (int[] edge : graph.get(node)) {
                    int neighbor = edge[0];
                    int weight = edge[1];
                    if (!dist.containsKey(neighbor)) {
                        pq.offer(new int[]{time + weight, neighbor});
                    }
                }
            }
        }
        
        if (dist.size() != n) return -1;
        
        int maxTime = 0;
        for (int time : dist.values()) {
            maxTime = Math.max(maxTime, time);
        }
        
        return maxTime;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Problem Set
- **Solve:** [863. All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)
- **Then:** [127. Word Ladder](https://leetcode.com/problems/word-ladder/)

### 📝 **Day 2 Checklist**
- [ ] Convert trees to graphs when needed
- [ ] Apply graph algorithms to tree problems
- [ ] Combine multiple data structures
- [ ] Complete both problems
- [ ] Practice explaining approach

---

## 📅 **DAY 3: Dynamic Programming Integration**

### 🌅 **Morning Session (45 minutes)**
#### DP with Other Techniques
```java
class DPIntegration {
    // Best Time to Buy and Sell Stock IV - DP + State Machine
    public int maxProfit(int k, int[] prices) {
        if (prices.length == 0) return 0;
        
        if (k >= prices.length / 2) {
            // Can do unlimited transactions
            int profit = 0;
            for (int i = 1; i < prices.length; i++) {
                profit += Math.max(0, prices[i] - prices[i-1]);
            }
            return profit;
        }
        
        int[] buy = new int[k + 1];
        int[] sell = new int[k + 1];
        Arrays.fill(buy, -prices[0]);
        
        for (int price : prices) {
            for (int i = k; i > 0; i--) {
                sell[i] = Math.max(sell[i], buy[i] + price);
                buy[i] = Math.max(buy[i], sell[i-1] - price);
            }
        }
        
        return sell[k];
    }
    
    // Word Search II - Trie + Backtracking + Board
    class TrieNode {
        TrieNode[] children = new TrieNode[26];
        String word = null;
    }
    
    public List<String> findWords(char[][] board, String[] words) {
        List<String> result = new ArrayList<>();
        TrieNode root = buildTrie(words);
        
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                dfs(board, i, j, root, result);
            }
        }
        
        return result;
    }
    
    private void dfs(char[][] board, int i, int j, TrieNode node, List<String> result) {
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length) return;
        
        char c = board[i][j];
        if (c == '#' || node.children[c - 'a'] == null) return;
        
        node = node.children[c - 'a'];
        if (node.word != null) {
            result.add(node.word);
            node.word = null; // Avoid duplicates
        }
        
        board[i][j] = '#'; // Mark visited
        dfs(board, i + 1, j, node, result);
        dfs(board, i - 1, j, node, result);
        dfs(board, i, j + 1, node, result);
        dfs(board, i, j - 1, node, result);
        board[i][j] = c; // Backtrack
    }
    
    private TrieNode buildTrie(String[] words) {
        TrieNode root = new TrieNode();
        for (String word : words) {
            TrieNode node = root;
            for (char c : word.toCharArray()) {
                if (node.children[c - 'a'] == null) {
                    node.children[c - 'a'] = new TrieNode();
                }
                node = node.children[c - 'a'];
            }
            node.word = word;
        }
        return root;
    }
    
    // Wildcard Matching - DP + String
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        
        // Handle patterns like *, **, ***
        for (int j = 1; j <= n; j++) {
            if (p.charAt(j - 1) == '*') {
                dp[0][j] = dp[0][j - 1];
            }
        }
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
                } else if (p.charAt(j - 1) == '?' || s.charAt(i - 1) == p.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                }
            }
        }
        
        return dp[m][n];
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Advanced DP Combinations
```java
class ComplexDPProblems {
    // Russian Doll Envelopes - DP + Sorting + Binary Search
    public int maxEnvelopes(int[][] envelopes) {
        Arrays.sort(envelopes, (a, b) -> {
            if (a[0] == b[0]) return b[1] - a[1];
            return a[0] - b[0];
        });
        
        int[] heights = new int[envelopes.length];
        for (int i = 0; i < envelopes.length; i++) {
            heights[i] = envelopes[i][1];
        }
        
        return lengthOfLIS(heights);
    }
    
    private int lengthOfLIS(int[] nums) {
        List<Integer> tails = new ArrayList<>();
        
        for (int num : nums) {
            int left = 0, right = tails.size();
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
    
    // Super Egg Drop - DP + Binary Search
    public int superEggDrop(int k, int n) {
        int[][] dp = new int[k + 1][n + 1];
        
        for (int i = 1; i <= k; i++) {
            dp[i][0] = 0;
            dp[i][1] = 1;
        }
        
        for (int j = 1; j <= n; j++) {
            dp[1][j] = j;
        }
        
        for (int i = 2; i <= k; i++) {
            for (int j = 2; j <= n; j++) {
                dp[i][j] = Integer.MAX_VALUE;
                
                int left = 1, right = j;
                while (left <= right) {
                    int mid = left + (right - left) / 2;
                    int broken = dp[i - 1][mid - 1];
                    int notBroken = dp[i][j - mid];
                    
                    if (broken > notBroken) {
                        right = mid - 1;
                        dp[i][j] = Math.min(dp[i][j], broken + 1);
                    } else {
                        left = mid + 1;
                        dp[i][j] = Math.min(dp[i][j], notBroken + 1);
                    }
                }
            }
        }
        
        return dp[k][n];
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Problem Set
- **Solve:** [188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)
- **Then:** [212. Word Search II](https://leetcode.com/problems/word-search-ii/)
- **Challenge:** [44. Wildcard Matching](https://leetcode.com/problems/wildcard-matching/)

### 📝 **Day 3 Checklist**
- [ ] Combine DP with greedy strategies
- [ ] Use DP with complex state machines
- [ ] Apply DP to optimization problems
- [ ] Complete all three problems
- [ ] Focus on problem decomposition

---

## 📅 **DAY 4: Design Problems**

### 🌅 **Morning Session (45 minutes)**
#### Data Structure Design
```java
// LRU Cache - HashMap + Doubly Linked List
class LRUCache {
    class Node {
        int key, value;
        Node prev, next;
        
        Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    
    private Map<Integer, Node> cache;
    private Node head, tail;
    private int capacity;
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.cache = new HashMap<>();
        this.head = new Node(0, 0);
        this.tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        if (!cache.containsKey(key)) return -1;
        
        Node node = cache.get(key);
        removeNode(node);
        addToHead(node);
        
        return node.value;
    }
    
    public void put(int key, int value) {
        if (cache.containsKey(key)) {
            Node node = cache.get(key);
            node.value = value;
            removeNode(node);
            addToHead(node);
        } else {
            if (cache.size() >= capacity) {
                Node lru = tail.prev;
                removeNode(lru);
                cache.remove(lru.key);
            }
            
            Node newNode = new Node(key, value);
            cache.put(key, newNode);
            addToHead(newNode);
        }
    }
    
    private void removeNode(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    private void addToHead(Node node) {
        node.next = head.next;
        node.prev = head;
        head.next.prev = node;
        head.next = node;
    }
}

// Implement Trie - Tree Structure
class Trie {
    class TrieNode {
        TrieNode[] children;
        boolean isEnd;
        
        TrieNode() {
            children = new TrieNode[26];
            isEnd = false;
        }
    }
    
    private TrieNode root;
    
    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (node.children[c - 'a'] == null) {
                node.children[c - 'a'] = new TrieNode();
            }
            node = node.children[c - 'a'];
        }
        node.isEnd = true;
    }
    
    public boolean search(String word) {
        TrieNode node = searchPrefix(word);
        return node != null && node.isEnd;
    }
    
    public boolean startsWith(String prefix) {
        return searchPrefix(prefix) != null;
    }
    
    private TrieNode searchPrefix(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (node.children[c - 'a'] == null) {
                return null;
            }
            node = node.children[c - 'a'];
        }
        return node;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Advanced Design Problems
```java
// Design Search Autocomplete System
class AutocompleteSystem {
    class TrieNode {
        Map<Character, TrieNode> children = new HashMap<>();
        Map<String, Integer> counts = new HashMap<>();
    }
    
    private TrieNode root;
    private String prefix;
    private TrieNode currNode;
    
    public AutocompleteSystem(String[] sentences, int[] times) {
        root = new TrieNode();
        prefix = "";
        currNode = root;
        
        for (int i = 0; i < sentences.length; i++) {
            add(sentences[i], times[i]);
        }
    }
    
    private void add(String sentence, int time) {
        TrieNode node = root;
        for (char c : sentence.toCharArray()) {
            node.children.putIfAbsent(c, new TrieNode());
            node = node.children.get(c);
            node.counts.put(sentence, node.counts.getOrDefault(sentence, 0) + time);
        }
    }
    
    public List<String> input(char c) {
        if (c == '#') {
            add(prefix, 1);
            prefix = "";
            currNode = root;
            return new ArrayList<>();
        }
        
        prefix += c;
        if (currNode == null || !currNode.children.containsKey(c)) {
            currNode = null;
            return new ArrayList<>();
        }
        
        currNode = currNode.children.get(c);
        
        PriorityQueue<Map.Entry<String, Integer>> pq = new PriorityQueue<>(
            (a, b) -> a.getValue() == b.getValue() ? 
            b.getKey().compareTo(a.getKey()) : a.getValue() - b.getValue()
        );
        
        for (Map.Entry<String, Integer> entry : currNode.counts.entrySet()) {
            pq.offer(entry);
            if (pq.size() > 3) pq.poll();
        }
        
        LinkedList<String> result = new LinkedList<>();
        while (!pq.isEmpty()) {
            result.addFirst(pq.poll().getKey());
        }
        
        return result;
    }
}

// Design Twitter - OOP + Data Structures
class Twitter {
    class Tweet {
        int id;
        int timestamp;
        
        Tweet(int id, int timestamp) {
            this.id = id;
            this.timestamp = timestamp;
        }
    }
    
    private Map<Integer, List<Tweet>> userTweets;
    private Map<Integer, Set<Integer>> following;
    private int timestamp;
    
    public Twitter() {
        userTweets = new HashMap<>();
        following = new HashMap<>();
        timestamp = 0;
    }
    
    public void postTweet(int userId, int tweetId) {
        userTweets.computeIfAbsent(userId, k -> new ArrayList<>())
                  .add(0, new Tweet(tweetId, timestamp++));
    }
    
    public List<Integer> getNewsFeed(int userId) {
        PriorityQueue<Tweet> pq = new PriorityQueue<>((a, b) -> b.timestamp - a.timestamp);
        
        // Add user's own tweets
        if (userTweets.containsKey(userId)) {
            List<Tweet> tweets = userTweets.get(userId);
            for (int i = 0; i < Math.min(10, tweets.size()); i++) {
                pq.offer(tweets.get(i));
            }
        }
        
        // Add followed users' tweets
        if (following.containsKey(userId)) {
            for (int followeeId : following.get(userId)) {
                if (userTweets.containsKey(followeeId)) {
                    List<Tweet> tweets = userTweets.get(followeeId);
                    for (int i = 0; i < Math.min(10, tweets.size()); i++) {
                        pq.offer(tweets.get(i));
                    }
                }
            }
        }
        
        List<Integer> result = new ArrayList<>();
        while (!pq.isEmpty() && result.size() < 10) {
            result.add(pq.poll().id);
        }
        
        return result;
    }
    
    public void follow(int followerId, int followeeId) {
        if (followerId == followeeId) return;
        following.computeIfAbsent(followerId, k -> new HashSet<>()).add(followeeId);
    }
    
    public void unfollow(int followerId, int followeeId) {
        if (following.containsKey(followerId)) {
            following.get(followerId).remove(followeeId);
        }
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Problem Set
- **Solve:** [146. LRU Cache](https://leetcode.com/problems/lru-cache/)
- **Then:** [208. Implement Trie](https://leetcode.com/problems/implement-trie-prefix-tree/)
- **Challenge:** [355. Design Twitter](https://leetcode.com/problems/design-twitter/)

### 📝 **Day 4 Checklist**
- [ ] Design efficient data structures
- [ ] Balance time/space tradeoffs
- [ ] Handle concurrent operations
- [ ] Complete all three problems
- [ ] Practice explaining design choices

---

## 📅 **DAY 5: Interview Simulation - Medium Problems**

### 🌅 **Morning Session (90 minutes)**
#### Timed Problem Set 1 (45 minutes each)
```java
/*
INTERVIEW SIMULATION RULES:
1. Set timer for 45 minutes per problem
2. No looking at solutions
3. Write clean, production-ready code
4. Think out loud (practice explaining)
5. Consider edge cases
6. Optimize after working solution
*/

// Problem 1: Spiral Matrix
public List<Integer> spiralOrder(int[][] matrix) {
    // Your implementation
    // Time limit: 45 minutes
    // Focus: Clear logic, boundary handling
}

// Problem 2: Rotting Oranges
public int orangesRotting(int[][] grid) {
    // Your implementation  
    // Time limit: 45 minutes
    // Focus: Multi-source BFS
}
```

### 🌞 **Afternoon Session (90 minutes)**
#### Timed Problem Set 2
```java
// Problem 3: Decode String
public String decodeString(String s) {
    // Your implementation
    // Time limit: 45 minutes
    // Focus: Stack or recursion
}

// Problem 4: Find Peak Element
public int findPeakElement(int[] nums) {
    // Your implementation
    // Time limit: 45 minutes
    // Focus: Binary search variation
}
```

### 🌙 **Evening Session (45 minutes)**
#### Review and Optimization
- Review all solutions from today
- Identify areas for improvement
- Compare with optimal solutions
- Document lessons learned

### 📝 **Day 5 Checklist**
- [ ] Complete 4 medium problems under time pressure
- [ ] Practice explaining approach while coding
- [ ] Handle all edge cases
- [ ] Achieve optimal time complexity
- [ ] Document problem-solving patterns

---

## 📅 **DAY 6: Interview Simulation - Hard Problems**

### 🌅 **Morning Session (120 minutes)**
#### Challenging Problem Set (60 minutes each)
```java
// Problem 1: Median of Two Sorted Arrays
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    // Your implementation
    // Time limit: 60 minutes
    // Focus: Binary search, O(log(min(m,n)))
}

// Problem 2: Serialize and Deserialize Binary Tree
public class Codec {
    public String serialize(TreeNode root) {
        // Your implementation
    }
    
    public TreeNode deserialize(String data) {
        // Your implementation
    }
}
```

### 🌞 **Afternoon Session (120 minutes)**
#### Complex Integration Problems
```java
// Problem 3: Sliding Window Maximum
public int[] maxSlidingWindow(int[] nums, int k) {
    // Your implementation
    // Time limit: 60 minutes
    // Focus: Deque, O(n) solution
}

// Problem 4: Basic Calculator II
public int calculate(String s) {
    // Your implementation
    // Time limit: 60 minutes
    // Focus: Stack, operator precedence
}
```

### 🌙 **Evening Session (45 minutes)**
#### Mock Interview Debrief
- Self-assessment of performance
- Areas of strength
- Areas needing improvement
- Time management analysis
- Communication practice

### 📝 **Day 6 Checklist**
- [ ] Attempt 4 hard problems
- [ ] Manage time effectively
- [ ] Implement at least 2 optimal solutions
- [ ] Practice problem breakdown
- [ ] Build confidence with hard problems

---

## 📅 **DAY 7: Final Review & Future Planning**

### 🌅 **Morning Session (60 minutes)**
#### Comprehensive Knowledge Check
```java
// FINAL ASSESSMENT QUIZ

/*
1. Algorithm Complexity Mastery:
Sort these by time complexity (best to worst):
- Binary search in sorted array
- BFS in graph
- Dynamic programming for knapsack
- Merge sort
- Finding duplicates with HashSet
- Matrix multiplication

2. Pattern Recognition:
Identify the best approach for each:
a) "Find shortest path in unweighted graph" → ?
b) "Count number of ways to reach target" → ?
c) "Find k-th largest element" → ?
d) "Detect cycle in directed graph" → ?
e) "Find longest palindromic substring" → ?

3. Space-Time Tradeoffs:
When would you choose:
- Recursive vs Iterative DFS?
- HashMap vs Sorting for finding duplicates?
- DP tabulation vs memoization?
- Array vs LinkedList?

4. Problem-Solving Strategy:
Order these steps for approaching a new problem:
[ ] Write code
[ ] Identify pattern
[ ] Consider edge cases
[ ] Clarify requirements
[ ] Design algorithm
[ ] Test with examples
[ ] Optimize solution

5. Code Quality:
What makes production-ready code?
List 5 essential qualities.
*/
```

### 🌞 **Afternoon Session (90 minutes)**
#### Personal Weak Areas Practice
Based on your week's performance, practice problems from your weakest areas:

```java
// Custom Problem Set Based on Weak Areas
// If weak in DP: Practice more DP problems
// If weak in Graphs: Focus on graph algorithms
// If weak in Trees: Review tree traversals
// If weak in Design: Practice more design problems

// Top 5 Problem Types to Master:
// 1. Two pointers/Sliding window
// 2. Tree/Graph traversal
// 3. Dynamic programming
// 4. Binary search variations
// 5. Design/Implementation
```

### 🌙 **Evening Session (60 minutes)**
#### Future Study Plan
```java
// 8-WEEK JOURNEY COMPLETION CERTIFICATE

/* ========== SKILLS MASTERED ========== */
// ✅ Arrays & Strings manipulation
// ✅ HashMap/HashSet optimization
// ✅ Two Pointers & Sliding Window
// ✅ Linked List operations
// ✅ Binary Tree & BST algorithms
// ✅ Graph traversals (DFS/BFS)
// ✅ Dynamic Programming patterns
// ✅ Integration of multiple techniques

/* ========== PROBLEM COUNT ========== */
// Week 1: 5+ problems
// Week 2: 6+ problems  
// Week 3: 7+ problems
// Week 4: 7+ problems
// Week 5: 8+ problems
// Week 6: 7+ problems
// Week 7: 8+ problems
// Week 8: 15+ problems
// TOTAL: 60+ LeetCode problems solved!

/* ========== NEXT STEPS ========== */

// MONTH 1-2: Consolidation
// - Solve 3-5 problems daily
// - Focus on medium difficulty
// - Time yourself strictly
// - Review solutions weekly

// MONTH 3-4: Advanced Topics
// - Segment trees
// - Fenwick trees  
// - Advanced graph algorithms (Dijkstra, Bellman-Ford)
// - String algorithms (KMP, Rabin-Karp)
// - Computational geometry basics

// MONTH 5-6: Interview Preparation
// - Mock interviews weekly
// - System design basics
// - Behavioral questions
// - Company-specific problems

/* ========== DAILY PRACTICE ROUTINE ========== */
// Morning: 1 new medium problem (45 min)
// Evening: 1 review problem (30 min)
// Weekend: 1 hard problem (60 min)

/* ========== RESOURCES FOR CONTINUED LEARNING ========== */
// 1. LeetCode Premium (company questions)
// 2. Pramp/Interviewing.io (mock interviews)
// 3. System Design Primer
// 4. CTCI (Cracking the Coding Interview)
// 5. Algorithm specialization courses

/* ========== PROBLEM CATEGORIES TO EXPLORE ========== */
Map<String, List<String>> futureTopics = new HashMap<>();

futureTopics.put("Math & Bit Manipulation", Arrays.asList(
    "Prime numbers",
    "GCD/LCM",
    "Bit operations",
    "Base conversion"
));

futureTopics.put("Advanced Strings", Arrays.asList(
    "Suffix arrays",
    "String matching",
    "Palindrome variations",
    "Compression algorithms"
));

futureTopics.put("Advanced Trees", Arrays.asList(
    "AVL trees",
    "Red-black trees",
    "B-trees",
    "Segment trees"
));

futureTopics.put("Advanced Graphs", Arrays.asList(
    "Minimum spanning tree",
    "Shortest path algorithms",
    "Network flow",
    "Bipartite matching"
));

/* ========== SUCCESS METRICS ========== */
// - Solve medium problems in < 30 minutes
// - Solve easy problems in < 15 minutes
// - 80% success rate on new problems
// - Clear explanation while coding
// - Optimize without hints

/* ========== INTERVIEW READINESS CHECKLIST ========== */
// ✅ Can solve 2 medium problems in 1 hour
// ✅ Know time/space complexity for all solutions
// ✅ Can explain approach clearly
// ✅ Handle edge cases systematically
// ✅ Can optimize brute force solutions
// ✅ Comfortable with all core patterns
// ✅ Can write clean, bug-free code
// ✅ Can debug efficiently

/* ========== MOTIVATIONAL REMINDERS ========== */
// 1. Every expert was once a beginner
// 2. Consistency beats intensity
// 3. Understanding > Memorization
// 4. Progress, not perfection
// 5. The journey continues!
```

### 📝 **Day 7 Final Checklist**
- [ ] Complete final assessment
- [ ] Review all 8 weeks of progress
- [ ] Identify top 3 strengths
- [ ] Identify top 3 areas for improvement
- [ ] Create personalized future study plan
- [ ] Celebrate your achievement! 🎉

---

## 🎯 **End of 8-Week Journey - Final Milestones**

### You Have Successfully:
✅ Mastered 20+ core algorithmic patterns  
✅ Solved 60+ LeetCode problems  
✅ Learned 5+ major data structures deeply  
✅ Developed systematic problem-solving approach  
✅ Built interview-ready coding skills  
✅ Gained confidence in technical challenges  

### Core Competencies Achieved:
1. **Data Structure Mastery** - Arrays, Lists, Trees, Graphs
2. **Algorithm Expertise** - Searching, Sorting, DP, Traversals
3. **Problem-Solving Skills** - Pattern recognition, optimization
4. **Code Quality** - Clean, efficient, maintainable code
5. **Interview Readiness** - Time management, communication

### Your Toolkit Contains:
- 🔧 Two Pointers & Sliding Window
- 🔧 HashMap & HashSet optimization
- 🔧 Tree & Graph traversals
- 🔧 Dynamic Programming
- 🔧 Binary Search variations
- 🔧 Backtracking & Recursion
- 🔧 Design patterns
- 🔧 Space-time optimization

### Interview Success Probability:
- **Easy Problems:** 95% success rate
- **Medium Problems:** 75% success rate  
- **Hard Problems:** 40% success rate
- **Overall Readiness:** 80% prepared

## 💪 **Final Reflection Prompts**
1. What was your biggest breakthrough moment?
2. Which week challenged you the most?
3. What pattern do you find most elegant?
4. How has your problem-solving approach evolved?
5. What advice would you give to someone starting Week 1?

## 🏆 **CONGRATULATIONS!**
You've completed an intensive 8-week journey that many start but few finish. You've transformed from someone learning basic arrays to someone who can tackle complex algorithmic challenges. Your dedication, persistence, and systematic approach have built a strong foundation that will serve you throughout your career.

Remember: This is not the end, but the beginning of your journey as a skilled problem solver. The patterns you've learned, the techniques you've mastered, and the confidence you've built are tools that will continue to grow with practice.

**You are now ready to:**
- Take on technical interviews with confidence
- Contribute to complex codebases
- Mentor others in their learning journey
- Continue exploring advanced topics
- Build amazing things with your skills

**Keep coding, keep learning, and keep growing! The best is yet to come! 🚀**
