# Week 3: Two Pointers & Sliding Window - Daily Structured Plan

## 📅 **DAY 1: Two Pointers Foundation**

### 🌅 **Morning Session (45 minutes)**
#### Understanding Two Pointers Concept
- **Core Patterns:**
  1. Opposite Direction (converging pointers)
  2. Same Direction (fast-slow pointers)
  3. Multiple Arrays (merge pattern)
  
#### Visual Understanding:
```java
/*
Pattern 1: Opposite Direction
Array: [1, 2, 3, 4, 5]
       ↑           ↑
      left       right
      → ←  (moving toward center)

Pattern 2: Same Direction  
Array: [1, 2, 3, 4, 5]
       ↑  ↑
      slow fast
      →   →  (both moving right)

Pattern 3: Multiple Arrays
arr1: [1, 3, 5] ↑
arr2: [2, 4, 6] ↑
result: [1, 2, 3, 4, 5, 6]
*/
```

#### Foundation Code:
```java
// Pattern 1: Opposite Direction - Palindrome Check
public boolean isPalindrome(String s) {
    int left = 0;
    int right = s.length() - 1;
    
    while (left < right) {
        // Skip non-alphanumeric characters
        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
            left++;
        }
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
            right--;
        }
        
        // Compare characters (case-insensitive)
        if (Character.toLowerCase(s.charAt(left)) != 
            Character.toLowerCase(s.charAt(right))) {
            return false;
        }
        
        left++;
        right--;
    }
    return true;
}

// Pattern 2: Same Direction - Remove Duplicates
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    
    int slow = 0;  // Points to last unique element
    
    for (int fast = 1; fast < nums.length; fast++) {
        if (nums[fast] != nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }
    
    return slow + 1;  // Length of unique elements
}

// Pattern 3: Merge Two Sorted Arrays
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int p1 = m - 1;  // Pointer for nums1
    int p2 = n - 1;  // Pointer for nums2  
    int p = m + n - 1;  // Pointer for merged result
    
    // Merge from back to avoid overwriting
    while (p1 >= 0 && p2 >= 0) {
        if (nums1[p1] > nums2[p2]) {
            nums1[p] = nums1[p1];
            p1--;
        } else {
            nums1[p] = nums2[p2];
            p2--;
        }
        p--;
    }
    
    // Copy remaining elements from nums2
    while (p2 >= 0) {
        nums1[p] = nums2[p2];
        p2--;
        p--;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### When to Use Two Pointers
- **Problem Indicators:**
  - Sorted array/string
  - Finding pairs with certain sum/difference
  - Reversing/palindrome
  - Partitioning array
  - In-place operations

#### Decision Tree:
```java
/*
Should I use Two Pointers?

1. Is the array/string sorted or can be sorted?
   → YES: Consider two pointers
   
2. Am I looking for a pair/triplet?
   → YES: Two pointers can help
   
3. Do I need O(1) space?
   → YES: Two pointers for in-place
   
4. Am I comparing elements from ends?
   → YES: Opposite direction pointers
   
5. Am I removing/filtering elements?
   → YES: Same direction pointers
*/

// Example: Two Sum in Sorted Array
public int[] twoSumSorted(int[] numbers, int target) {
    int left = 0;
    int right = numbers.length - 1;
    
    while (left < right) {
        int sum = numbers[left] + numbers[right];
        
        if (sum == target) {
            return new int[]{left + 1, right + 1};  // 1-indexed
        } else if (sum < target) {
            left++;  // Need larger sum
        } else {
            right--;  // Need smaller sum
        }
    }
    
    return new int[]{-1, -1};
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
- **Then:** [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)

```java
// Move Zeroes - Maintain Order
public void moveZeroes(int[] nums) {
    int nonZeroPos = 0;  // Position to place next non-zero
    
    // First pass: move all non-zeros to front
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != 0) {
            nums[nonZeroPos] = nums[i];
            nonZeroPos++;
        }
    }
    
    // Second pass: fill remaining with zeros
    for (int i = nonZeroPos; i < nums.length; i++) {
        nums[i] = 0;
    }
    
    // Alternative: One pass with swapping
    /*
    int nonZeroPos = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != 0) {
            int temp = nums[nonZeroPos];
            nums[nonZeroPos] = nums[i];
            nums[i] = temp;
            nonZeroPos++;
        }
    }
    */
}
```

### 📝 **Day 1 Checklist**
- [ ] Understand three two-pointer patterns
- [ ] Implement palindrome check with two pointers
- [ ] Master remove duplicates pattern
- [ ] Complete Valid Palindrome problem
- [ ] Complete Move Zeroes problem

---

## 📅 **DAY 2: Advanced Two Pointers Techniques**

### 🌅 **Morning Session (45 minutes)**
#### Three Pointers and Beyond
- **Extending two pointers to solve complex problems**

```java
// Dutch National Flag Problem (Sort Colors)
// Sort array with only 0, 1, 2
public void sortColors(int[] nums) {
    int low = 0;    // Boundary of 0s
    int high = nums.length - 1;  // Boundary of 2s
    int mid = 0;    // Current element
    
    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums, low, mid);
            low++;
            mid++;
        } else if (nums[mid] == 1) {
            mid++;
        } else {  // nums[mid] == 2
            swap(nums, mid, high);
            high--;
            // Don't increment mid - need to check swapped element
        }
    }
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}

// Three Sum Problem
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(nums);  // Essential for two pointers
    
    for (int i = 0; i < nums.length - 2; i++) {
        // Skip duplicates for first number
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        
        int left = i + 1;
        int right = nums.length - 1;
        int target = -nums[i];  // Looking for two sum = -nums[i]
        
        while (left < right) {
            int sum = nums[left] + nums[right];
            
            if (sum == target) {
                result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                
                // Skip duplicates
                while (left < right && nums[left] == nums[left + 1]) left++;
                while (left < right && nums[right] == nums[right - 1]) right--;
                
                left++;
                right--;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
    }
    
    return result;
}

// Four Sum (extending the pattern)
public List<List<Integer>> fourSum(int[] nums, int target) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(nums);
    
    for (int i = 0; i < nums.length - 3; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        
        for (int j = i + 1; j < nums.length - 2; j++) {
            if (j > i + 1 && nums[j] == nums[j - 1]) continue;
            
            int left = j + 1;
            int right = nums.length - 1;
            long remainingTarget = (long)target - nums[i] - nums[j];
            
            while (left < right) {
                long sum = nums[left] + nums[right];
                
                if (sum == remainingTarget) {
                    result.add(Arrays.asList(nums[i], nums[j], 
                                           nums[left], nums[right]));
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    left++;
                    right--;
                } else if (sum < remainingTarget) {
                    left++;
                } else {
                    right--;
                }
            }
        }
    }
    
    return result;
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Trapping Water Problems
```java
// Container With Most Water
public int maxArea(int[] height) {
    int left = 0;
    int right = height.length - 1;
    int maxWater = 0;
    
    while (left < right) {
        int width = right - left;
        int minHeight = Math.min(height[left], height[right]);
        int currentWater = width * minHeight;
        maxWater = Math.max(maxWater, currentWater);
        
        // Move pointer with smaller height
        // (moving larger height can only decrease area)
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }
    
    return maxWater;
}

// Trapping Rain Water (preview for advanced)
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
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- **Challenge:** [15. 3Sum](https://leetcode.com/problems/3sum/)

### 📝 **Day 2 Checklist**
- [ ] Understand three-pointer technique (Dutch Flag)
- [ ] Implement 3Sum with duplicate handling
- [ ] Master Container With Most Water logic
- [ ] Complete both LeetCode problems
- [ ] Understand pointer movement decisions

---

## 📅 **DAY 3: Sliding Window Fundamentals**

### 🌅 **Morning Session (45 minutes)**
#### Fixed Size Sliding Window
- **Core concept and implementation**

```java
// Fixed Window Template
public void fixedSlidingWindow(int[] arr, int k) {
    // k = window size
    int windowSum = 0;
    
    // Initialize first window
    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    
    int maxSum = windowSum;
    
    // Slide the window
    for (int i = k; i < arr.length; i++) {
        windowSum += arr[i];        // Add new element
        windowSum -= arr[i - k];    // Remove old element
        maxSum = Math.max(maxSum, windowSum);
    }
}

// Maximum Average Subarray
public double findMaxAverage(int[] nums, int k) {
    int windowSum = 0;
    
    // First window
    for (int i = 0; i < k; i++) {
        windowSum += nums[i];
    }
    
    int maxSum = windowSum;
    
    // Slide window
    for (int i = k; i < nums.length; i++) {
        windowSum += nums[i] - nums[i - k];
        maxSum = Math.max(maxSum, windowSum);
    }
    
    return (double) maxSum / k;
}

// Contains Duplicate II (within k distance)
public boolean containsNearbyDuplicate(int[] nums, int k) {
    HashSet<Integer> window = new HashSet<>();
    
    for (int i = 0; i < nums.length; i++) {
        // Remove element outside window
        if (i > k) {
            window.remove(nums[i - k - 1]);
        }
        
        // Check if duplicate exists in window
        if (!window.add(nums[i])) {
            return true;
        }
    }
    
    return false;
}

// Sliding Window Maximum (using deque)
public int[] maxSlidingWindow(int[] nums, int k) {
    if (nums.length == 0 || k == 0) return new int[0];
    
    int n = nums.length;
    int[] result = new int[n - k + 1];
    Deque<Integer> deque = new ArrayDeque<>();  // Stores indices
    
    for (int i = 0; i < n; i++) {
        // Remove elements outside window
        while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
            deque.pollFirst();
        }
        
        // Remove smaller elements (they can't be max)
        while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
            deque.pollLast();
        }
        
        deque.offerLast(i);
        
        // Add to result after first window
        if (i >= k - 1) {
            result[i - k + 1] = nums[deque.peekFirst()];
        }
    }
    
    return result;
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Variable Size Sliding Window
```java
// Variable Window Template
public int variableSlidingWindow(String s, int condition) {
    int left = 0;
    int result = 0;
    // Additional data structures (HashMap, etc.)
    
    for (int right = 0; right < s.length(); right++) {
        // Expand window by including s[right]
        
        // Contract window while condition is violated
        while (/* condition violated */) {
            // Remove s[left] from window
            left++;
        }
        
        // Update result
        result = Math.max(result, right - left + 1);
    }
    
    return result;
}

// Longest Substring with At Most K Distinct Characters
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    if (s == null || s.length() == 0 || k == 0) {
        return 0;
    }
    
    HashMap<Character, Integer> window = new HashMap<>();
    int left = 0;
    int maxLen = 0;
    
    for (int right = 0; right < s.length(); right++) {
        char rightChar = s.charAt(right);
        window.put(rightChar, window.getOrDefault(rightChar, 0) + 1);
        
        // Shrink window if more than k distinct chars
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

// Longest Substring Without Repeating Characters
public int lengthOfLongestSubstring(String s) {
    HashSet<Character> window = new HashSet<>();
    int left = 0;
    int maxLen = 0;
    
    for (int right = 0; right < s.length(); right++) {
        // Shrink window until no duplicate
        while (window.contains(s.charAt(right))) {
            window.remove(s.charAt(left));
            left++;
        }
        
        window.add(s.charAt(right));
        maxLen = Math.max(maxLen, right - left + 1);
    }
    
    return maxLen;
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- **Bonus:** [643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/)

### 📝 **Day 3 Checklist**
- [ ] Understand fixed vs variable window
- [ ] Implement fixed window for max sum
- [ ] Master variable window expansion/contraction
- [ ] Complete Longest Substring Without Repeating
- [ ] Know when to use each window type

---

## 📅 **DAY 4: Advanced Sliding Window Patterns**

### 🌅 **Morning Session (45 minutes)**
#### Window with Complex Conditions
```java
// Minimum Window Substring
public String minWindow(String s, String t) {
    if (s.length() == 0 || t.length() == 0) return "";
    
    // Character frequency in t
    HashMap<Character, Integer> dictT = new HashMap<>();
    for (char c : t.toCharArray()) {
        dictT.put(c, dictT.getOrDefault(c, 0) + 1);
    }
    
    int required = dictT.size();  // Unique characters in t
    int formed = 0;  // Unique chars in window with desired frequency
    
    HashMap<Character, Integer> windowCounts = new HashMap<>();
    
    int left = 0, right = 0;
    int[] ans = {-1, 0, 0};  // {window length, left, right}
    
    while (right < s.length()) {
        char c = s.charAt(right);
        windowCounts.put(c, windowCounts.getOrDefault(c, 0) + 1);
        
        if (dictT.containsKey(c) && 
            windowCounts.get(c).intValue() == dictT.get(c).intValue()) {
            formed++;
        }
        
        // Try to contract window
        while (left <= right && formed == required) {
            c = s.charAt(left);
            
            // Update result
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

// Find All Anagrams in String
public List<Integer> findAnagrams(String s, String p) {
    List<Integer> result = new ArrayList<>();
    if (s.length() < p.length()) return result;
    
    // Character frequency maps
    int[] pFreq = new int[26];
    int[] windowFreq = new int[26];
    
    for (char c : p.toCharArray()) {
        pFreq[c - 'a']++;
    }
    
    // Sliding window
    for (int i = 0; i < s.length(); i++) {
        windowFreq[s.charAt(i) - 'a']++;
        
        // Remove leftmost character after window size exceeds
        if (i >= p.length()) {
            windowFreq[s.charAt(i - p.length()) - 'a']--;
        }
        
        // Check if window matches pattern
        if (i >= p.length() - 1 && Arrays.equals(pFreq, windowFreq)) {
            result.add(i - p.length() + 1);
        }
    }
    
    return result;
}

// Permutation in String
public boolean checkInclusion(String s1, String s2) {
    if (s1.length() > s2.length()) return false;
    
    int[] s1Freq = new int[26];
    int[] windowFreq = new int[26];
    
    for (char c : s1.toCharArray()) {
        s1Freq[c - 'a']++;
    }
    
    for (int i = 0; i < s2.length(); i++) {
        windowFreq[s2.charAt(i) - 'a']++;
        
        if (i >= s1.length()) {
            windowFreq[s2.charAt(i - s1.length()) - 'a']--;
        }
        
        if (Arrays.equals(s1Freq, windowFreq)) {
            return true;
        }
    }
    
    return false;
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Optimized Sliding Window Techniques
```java
// Sliding Window with Character Match Count
public boolean checkInclusionOptimized(String s1, String s2) {
    if (s1.length() > s2.length()) return false;
    
    int[] freq = new int[26];
    for (char c : s1.toCharArray()) {
        freq[c - 'a']++;
    }
    
    int left = 0, right = 0;
    int count = s1.length();  // Characters to match
    
    while (right < s2.length()) {
        // Expand window
        if (freq[s2.charAt(right) - 'a'] > 0) {
            count--;
        }
        freq[s2.charAt(right) - 'a']--;
        right++;
        
        // Check if window matches
        if (count == 0) return true;
        
        // Shrink window if size exceeds
        if (right - left == s1.length()) {
            if (freq[s2.charAt(left) - 'a'] >= 0) {
                count++;
            }
            freq[s2.charAt(left) - 'a']++;
            left++;
        }
    }
    
    return false;
}

// Substring with Concatenation of All Words
public List<Integer> findSubstring(String s, String[] words) {
    List<Integer> result = new ArrayList<>();
    if (s == null || s.length() == 0 || words == null || words.length == 0) {
        return result;
    }
    
    int wordLength = words[0].length();
    int wordCount = words.length;
    int totalLength = wordLength * wordCount;
    
    // Word frequency map
    HashMap<String, Integer> wordFreq = new HashMap<>();
    for (String word : words) {
        wordFreq.put(word, wordFreq.getOrDefault(word, 0) + 1);
    }
    
    // Try each starting position within a word length
    for (int i = 0; i < wordLength; i++) {
        int left = i;
        int count = 0;
        HashMap<String, Integer> windowFreq = new HashMap<>();
        
        for (int right = i; right <= s.length() - wordLength; right += wordLength) {
            String word = s.substring(right, right + wordLength);
            
            if (wordFreq.containsKey(word)) {
                windowFreq.put(word, windowFreq.getOrDefault(word, 0) + 1);
                count++;
                
                // Shrink window if word frequency exceeds
                while (windowFreq.get(word) > wordFreq.get(word)) {
                    String leftWord = s.substring(left, left + wordLength);
                    windowFreq.put(leftWord, windowFreq.get(leftWord) - 1);
                    count--;
                    left += wordLength;
                }
                
                // Check if valid window
                if (count == wordCount) {
                    result.add(left);
                }
            } else {
                // Reset window
                windowFreq.clear();
                count = 0;
                left = right + wordLength;
            }
        }
    }
    
    return result;
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- **Or:** [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

### 📝 **Day 4 Checklist**
- [ ] Master complex window conditions
- [ ] Implement character frequency matching
- [ ] Understand optimization with match counts
- [ ] Complete Minimum Window Substring or Anagrams
- [ ] Know multiple window validation approaches

---

## 📅 **DAY 5: Combining Two Pointers and Sliding Window**

### 🌅 **Morning Session (45 minutes)**
#### Hybrid Approaches
```java
// Longest Repeating Character Replacement
public int characterReplacement(String s, int k) {
    int[] freq = new int[26];
    int maxFreq = 0;
    int left = 0;
    int maxLen = 0;
    
    for (int right = 0; right < s.length(); right++) {
        freq[s.charAt(right) - 'A']++;
        maxFreq = Math.max(maxFreq, freq[s.charAt(right) - 'A']);
        
        // Window size - maxFreq = characters to replace
        while (right - left + 1 - maxFreq > k) {
            freq[s.charAt(left) - 'A']--;
            left++;
            // Note: We don't update maxFreq here (optimization)
        }
        
        maxLen = Math.max(maxLen, right - left + 1);
    }
    
    return maxLen;
}

// Max Consecutive Ones III
public int longestOnes(int[] nums, int k) {
    int left = 0;
    int zerosCount = 0;
    int maxLen = 0;
    
    for (int right = 0; right < nums.length; right++) {
        if (nums[right] == 0) {
            zerosCount++;
        }
        
        // Shrink window if too many zeros
        while (zerosCount > k) {
            if (nums[left] == 0) {
                zerosCount--;
            }
            left++;
        }
        
        maxLen = Math.max(maxLen, right - left + 1);
    }
    
    return maxLen;
}

// Subarrays with K Different Integers
public int subarraysWithKDistinct(int[] nums, int k) {
    return atMostKDistinct(nums, k) - atMostKDistinct(nums, k - 1);
}

private int atMostKDistinct(int[] nums, int k) {
    HashMap<Integer, Integer> count = new HashMap<>();
    int left = 0;
    int result = 0;
    
    for (int right = 0; right < nums.length; right++) {
        count.put(nums[right], count.getOrDefault(nums[right], 0) + 1);
        
        while (count.size() > k) {
            count.put(nums[left], count.get(nums[left]) - 1);
            if (count.get(nums[left]) == 0) {
                count.remove(nums[left]);
            }
            left++;
        }
        
        // Add all subarrays ending at right
        result += right - left + 1;
    }
    
    return result;
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Two Pointers in 2D Arrays
```java
// Search in 2D Matrix II
public boolean searchMatrix(int[][] matrix, int target) {
    if (matrix == null || matrix.length == 0) {
        return false;
    }
    
    // Start from top-right corner
    int row = 0;
    int col = matrix[0].length - 1;
    
    while (row < matrix.length && col >= 0) {
        if (matrix[row][col] == target) {
            return true;
        } else if (matrix[row][col] > target) {
            col--;  // Move left
        } else {
            row++;  // Move down
        }
    }
    
    return false;
}

// Shortest Distance to Target Color
public List<Integer> shortestDistanceColor(int[] colors, int[][] queries) {
    int n = colors.length;
    int[][] leftDistance = new int[3][n];
    int[][] rightDistance = new int[3][n];
    
    // Initialize with max values
    for (int i = 0; i < 3; i++) {
        Arrays.fill(leftDistance[i], Integer.MAX_VALUE);
        Arrays.fill(rightDistance[i], Integer.MAX_VALUE);
    }
    
    // Left to right scan
    for (int i = 0; i < n; i++) {
        int color = colors[i] - 1;
        leftDistance[color][i] = 0;
        
        if (i > 0) {
            for (int c = 0; c < 3; c++) {
                if (leftDistance[c][i - 1] != Integer.MAX_VALUE) {
                    leftDistance[c][i] = Math.min(leftDistance[c][i], 
                                                  leftDistance[c][i - 1] + 1);
                }
            }
        }
    }
    
    // Right to left scan
    for (int i = n - 1; i >= 0; i--) {
        int color = colors[i] - 1;
        rightDistance[color][i] = 0;
        
        if (i < n - 1) {
            for (int c = 0; c < 3; c++) {
                if (rightDistance[c][i + 1] != Integer.MAX_VALUE) {
                    rightDistance[c][i] = Math.min(rightDistance[c][i], 
                                                   rightDistance[c][i + 1] + 1);
                }
            }
        }
    }
    
    List<Integer> result = new ArrayList<>();
    for (int[] query : queries) {
        int index = query[0];
        int color = query[1] - 1;
        
        int distance = Math.min(leftDistance[color][index], 
                               rightDistance[color][index]);
        result.add(distance == Integer.MAX_VALUE ? -1 : distance);
    }
    
    return result;
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
- **Bonus:** [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

### 📝 **Day 5 Checklist**
- [ ] Understand hybrid two-pointer/sliding window
- [ ] Master "at most K" to "exactly K" conversion
- [ ] Implement character replacement logic
- [ ] Complete both LeetCode problems
- [ ] Know when to combine techniques

---

## 📅 **DAY 6: Practice & Pattern Mastery**

### 🌅 **Morning Session (60 minutes)**
#### Pattern Review and Quick Reference
```java
// TWO POINTERS PATTERNS REFERENCE

// 1. Opposite Direction
int left = 0, right = arr.length - 1;
while (left < right) {
    // Process and move pointers based on condition
}

// 2. Same Direction (Fast-Slow)
int slow = 0;
for (int fast = 0; fast < arr.length; fast++) {
    if (condition) {
        // Process slow pointer
        slow++;
    }
}

// 3. Multiple Arrays Merge
int p1 = 0, p2 = 0, p3 = 0;
while (p1 < arr1.length && p2 < arr2.length) {
    // Compare and advance appropriate pointer
}

// SLIDING WINDOW PATTERNS REFERENCE

// 1. Fixed Size Window
for (int i = k; i < arr.length; i++) {
    // Add arr[i], remove arr[i-k]
}

// 2. Variable Size Window
int left = 0;
for (int right = 0; right < arr.length; right++) {
    // Expand window
    while (windowInvalid) {
        // Shrink window from left
        left++;
    }
    // Update result
}

// 3. Window with Frequency Map
HashMap<Character, Integer> window = new HashMap<>();
for (int right = 0; right < s.length(); right++) {
    window.put(s.charAt(right), window.getOrDefault(s.charAt(right), 0) + 1);
    while (window.size() > k) {
        // Shrink and update map
    }
}
```

### 🌞 **Afternoon Session (90 minutes)**
#### Problem-Solving Marathon
**Complete these problems independently:**

1. **Squares of a Sorted Array**
```java
public int[] sortedSquares(int[] nums) {
    // Two pointers from ends approach
    // Your implementation
}
```

2. **Fruit Into Baskets**
```java
public int totalFruit(int[] fruits) {
    // Sliding window with at most 2 types
    // Your implementation  
}
```

3. **Subarray Product Less Than K**
```java
public int numSubarrayProductLessThanK(int[] nums, int k) {
    // Sliding window counting subarrays
    // Your implementation
}
```

4. **Backspace String Compare**
```java
public boolean backspaceCompare(String s, String t) {
    // Two pointers from end, handle backspaces
    // Your implementation
}
```

### 🌙 **Evening Session (45 minutes)**
#### LeetCode Challenge Set
- **Must Complete:**
  1. [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)
  2. [904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)
  3. [713. Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)

### 📝 **Day 6 Checklist**
- [ ] Review all two-pointer patterns
- [ ] Review all sliding window patterns
- [ ] Complete 4 practice problems
- [ ] Solve LeetCode challenge set
- [ ] Identify personal weak areas

---

## 📅 **DAY 7: Week Review & Advanced Challenges**

### 🌅 **Morning Session (60 minutes)**
#### Comprehensive Knowledge Assessment
```java
// SELF-ASSESSMENT QUIZ

// 1. Time Complexity Analysis
// What's the time complexity?
public int solution1(int[] nums, int k) {
    Arrays.sort(nums);  // O(?)
    int left = 0, right = nums.length - 1;
    while (left < right) {  // O(?)
        if (nums[left] + nums[right] == k) return true;
        // pointer movement
    }
    // Total: O(?)
}

// 2. Choose the Right Approach
// Problem: Find longest subarray with sum <= k
// Which approach: Two Pointers or Sliding Window? Why?

// 3. Debug this code
public int[] twoSum(int[] nums, int target) {
    Arrays.sort(nums);  // Problem?
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) {
            return new int[]{left, right};  // Issue?
        }
        // pointer movement
    }
}

// 4. Optimize this solution
public int longestSubstring(String s, int k) {
    int max = 0;
    for (int i = 0; i < s.length(); i++) {
        HashSet<Character> set = new HashSet<>();
        for (int j = i; j < s.length(); j++) {
            set.add(s.charAt(j));
            if (set.size() <= k) {
                max = Math.max(max, j - i + 1);
            }
        }
    }
    return max;  // How to optimize to O(n)?
}

// 5. Pattern Recognition
// Given: sorted array, find two numbers with difference k
// Which pattern fits best?
```

### 🌞 **Afternoon Session (90 minutes)**
#### Advanced Problem Set
```java
// 1. Trapping Rain Water (Hard)
public int trap(int[] height) {
    // Two pointers approach
    // Your optimized implementation
}

// 2. Sliding Window Median (Hard)
public double[] medianSlidingWindow(int[] nums, int k) {
    // Sliding window with ordered data structure
    // Your implementation
}

// 3. Minimum Size Subarray Sum
public int minSubArrayLen(int target, int[] nums) {
    int left = 0;
    int sum = 0;
    int minLen = Integer.MAX_VALUE;
    
    for (int right = 0; right < nums.length; right++) {
        sum += nums[right];
        
        while (sum >= target) {
            minLen = Math.min(minLen, right - left + 1);
            sum -= nums[left];
            left++;
        }
    }
    
    return minLen == Integer.MAX_VALUE ? 0 : minLen;
}

// 4. Count Number of Nice Subarrays
public int numberOfSubarrays(int[] nums, int k) {
    return atMostK(nums, k) - atMostK(nums, k - 1);
}

private int atMostK(int[] nums, int k) {
    int left = 0, odds = 0, count = 0;
    
    for (int right = 0; right < nums.length; right++) {
        if (nums[right] % 2 == 1) odds++;
        
        while (odds > k) {
            if (nums[left] % 2 == 1) odds--;
            left++;
        }
        
        count += right - left + 1;
    }
    
    return count;
}
```

### 🌙 **Evening Session (30 minutes)**
#### Week 3 Mastery Documentation
```java
// WEEK 3 COMPLETE REFERENCE SHEET

/* ========== TWO POINTERS MASTERY ========== */

// Pattern 1: Opposite Direction
// Use when: sorted array, finding pairs, palindromes
// Examples: Two Sum II, Container With Most Water, Valid Palindrome

// Pattern 2: Same Direction (Fast-Slow)  
// Use when: removing duplicates, partitioning, linked list cycles
// Examples: Remove Duplicates, Move Zeroes, Remove Element

// Pattern 3: Multiple Arrays
// Use when: merging sorted arrays, finding intersection
// Examples: Merge Sorted Array, Intersection of Arrays

/* ========== SLIDING WINDOW MASTERY ========== */

// Pattern 1: Fixed Size
// Use when: k-size subarray/substring problems
// Examples: Max Average Subarray, Contains Duplicate II

// Pattern 2: Variable Size (Expanding/Shrinking)
// Use when: optimize window based on condition
// Examples: Longest Substring Without Repeating, Min Window Substring

// Pattern 3: With HashMap/Frequency
// Use when: tracking element counts in window
// Examples: Longest K Distinct, Find All Anagrams

/* ========== DECISION FLOWCHART ========== */
/*
Is array sorted or can be sorted?
├─ YES → Consider Two Pointers
│   ├─ Finding pairs? → Opposite direction
│   └─ Filtering/partitioning? → Same direction
└─ NO → Consider Sliding Window
    ├─ Fixed size constraint? → Fixed window
    └─ Optimize for condition? → Variable window
*/

/* ========== OPTIMIZATION TIPS ========== */
// 1. Two pointers often O(n) time, O(1) space
// 2. Sliding window avoids recalculation
// 3. Use HashMap for O(1) lookups in window
// 4. "Exactly K" = AtMost(K) - AtMost(K-1)
// 5. For 2D arrays, start from corner for elimination

/* ========== COMMON MISTAKES TO AVOID ========== */
// 1. Forgetting to handle duplicates in sum problems
// 2. Not updating window state when shrinking
// 3. Off-by-one errors in window size
// 4. Modifying array when need to preserve indices
// 5. Integer overflow in sum calculations
```

### 📝 **Day 7 Final Checklist**
- [ ] Score at least 4/5 on self-assessment
- [ ] Complete all Week 3 core problems
- [ ] Solve at least one hard problem
- [ ] Create comprehensive reference sheet
- [ ] Document top learnings and patterns
- [ ] Ready for Week 4: Linked Lists

---

## 🎯 **End of Week 3 Milestones**

### You Should Now Be Able To:
✅ Identify when to use two pointers vs sliding window  
✅ Implement all three two-pointer patterns  
✅ Handle fixed and variable sliding windows  
✅ Optimize brute force to linear time  
✅ Combine techniques for complex problems  
✅ Solve medium difficulty problems confidently  

### Problems Completed (Minimum):
- ✅ Valid Palindrome
- ✅ Move Zeroes  
- ✅ Container With Most Water
- ✅ 3Sum
- ✅ Longest Substring Without Repeating Characters
- ✅ Minimum Window Substring (attempted)
- ✅ Find All Anagrams

### Core Patterns Mastered:
1. **Opposite Direction Pointers** - Pairs, palindromes
2. **Same Direction Pointers** - Filtering, partitioning
3. **Fixed Sliding Window** - K-size problems
4. **Variable Sliding Window** - Optimization problems
5. **Window with HashMap** - Frequency tracking

### Skills Developed:
- 🎯 O(n) solutions for array/string problems
- 🎯 Space-efficient in-place operations
- 🎯 Pattern recognition for optimization
- 🎯 Handling edge cases systematically
- 🎯 Debugging pointer movement logic

### Prepare for Week 4:
- Linked Lists will use fast-slow pointer pattern
- Review pointer manipulation basics
- Understand reference vs value in Java
- Rest and consolidate Week 3 learning!

## 💪 **Week 3 Reflection Prompts**
1. Which pattern (two pointers vs sliding window) feels more intuitive?
2. What was your biggest "aha" moment this week?
3. Which problem challenged you the most and why?
4. How has this week improved your problem-solving speed?
5. What optimization technique was most surprising?

## 🎉 **Outstanding Progress!**
Week 3 is often considered the most crucial week for interview preparation. Two Pointers and Sliding Window techniques appear in 40-50% of array/string problems. Your ability to recognize and apply these patterns will significantly boost your problem-solving efficiency. You're now equipped with powerful optimization techniques that transform O(n²) solutions to O(n). Keep practicing these patterns - they become second nature with repetition!
