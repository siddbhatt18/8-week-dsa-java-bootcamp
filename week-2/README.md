# Week 2: HashMap & HashSet Mastery - Daily Structured Plan

## 📅 **DAY 1: HashMap Fundamentals & Internal Working**

### 🌅 **Morning Session (45 minutes)**
#### Understanding HashMap Internals
- **Core Concepts:**
  - What is hashing and hash functions
  - Collision handling (chaining vs open addressing)
  - Load factor and rehashing
  - Time complexity: average O(1) vs worst case O(n)

#### Conceptual Understanding:
```java
/*
HashMap Internal Structure:
- Array of buckets (linked lists or trees)
- Hash function maps key -> bucket index
- Collision: multiple keys map to same bucket
- Load factor: 0.75 default (resize when 75% full)

Visual:
Buckets: [0] -> null
         [1] -> (key1, val1) -> (key5, val5)  // collision chain
         [2] -> (key2, val2)
         [3] -> null
         [4] -> (key3, val3)
*/

// How HashMap calculates index
int hash = key.hashCode();
int index = hash & (capacity - 1);  // efficient modulo for power of 2
```

### 🌞 **Afternoon Session (45 minutes)**
#### HashMap Basic Operations in Java
- **Essential Methods:**
  - put(key, value)
  - get(key)
  - containsKey(key)
  - containsValue(value)
  - remove(key)
  - size(), isEmpty(), clear()

#### Practice Code:
```java
import java.util.HashMap;
import java.util.Map;

// Creating and basic operations
HashMap<String, Integer> map = new HashMap<>();

// Adding elements
map.put("apple", 5);
map.put("banana", 3);
map.put("orange", 7);

// Accessing elements
Integer appleCount = map.get("apple");  // 5
Integer grapeCount = map.get("grape");  // null

// Checking existence
if (map.containsKey("banana")) {
    System.out.println("Banana exists: " + map.get("banana"));
}

// Safe retrieval with default
int count = map.getOrDefault("grape", 0);  // Returns 0 if not found

// Updating values
map.put("apple", 10);  // Overwrites existing value
map.replace("banana", 5);  // Only replaces if key exists

// Removing elements
Integer removed = map.remove("orange");  // Returns removed value
map.remove("grape");  // Returns null if not found

// Size operations
System.out.println("Size: " + map.size());
System.out.println("Is empty: " + map.isEmpty());
```

### 🌙 **Evening Session (30 minutes)**
#### Iteration Patterns
```java
// Method 1: Iterate over entries
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

// Method 2: Iterate over keys
for (String key : map.keySet()) {
    System.out.println(key + ": " + map.get(key));
}

// Method 3: Iterate over values
for (Integer value : map.values()) {
    System.out.println("Value: " + value);
}

// Method 4: Using forEach (Java 8+)
map.forEach((key, value) -> {
    System.out.println(key + ": " + value);
});

// Method 5: Using iterator
Iterator<Map.Entry<String, Integer>> iterator = map.entrySet().iterator();
while (iterator.hasNext()) {
    Map.Entry<String, Integer> entry = iterator.next();
    if (entry.getValue() < 5) {
        iterator.remove();  // Safe removal during iteration
    }
}
```

### 📝 **Day 1 Checklist**
- [ ] Understand how HashMap works internally
- [ ] Know what causes collisions and how they're handled
- [ ] Master basic HashMap operations
- [ ] Can iterate through HashMap in multiple ways
- [ ] Understand when to use each iteration method

---

## 📅 **DAY 2: Advanced HashMap Techniques**

### 🌅 **Morning Session (45 minutes)**
#### HashMap with Complex Values
- **Common Patterns:**
  - HashMap with List as value
  - HashMap with another HashMap
  - Custom objects as keys (equals & hashCode)

#### Implementation Examples:
```java
// Pattern 1: HashMap with List values (for grouping)
HashMap<String, List<Integer>> groupMap = new HashMap<>();

// Adding to list in map
String key = "even";
groupMap.putIfAbsent(key, new ArrayList<>());
groupMap.get(key).add(2);
groupMap.get(key).add(4);

// Better approach with computeIfAbsent
groupMap.computeIfAbsent("odd", k -> new ArrayList<>()).add(1);
groupMap.computeIfAbsent("odd", k -> new ArrayList<>()).add(3);

// Pattern 2: Nested HashMap (2D map)
HashMap<String, HashMap<String, Integer>> nestedMap = new HashMap<>();
nestedMap.putIfAbsent("user1", new HashMap<>());
nestedMap.get("user1").put("score", 100);

// Pattern 3: Custom class as key
class Point {
    int x, y;
    
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Point point = (Point) obj;
        return x == point.x && y == point.y;
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(x, y);  // or: 31 * x + y
    }
}

HashMap<Point, String> pointMap = new HashMap<>();
pointMap.put(new Point(1, 2), "A");
```

### 🌞 **Afternoon Session (45 minutes)**
#### Frequency Counting Patterns
- **Master these essential patterns:**

```java
// Pattern 1: Character frequency
public HashMap<Character, Integer> charFrequency(String s) {
    HashMap<Character, Integer> freq = new HashMap<>();
    for (char c : s.toCharArray()) {
        freq.put(c, freq.getOrDefault(c, 0) + 1);
        // Alternative: freq.merge(c, 1, Integer::sum);
    }
    return freq;
}

// Pattern 2: Word frequency
public HashMap<String, Integer> wordFrequency(String text) {
    HashMap<String, Integer> freq = new HashMap<>();
    String[] words = text.toLowerCase().split("\\s+");
    for (String word : words) {
        freq.put(word, freq.getOrDefault(word, 0) + 1);
    }
    return freq;
}

// Pattern 3: Finding most frequent element
public int mostFrequent(int[] nums) {
    HashMap<Integer, Integer> freq = new HashMap<>();
    int maxCount = 0;
    int mostFreq = nums[0];
    
    for (int num : nums) {
        int count = freq.getOrDefault(num, 0) + 1;
        freq.put(num, count);
        if (count > maxCount) {
            maxCount = count;
            mostFreq = num;
        }
    }
    return mostFreq;
}

// Pattern 4: First non-repeating character
public char firstNonRepeating(String s) {
    HashMap<Character, Integer> freq = new HashMap<>();
    for (char c : s.toCharArray()) {
        freq.put(c, freq.getOrDefault(c, 0) + 1);
    }
    
    for (char c : s.toCharArray()) {
        if (freq.get(c) == 1) {
            return c;
        }
    }
    return '\0';  // No non-repeating character
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)
  - Approach 1: Sort both strings and compare
  - Approach 2: Use HashMap for character frequency
  - Approach 3: Use array for frequency (if only lowercase letters)

```java
// Solution template
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;
    
    // Approach 2: HashMap
    HashMap<Character, Integer> map = new HashMap<>();
    
    // Count frequency in s
    for (char c : s.toCharArray()) {
        map.put(c, map.getOrDefault(c, 0) + 1);
    }
    
    // Decrement for t
    for (char c : t.toCharArray()) {
        if (!map.containsKey(c) || map.get(c) == 0) {
            return false;
        }
        map.put(c, map.get(c) - 1);
    }
    
    return true;
}
```

### 📝 **Day 2 Checklist**
- [ ] Implement HashMap with List values
- [ ] Understand custom objects as keys (equals/hashCode)
- [ ] Master frequency counting patterns
- [ ] Complete Valid Anagram with multiple approaches
- [ ] Know when to use putIfAbsent vs computeIfAbsent

---

## 📅 **DAY 3: HashSet Deep Dive**

### 🌅 **Morning Session (45 minutes)**
#### HashSet Fundamentals
- **Core Concepts:**
  - HashSet vs HashMap (HashSet uses HashMap internally)
  - No duplicates, no ordering
  - Null values (only one null)
  - When to use Set vs Map

#### Basic Operations:
```java
import java.util.HashSet;
import java.util.Set;

// Creating and basic operations
HashSet<Integer> set = new HashSet<>();

// Adding elements
set.add(5);
set.add(10);
set.add(5);  // Returns false, not added
System.out.println(set.size());  // 2

// Checking existence - O(1)
boolean exists = set.contains(10);  // true

// Removing elements
boolean removed = set.remove(5);  // Returns true if removed
set.remove(100);  // Returns false

// Bulk operations
HashSet<Integer> set2 = new HashSet<>();
set2.add(10);
set2.add(20);
set2.add(30);

// Union
HashSet<Integer> union = new HashSet<>(set);
union.addAll(set2);  // {10, 20, 30}

// Intersection  
HashSet<Integer> intersection = new HashSet<>(set);
intersection.retainAll(set2);  // {10}

// Difference
HashSet<Integer> difference = new HashSet<>(set);
difference.removeAll(set2);  // {}

// Convert array to set (remove duplicates)
int[] arr = {1, 2, 2, 3, 3, 3};
HashSet<Integer> uniqueSet = new HashSet<>();
for (int num : arr) {
    uniqueSet.add(num);
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Set Patterns for Problem Solving
```java
// Pattern 1: Finding duplicates
public boolean containsDuplicate(int[] nums) {
    HashSet<Integer> set = new HashSet<>();
    for (int num : nums) {
        if (!set.add(num)) {  // add returns false if already exists
            return true;
        }
    }
    return false;
}

// Pattern 2: Finding intersection of arrays
public int[] intersection(int[] nums1, int[] nums2) {
    HashSet<Integer> set1 = new HashSet<>();
    for (int num : nums1) {
        set1.add(num);
    }
    
    HashSet<Integer> resultSet = new HashSet<>();
    for (int num : nums2) {
        if (set1.contains(num)) {
            resultSet.add(num);
        }
    }
    
    // Convert set to array
    int[] result = new int[resultSet.size()];
    int i = 0;
    for (int num : resultSet) {
        result[i++] = num;
    }
    return result;
}

// Pattern 3: Tracking seen elements
public int findFirstRepeating(int[] nums) {
    HashSet<Integer> seen = new HashSet<>();
    for (int num : nums) {
        if (seen.contains(num)) {
            return num;
        }
        seen.add(num);
    }
    return -1;  // No repeating element
}

// Pattern 4: Finding missing elements
public List<Integer> findMissingNumbers(int[] nums, int n) {
    HashSet<Integer> set = new HashSet<>();
    for (int num : nums) {
        set.add(num);
    }
    
    List<Integer> missing = new ArrayList<>();
    for (int i = 1; i <= n; i++) {
        if (!set.contains(i)) {
            missing.add(i);
        }
    }
    return missing;
}
```

### 🌙 **Evening Session (30 minutes)**
#### HashSet vs HashMap Decision Making
```java
/*
Use HashSet when:
- Only need to check existence
- Need unique elements
- Don't need to store associated values
- Set operations (union, intersection)

Use HashMap when:
- Need key-value pairs
- Need to count frequency
- Need to store additional information
- Need to map relationships
*/

// Example: Two Sum problem comparison
// HashMap approach - can store index
public int[] twoSumHashMap(int[] nums, int target) {
    HashMap<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}

// HashSet approach - only for checking existence
public boolean twoSumExists(int[] nums, int target) {
    HashSet<Integer> set = new HashSet<>();
    for (int num : nums) {
        if (set.contains(target - num)) {
            return true;
        }
        set.add(num);
    }
    return false;
}
```

### 📝 **Day 3 Checklist**
- [ ] Understand HashSet internal implementation
- [ ] Master set operations (union, intersection, difference)
- [ ] Implement duplicate/missing element patterns
- [ ] Know when to choose HashSet vs HashMap
- [ ] Practice set-to-array conversions

---

## 📅 **DAY 4: Sliding Window with HashMap**

### 🌅 **Morning Session (45 minutes)**
#### Sliding Window Fundamentals
- **Concept Review:**
  - Fixed vs variable size windows
  - When to expand/contract window
  - HashMap for tracking window state

#### Basic Sliding Window Template:
```java
// Fixed size window template
public void fixedWindow(int[] nums, int k) {
    HashMap<Integer, Integer> window = new HashMap<>();
    
    // Initialize first window
    for (int i = 0; i < k; i++) {
        window.put(nums[i], window.getOrDefault(nums[i], 0) + 1);
    }
    
    // Slide the window
    for (int i = k; i < nums.length; i++) {
        // Add new element
        window.put(nums[i], window.getOrDefault(nums[i], 0) + 1);
        
        // Remove oldest element
        int oldElement = nums[i - k];
        window.put(oldElement, window.get(oldElement) - 1);
        if (window.get(oldElement) == 0) {
            window.remove(oldElement);
        }
        
        // Process current window
    }
}

// Variable size window template
public void variableWindow(String s) {
    HashMap<Character, Integer> window = new HashMap<>();
    int left = 0;
    
    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        window.put(c, window.getOrDefault(c, 0) + 1);
        
        // Shrink window if condition violated
        while (/* window condition violated */) {
            char leftChar = s.charAt(left);
            window.put(leftChar, window.get(leftChar) - 1);
            if (window.get(leftChar) == 0) {
                window.remove(leftChar);
            }
            left++;
        }
        
        // Update result
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Sliding Window with Character Frequency
```java
// Pattern 1: Longest substring with at most K distinct characters
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    if (s == null || s.length() == 0 || k == 0) return 0;
    
    HashMap<Character, Integer> window = new HashMap<>();
    int left = 0, maxLen = 0;
    
    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        window.put(c, window.getOrDefault(c, 0) + 1);
        
        while (window.size() > k) {
            char leftChar = s.charAt(left);
            window.put(leftChar, window.get(leftChar) - 1);
            if (window.get(leftChar) == 0) {
                window.remove(leftChar);
            }
            left++;
        }
        
        maxLen = Math.max(maxLen, right - left + 1);
    }
    
    return maxLen;
}

// Pattern 2: Find all anagrams in string
public List<Integer> findAnagrams(String s, String p) {
    List<Integer> result = new ArrayList<>();
    if (s.length() < p.length()) return result;
    
    HashMap<Character, Integer> pMap = new HashMap<>();
    HashMap<Character, Integer> window = new HashMap<>();
    
    // Build pattern frequency map
    for (char c : p.toCharArray()) {
        pMap.put(c, pMap.getOrDefault(c, 0) + 1);
    }
    
    // Sliding window
    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        window.put(c, window.getOrDefault(c, 0) + 1);
        
        // Remove element outside window
        if (i >= p.length()) {
            char leftChar = s.charAt(i - p.length());
            if (window.get(leftChar) == 1) {
                window.remove(leftChar);
            } else {
                window.put(leftChar, window.get(leftChar) - 1);
            }
        }
        
        // Check if window matches pattern
        if (window.equals(pMap)) {
            result.add(i - p.length() + 1);
        }
    }
    
    return result;
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
```java
public int lengthOfLongestSubstring(String s) {
    HashSet<Character> window = new HashSet<>();
    int maxLength = 0;
    int left = 0;
    
    for (int right = 0; right < s.length(); right++) {
        // Shrink window until no duplicate
        while (window.contains(s.charAt(right))) {
            window.remove(s.charAt(left));
            left++;
        }
        
        window.add(s.charAt(right));
        maxLength = Math.max(maxLength, right - left + 1);
    }
    
    return maxLength;
}
```

### 📝 **Day 4 Checklist**
- [ ] Understand fixed vs variable sliding window
- [ ] Implement window expansion/contraction logic
- [ ] Master HashMap for window state tracking
- [ ] Complete Longest Substring Without Repeating Characters
- [ ] Know when sliding window is applicable

---

## 📅 **DAY 5: HashMap Optimization Techniques**

### 🌅 **Morning Session (45 minutes)**
#### Space-Time Tradeoffs
- **Optimization Patterns:**
  - Caching/Memoization with HashMap
  - Pre-computation for multiple queries
  - Trading space for time complexity

```java
// Pattern 1: Two Sum optimization comparison
// Approach 1: Nested loops - Time: O(n²), Space: O(1)
public int[] twoSumBrute(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) {
                return new int[]{i, j};
            }
        }
    }
    return new int[]{};
}

// Approach 2: One-pass HashMap - Time: O(n), Space: O(n)
public int[] twoSumOptimal(int[] nums, int target) {
    HashMap<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}

// Pattern 2: Subarray sum equals K with prefix sum
public int subarraySum(int[] nums, int k) {
    HashMap<Integer, Integer> prefixSumCount = new HashMap<>();
    prefixSumCount.put(0, 1);  // Empty subarray
    
    int currentSum = 0;
    int count = 0;
    
    for (int num : nums) {
        currentSum += num;
        
        // Check if (currentSum - k) exists
        if (prefixSumCount.containsKey(currentSum - k)) {
            count += prefixSumCount.get(currentSum - k);
        }
        
        prefixSumCount.put(currentSum, 
            prefixSumCount.getOrDefault(currentSum, 0) + 1);
    }
    
    return count;
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Advanced HashMap Patterns
```java
// Pattern 1: Group elements by property
public List<List<String>> groupAnagrams(String[] strs) {
    HashMap<String, List<String>> map = new HashMap<>();
    
    for (String str : strs) {
        // Create key by sorting characters
        char[] chars = str.toCharArray();
        Arrays.sort(chars);
        String key = String.valueOf(chars);
        
        // Alternative: Use character frequency as key
        // String key = getFrequencyString(str);
        
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(str);
    }
    
    return new ArrayList<>(map.values());
}

// Alternative key generation using frequency
private String getFrequencyString(String str) {
    int[] freq = new int[26];
    for (char c : str.toCharArray()) {
        freq[c - 'a']++;
    }
    
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < 26; i++) {
        if (freq[i] > 0) {
            sb.append((char)('a' + i)).append(freq[i]);
        }
    }
    return sb.toString();
}

// Pattern 2: LRU Cache concept (simplified)
class SimpleLRU {
    private int capacity;
    private LinkedHashMap<Integer, Integer> cache;
    
    public SimpleLRU(int capacity) {
        this.capacity = capacity;
        // true = access order, false = insertion order
        this.cache = new LinkedHashMap<>(capacity, 0.75f, true) {
            protected boolean removeEldestEntry(Map.Entry eldest) {
                return size() > capacity;
            }
        };
    }
    
    public int get(int key) {
        return cache.getOrDefault(key, -1);
    }
    
    public void put(int key, int value) {
        cache.put(key, value);
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)
- **Then:** [1. Two Sum](https://leetcode.com/problems/two-sum/) - Optimize to one-pass solution

### 📝 **Day 5 Checklist**
- [ ] Understand space-time tradeoffs with HashMap
- [ ] Master prefix sum pattern with HashMap
- [ ] Implement grouping pattern (Group Anagrams)
- [ ] Know LinkedHashMap for ordered operations
- [ ] Complete both LeetCode problems optimally

---

## 📅 **DAY 6: Practice & Pattern Recognition Day**

### 🌅 **Morning Session (45 minutes)**
#### Review Core Patterns
- **Quick revision of all patterns learned:**

```java
// HASHMAP PATTERNS SUMMARY

// 1. Frequency Counting
HashMap<Character, Integer> freq = new HashMap<>();
for (char c : str.toCharArray()) {
    freq.put(c, freq.getOrDefault(c, 0) + 1);
}

// 2. Two Sum Pattern (complement search)
HashMap<Integer, Integer> map = new HashMap<>();
for (int i = 0; i < nums.length; i++) {
    int complement = target - nums[i];
    if (map.containsKey(complement)) {
        // Found pair
    }
    map.put(nums[i], i);
}

// 3. Grouping Pattern
HashMap<String, List<String>> groups = new HashMap<>();
for (String item : items) {
    String key = generateKey(item);
    groups.computeIfAbsent(key, k -> new ArrayList<>()).add(item);
}

// 4. Sliding Window with HashMap
HashMap<Character, Integer> window = new HashMap<>();
int left = 0;
for (int right = 0; right < s.length(); right++) {
    // Add to window
    // Check/shrink window
    // Update result
}

// 5. Prefix Sum Pattern
HashMap<Integer, Integer> prefixSum = new HashMap<>();
prefixSum.put(0, 1);
int sum = 0;
for (int num : nums) {
    sum += num;
    // Check sum - target
    prefixSum.put(sum, prefixSum.getOrDefault(sum, 0) + 1);
}
```

### 🌞 **Afternoon Session (60 minutes)**
#### Problem-Solving Session
**Solve these problems independently:**

1. **Find First Non-Repeating Character**
```java
public char firstUniqChar(String s) {
    // Your implementation
    // Hint: Two-pass solution with frequency map
}
```

2. **Check if Array Contains Duplicate within K Distance**
```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    // Your implementation
    // Hint: HashMap stores index, check distance
}
```

3. **Find Common Elements in Three Arrays**
```java
public List<Integer> commonElements(int[] arr1, int[] arr2, int[] arr3) {
    // Your implementation
    // Hint: Use frequency map or multiple sets
}
```

### 🌙 **Evening Session (45 minutes)**
#### LeetCode Challenge Problems
- **Solve:** 
  1. [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
  2. [387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)

```java
// Longest Consecutive Sequence approach
public int longestConsecutive(int[] nums) {
    HashSet<Integer> set = new HashSet<>();
    for (int num : nums) {
        set.add(num);
    }
    
    int maxLength = 0;
    
    for (int num : set) {
        // Only start counting from sequence beginning
        if (!set.contains(num - 1)) {
            int currentNum = num;
            int currentLength = 1;
            
            while (set.contains(currentNum + 1)) {
                currentNum++;
                currentLength++;
            }
            
            maxLength = Math.max(maxLength, currentLength);
        }
    }
    
    return maxLength;
}
```

### 📝 **Day 6 Checklist**
- [ ] Review all 5 core HashMap patterns
- [ ] Solve 3 practice problems independently
- [ ] Complete Longest Consecutive Sequence
- [ ] Complete First Unique Character
- [ ] Document problem-solving approaches

---

## 📅 **DAY 7: Week Review & Advanced Applications**

### 🌅 **Morning Session (60 minutes)**
#### Comprehensive Knowledge Check

**Quiz Yourself:**
```java
// 1. What's the time complexity of HashMap operations?
// put: O(?) average, O(?) worst
// get: O(?) average, O(?) worst
// remove: O(?) average, O(?) worst

// 2. When does HashMap resize?
// Load factor = ?
// When to resize = ?

// 3. Fix this code:
HashMap<List<Integer>, String> map = new HashMap<>();
List<Integer> key = Arrays.asList(1, 2, 3);
map.put(key, "value");
key.add(4);  // Problem?
String value = map.get(key);  // What happens?

// 4. Memory usage:
// HashMap with n entries uses approximately O(?) space
// HashSet with n entries uses approximately O(?) space

// 5. Which is more efficient for checking duplicates?
boolean hasDuplicate1(int[] nums) {
    Arrays.sort(nums);  // O(n log n)
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] == nums[i-1]) return true;
    }
    return false;
}

boolean hasDuplicate2(int[] nums) {
    HashSet<Integer> set = new HashSet<>();  // O(n) space
    for (int num : nums) {  // O(n) time
        if (!set.add(num)) return true;
    }
    return false;
}
```

### 🌞 **Afternoon Session (90 minutes)**
#### Complete Weekly Challenge Set

**Must Complete:**
1. All previous incomplete problems
2. Bonus challenge problems

**Advanced Problems to Attempt:**
```java
// 1. Implement a simple spell checker
public List<String> spellCheck(String[] words, String[] dictionary) {
    HashSet<String> dict = new HashSet<>(Arrays.asList(dictionary));
    List<String> misspelled = new ArrayList<>();
    
    for (String word : words) {
        if (!dict.contains(word.toLowerCase())) {
            misspelled.add(word);
        }
    }
    return misspelled;
}

// 2. Find all pairs with given sum
public List<int[]> findPairsWithSum(int[] nums, int target) {
    HashMap<Integer, List<Integer>> map = new HashMap<>();
    List<int[]> pairs = new ArrayList<>();
    
    // Store all indices for each value
    for (int i = 0; i < nums.length; i++) {
        map.computeIfAbsent(nums[i], k -> new ArrayList<>()).add(i);
    }
    
    // Find pairs
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            for (int j : map.get(complement)) {
                if (i < j) {  // Avoid duplicates
                    pairs.add(new int[]{i, j});
                }
            }
        }
    }
    return pairs;
}

// 3. Design a data structure for O(1) insert, delete, getRandom
class RandomizedSet {
    private HashMap<Integer, Integer> map;  // value -> index
    private List<Integer> list;  // actual values
    private Random random;
    
    public RandomizedSet() {
        map = new HashMap<>();
        list = new ArrayList<>();
        random = new Random();
    }
    
    public boolean insert(int val) {
        if (map.containsKey(val)) return false;
        
        list.add(val);
        map.put(val, list.size() - 1);
        return true;
    }
    
    public boolean remove(int val) {
        if (!map.containsKey(val)) return false;
        
        int index = map.get(val);
        int lastElement = list.get(list.size() - 1);
        
        // Move last element to index position
        list.set(index, lastElement);
        map.put(lastElement, index);
        
        // Remove last element
        list.remove(list.size() - 1);
        map.remove(val);
        return true;
    }
    
    public int getRandom() {
        return list.get(random.nextInt(list.size()));
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Week 2 Reflection & Documentation

**Create Your HashMap/HashSet Cheat Sheet:**
```java
// WEEK 2 MASTER REFERENCE

// ========== HASHMAP ESSENTIALS ==========
// Declaration
HashMap<K, V> map = new HashMap<>();

// Core Operations - O(1) average
map.put(key, value);           // Add/update
V val = map.get(key);          // Retrieve (null if absent)
V val = map.getOrDefault(key, defaultValue);
boolean exists = map.containsKey(key);
V removed = map.remove(key);

// Advanced Operations
map.putIfAbsent(key, value);   // Only if not present
map.computeIfAbsent(key, k -> new ArrayList<>());
map.merge(key, value, (old, new) -> old + new);

// Iteration
for (Map.Entry<K, V> entry : map.entrySet()) { }
for (K key : map.keySet()) { }
for (V value : map.values()) { }

// ========== HASHSET ESSENTIALS ==========
HashSet<E> set = new HashSet<>();

// Core Operations - O(1) average
boolean added = set.add(element);     // false if exists
boolean exists = set.contains(element);
boolean removed = set.remove(element);

// Set Operations
set1.addAll(set2);     // Union
set1.retainAll(set2);  // Intersection
set1.removeAll(set2);  // Difference

// ========== KEY PATTERNS ==========
// 1. Frequency: map.put(key, map.getOrDefault(key, 0) + 1)
// 2. Grouping: map.computeIfAbsent(key, k -> new ArrayList<>()).add(value)
// 3. Two Sum: Check complement in map
// 4. Sliding Window: Track window state with map
// 5. Prefix Sum: Store cumulative sums in map

// ========== GOTCHAS ==========
// - Mutable keys break HashMap (use immutable)
// - Default load factor: 0.75
// - Initial capacity: 16
// - Resize at: capacity * load factor
// - null key allowed in HashMap (only one)
// - LinkedHashMap maintains insertion order
// - TreeMap maintains sorted order (O(log n) operations)
```

### 📝 **Day 7 Final Checklist**
- [ ] Score at least 4/5 on knowledge quiz
- [ ] Complete all Week 2 LeetCode problems
- [ ] Implement RandomizedSet or similar design problem
- [ ] Create comprehensive cheat sheet
- [ ] Document top 5 learnings from Week 2
- [ ] Ready for Week 3: Two Pointers & Sliding Window

---

## 🎯 **End of Week 2 Milestones**

### You Should Now Be Able To:
✅ Choose between HashMap and HashSet appropriately  
✅ Implement frequency counting efficiently  
✅ Use HashMap for optimization (space-time tradeoffs)  
✅ Apply sliding window with HashMap  
✅ Group elements using HashMap patterns  
✅ Solve Two Sum variants optimally  

### Problems Completed (Minimum):
- ✅ Valid Anagram (multiple approaches)
- ✅ Two Sum (one-pass HashMap)
- ✅ Group Anagrams
- ✅ Longest Consecutive Sequence
- ✅ Longest Substring Without Repeating Characters
- ✅ First Unique Character

### Patterns Mastered:
1. **Frequency Counting** - Character/element frequencies
2. **Complement Search** - Two Sum pattern
3. **Grouping** - Anagrams, categories
4. **Sliding Window** - With HashMap state
5. **Set Operations** - Unique elements, intersections

### Prepare for Week 3:
- Two Pointers will build on array manipulation
- Sliding Window will extend HashMap knowledge
- Review array basics if needed
- Rest and consolidate learning!

## 💪 **Week 2 Reflection Questions**
1. What was the most challenging concept this week?
2. Which pattern do you find most useful?
3. How has HashMap changed your problem-solving approach?
4. What would you review again before interviews?
5. Which problem gave you the biggest "aha" moment?

## 🎉 **Congratulations!**
You've mastered one of the most important data structures in programming! HashMap/HashSet appear in 30-40% of interview problems. Your ability to recognize when and how to use them will dramatically improve your problem-solving speed. Week 3 will combine these skills with Two Pointers and Sliding Window for even more powerful solutions!
