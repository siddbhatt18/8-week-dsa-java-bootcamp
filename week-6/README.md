**Week 6 Focus:**  
- Heaps / PriorityQueue in Java (min‑heap, max‑heap)  
- Top‑K and “keep best few” patterns  
- Greedy problems powered by heaps  
- Grid as graph: DFS/BFS on 2D matrices (Number of Islands, Rotting Oranges)  

Assume ~2–3 hours/day. Maintain the routine: **think → write on paper → code → reflect**.

---

## Shared Setup for the Week

You’ll use:

```java
import java.util.*;
```

And often:

- `PriorityQueue<Integer>` (min‑heap)
- `PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);`
- For grid problems, a directions array:

```java
int[][] dirs = {{1,0}, {-1,0}, {0,1}, {0,-1}};
```

---

## Day 1 – PriorityQueue Basics + Min/Max Heap

### 1. Concept: What Is a Heap? (25–35 min)

On paper:

- **Heap** (binary heap):
  - A tree‑based structure where:
    - Min‑heap: parent ≤ children → `peek()` is minimum.
    - Max‑heap: parent ≥ children → `peek()` is maximum.
  - Efficient operations:
    - Insert (push/offer): O(log n)
    - Extract min/max (poll): O(log n)
    - Peek: O(1)

- In Java, `PriorityQueue` is a **min‑heap by default**.

Write down:

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
```

### 2. Coding: Simple Heap Operations (45–60 min)

Create `Week6Day1.java`.

1. **Min‑heap demo**

   ```java
   PriorityQueue<Integer> minHeap = new PriorityQueue<>();
   minHeap.offer(5);
   minHeap.offer(2);
   minHeap.offer(8);
   minHeap.offer(1);
   ```

   - Write a loop that polls all elements and prints them:
     - Expected order: `1, 2, 5, 8`.

2. **Max‑heap demo**

   ```java
   PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
   ```

   - Add same numbers, poll all out, print:
     - Expected: `8, 5, 2, 1`.

3. **Practice functions**

   - `int[] kSmallest(int[] nums, int k)`  
     Approach:
     - Add all elements to min‑heap.
     - Poll `k` times → store in array.
   - For now, this is O(n log n); optimization comes later.

**Think in comments:**
- Why is polling `k` elements O(k log n) after building the heap?
- How would brute force (sorting the whole array) compare?

### 3. Reflection (10–15 min)

Write:
- When is a heap better than sorting all elements?
- What’s one example where you only need “top K” and not the whole sorted list?

---

## Day 2 – Kth Largest Element in an Array (Top‑K with Heap)

### 1. Quick Review (10–15 min)

From memory, on paper:
- Write how to create min‑heap and max‑heap in Java (`PriorityQueue` syntax).
- Describe what `offer`, `poll`, and `peek` do.

### 2. Concept: Top‑K with Fixed‑Size Heap (25–35 min)

On paper:

- Core idea:
  - To find **Kth largest**:
    - Maintain a **min‑heap of size K**.
    - Iterate through numbers:
      - Push current number.
      - If heap size exceeds K, poll the smallest.
    - At the end, heap top = Kth largest.

Why?
- Heap always keeps the K **largest** seen so far (min‑heap of that set).
- Smallest among them is the Kth largest overall.

Complexity:
- Each insert/poll O(log K) → overall O(n log K), better than O(n log n) when K small.

### 3. LeetCode: Kth Largest Element in an Array (Medium) (60–75 min)

LC **215. Kth Largest Element in an Array**.

1. **Think First (15–20 min):**
   - Brute force: sort array descending → answer at index K‑1 → O(n log n).
   - Optimized: min‑heap of size K.

2. **Implement:**

   ```java
   public int findKthLargest(int[] nums, int k) {
       PriorityQueue<Integer> minHeap = new PriorityQueue<>();
       for (int num : nums) {
           minHeap.offer(num);
           if (minHeap.size() > k) {
               minHeap.poll();
           }
       }
       return minHeap.peek();
   }
   ```

3. Test with small arrays and K values.

### 4. Custom Variant: K Smallest Elements (30–40 min)

In `Week6Day2.java`:

Implement:

```java
int[] kSmallestElements(int[] nums, int k)
```

Approach (mirror logic):

- Use a **max‑heap** of size K:
  - Keep the K smallest.
  - For each element:
    - Offer it into max‑heap.
    - If size > K, poll (removes largest of the K+1, leaving the smallest K).

Return the K elements (order doesn’t matter, but you can sort at the end if you want).

### 5. Reflection (10–15 min)

Write:
- Tradeoff: `O(n log K)` with heap vs `O(n log n)` sorting.
- Describe a situation (real or imagined) where K is much smaller than n, making this pattern very useful.

---

## Day 3 – Top K Frequent Elements (Heap + HashMap)

### 1. Quick Review (10–15 min)

- From memory, describe the algorithm for `findKthLargest` in 3–5 bullet points.

### 2. Concept: Counting + Heap (Top Frequencies) (25–35 min)

On paper:

- Problem pattern:
  1. Count frequencies using `HashMap`.
  2. Use a heap to keep top K based on frequency.

- Key pattern:
  - Elements: numbers or strings.
  - We want highest frequencies.
  - Use:
    - `Map<Integer, Integer> freq = new HashMap<>();`
    - Then a `PriorityQueue<Map.Entry<Integer, Integer>>` or custom object with comparator on `value` (frequency).

### 3. LeetCode: Top K Frequent Elements (Medium) (60–75 min)

LC **347. Top K Frequent Elements**.

1. **Think First (15–20 min):**
   - Step 1: Build frequency map.
   - Step 2: Min‑heap of size K based on frequency.
     - Comparator: `Comparator.comparingInt(Map.Entry::getValue)`
   - Step 3: Extract keys from heap into result array.

2. **Implement:**

   Rough outline:

   ```java
   public int[] topKFrequent(int[] nums, int k) {
       Map<Integer, Integer> freq = new HashMap<>();
       for (int num : nums) {
           freq.put(num, freq.getOrDefault(num, 0) + 1);
       }

       PriorityQueue<Map.Entry<Integer, Integer>> minHeap =
               new PriorityQueue<>(Comparator.comparingInt(Map.Entry::getValue));

       for (Map.Entry<Integer, Integer> entry : freq.entrySet()) {
           minHeap.offer(entry);
           if (minHeap.size() > k) {
               minHeap.poll();
           }
       }

       int[] res = new int[k];
       for (int i = k - 1; i >= 0; i--) {
           res[i] = minHeap.poll().getKey();
       }
       return res;
   }
   ```

3. Understand:  
   Why do we poll when size > k?

### 4. Optional: Use Bucket Sort (Think Only) (15–20 min)

On paper, just outline:

- Another solution uses “buckets”:
  - `List<Integer>[] buckets = new ArrayList[maxFreq + 1];`
  - Loss of need for heap.
- Don’t implement now; just note that heaps aren’t the only solution.

### 5. Reflection (10–15 min)

Write:
- What new combination of tools did you use here? (Map + heap + custom comparator).
- How does the pattern generalize? (e.g., “top K words by frequency”, “top K websites by visits”, etc.)

---

## Day 4 – Merge K Sorted Lists (Heap + Linked Lists)

### 1. Quick Review (10–15 min)

- Recap: how do you define a comparator for `PriorityQueue` in Java?
  - For integers: `(a, b) -> a - b` or `Integer.compare(a, b)`.
  - For objects: compare a field.

### 2. Concept: Merge K Sorted Lists with Min‑Heap (30–40 min)

On paper:

- Problem pattern (LC **23. Merge k Sorted Lists**):

  - Input: array `lists[]` of K sorted linked list heads.
  - Output: single merged sorted list.

- Idea:
  - Use a min‑heap of nodes:
    - Heap element: `ListNode`.
    - Comparator: based on `val`.
  - Steps:
    1. Initialize heap and add the head of each non‑null list.
    2. While heap not empty:
       - Poll smallest node.
       - Append it to result list (using dummy node + tail).
       - If that node has `next`, add `next` to heap.

Complexity:
- Every push/pop is O(log K).
- Total N nodes processed → O(N log K).

### 3. Coding Locally (60–75 min)

In `Week6Day4.java`:

1. Reuse or define `ListNode` class from earlier weeks:

   ```java
   class ListNode {
       int val;
       ListNode next;
       ListNode(int val) { this.val = val; }
   }
   ```

2. Implement:

   ```java
   ListNode mergeKLists(ListNode[] lists)
   ```

   - Use `PriorityQueue<ListNode> minHeap = new PriorityQueue<>(Comparator.comparingInt(a -> a.val));`.

3. Test locally with:
   - 3 lists:
     - `1 -> 4 -> 5`
     - `1 -> 3 -> 4`
     - `2 -> 6`
   - Verify output: `1 1 2 3 4 4 5 6`.

### 4. LeetCode: Merge k Sorted Lists (Hard, but now familiar) (30–45 min)

- Solve LC **23. Merge k Sorted Lists** using your code.
- Even though it’s labeled Hard, your heap pattern makes it manageable.

### 5. Reflection (10–15 min)

Write:
- How does this generalize merging 2 sorted lists (which you did in Week 3)?
- When K is large, why does heap beat repeated pairwise merges?

---

## Day 5 – Grid as Graph: DFS & BFS (Number of Islands)

### 1. Concept: 2D Grid as Implicit Graph (30–40 min)

On paper:

- Many problems are on 2D grids (matrix).
- Each cell `(r, c)` can have neighbors:
  - Up, down, left, right (4‑directional).
  - Sometimes 8 directions (including diagonals).

- You can treat each cell as a node in a graph.
- Edges exist between adjacent cells of interest (e.g., same region, same color).

Patterns:
- **DFS**: recursive or stack to explore connected component.
- **BFS**: queue to explore layer by layer.

Define direction array:

```java
int[][] dirs = {{1,0}, {-1,0}, {0,1}, {0,-1}};
```

Check bounds: `0 <= nr < rows`, `0 <= nc < cols`.

### 2. Problem: Number of Islands (DFS approach) (30–40 min)

LC **200. Number of Islands (Medium)**.

Paraphrase problem:
- Given a grid of `'1'` (land) and `'0'` (water), count islands.
- Island: group of `'1'`s connected horizontally or vertically.

Plan on paper:

1. Iterate through all cells.
2. When you find a `'1'` that is not yet visited:
   - Increment island count.
   - Perform DFS (or BFS) to mark all connected `'1'` as visited.
3. Use either:
   - A `boolean[][] visited` array, or
   - Modify grid in‑place: turn visited `'1'` into `'0'`.

DFS helper:

```java
void dfs(char[][] grid, int r, int c) {
    if (r < 0 || r >= rows || c < 0 || c >= cols) return;
    if (grid[r][c] != '1') return;

    grid[r][c] = '0'; // mark visited
    for (int[] d : dirs) {
        dfs(grid, r + d[0], c + d[1]);
    }
}
```

### 3. Coding: Number of Islands (60–75 min)

In `Week6Day5.java`:

1. Implement:

   ```java
   int numIslands(char[][] grid)
   ```

2. Use DFS as above.
3. Test with small grids you create.

4. Then solve LC **200. Number of Islands** on LeetCode.

### 4. Optional: BFS Version (20–30 min)

Instead of DFS:

- Use `Queue<int[]>` to hold coordinates.
- For each `'1'`, start BFS and mark visited while processing.

Outline even if you don’t implement fully.

### 5. Reflection (10–15 min)

Write:
- How is an “island” related to a connected component in graph theory?
- When might BFS vs DFS be preferable on grids (e.g., shortest path vs just region counting)?

---

## Day 6 – Rotting Oranges (Multi‑Source BFS)

### 1. Quick Review (10–15 min)

- Describe, in words, how `numIslands` works.
- Specifically, what triggers a DFS/BFS call?

### 2. Concept: Multi‑Source BFS (30–40 min)

On paper:

- Sometimes you start BFS from **multiple sources** at once.
- Example: spread of infection, fire, etc.
- Instead of a single starting node, push all starting nodes into the queue initially.

Levels in BFS:
- Each BFS level can represent a time unit (minute, hour, etc.).

### 3. Problem: Rotting Oranges (Medium) (60–75 min)

LC **994. Rotting Oranges**.

Paraphrase:
- Grid of:
  - 0 = empty
  - 1 = fresh orange
  - 2 = rotten orange
- Each minute:
  - Fresh orange adjacent (4‑dir) to rotten becomes rotten.
- Find minimum minutes for all to become rotten, or ‑1 if impossible.

On paper:

1. Steps:
   - Count total fresh oranges.
   - Initialize a queue with all starting rotten oranges (all cells == 2).
   - Perform BFS:
     - For each minute (level of BFS):
       - Process all nodes currently in queue.
       - For each, infect adjacent fresh oranges:
         - Change them to rotten.
         - Decrease fresh count.
         - Add them to queue.
   - Track minutes.
   - If fresh count becomes 0, return minutes; else ‑1.

2. Edge cases:
   - No fresh orange at start → return 0.
   - Some fresh oranges isolated → return ‑1.

### 4. Coding: Rotting Oranges (45–60 min)

In `Week6Day6.java`:

1. Implement:

   ```java
   int orangesRotting(int[][] grid)
   ```

2. Use BFS as per your outline.
3. Test with examples from the problem statement.

### 5. Reflection (10–15 min)

Write:
- What does each BFS level represent in this problem?
- Why do you need to track the count of fresh oranges?

---

## Day 7 – Consolidation: Heaps + Grid BFS/DFS

### 1. Concept Review (30–40 min)

Without looking at code, on paper:

- Summarize:
  - How a min‑heap in Java is declared and its main operations.
  - Two patterns for using heaps:
    - Kth largest (fixed‑size heap).
    - Top K frequent (hash map + heap).
  - Grid DFS vs BFS:
    - What structure stores visited nodes?
    - How to move through neighbors.

- For each problem, write a 1–2 sentence solution sketch:
  - `findKthLargest`
  - `topKFrequent`
  - `mergeKLists`
  - `numIslands`
  - `orangesRotting`

Then compare with your notes and adjust.

### 2. Re‑implement from Memory (60–75 min)

In `Week6Review.java`, re‑implement:

1. `int findKthLargest(int[] nums, int k)`
2. `int[] topKFrequent(int[] nums, int k)`
3. `ListNode mergeKLists(ListNode[] lists)` (if you’re comfortable with ListNode)
4. `int numIslands(char[][] grid)`
5. `int orangesRotting(int[][] grid)`

For each:
- Add comments:
  - Time complexity.
  - Space complexity.
  - 1–2 line intuition.

### 3. LeetCode Mini‑Session (60–75 min)

On LeetCode, solve or re‑solve:

1. **215. Kth Largest Element in an Array (Medium)**  
2. **347. Top K Frequent Elements (Medium)**  
3. **23. Merge k Sorted Lists (Hard)** – if time/energy; otherwise skip or just outline.  
4. **200. Number of Islands (Medium)**  
5. **994. Rotting Oranges (Medium)**  

Give each at least 15 minutes of honest thinking before checking hints or solutions.

### 4. End‑of‑Week Reflection (15–20 min)

In your notebook:

1. **Pattern Map:**
   - Heaps:
     - “Keep best K values while scanning.”
   - Map + Heap:
     - “Count, then keep top K by frequency/score.”
   - Grid DFS:
     - “Mark visited region starting from each unvisited land.”
   - Grid BFS:
     - “Spread effect from multiple sources level by level.”

2. **Comfort Ratings (1–5):**
   - Using `PriorityQueue` (min & max heap).
   - Writing custom comparators.
   - Designing top‑K solutions.
   - Implementing DFS on grids.
   - Implementing BFS on grids.

3. **Questions for Next Week:**
   - Example:
     - “How to handle visited states in more complex graphs (not just grids)?”
     - “When should I think DP vs BFS/DFS vs heap?”
     - “How to systematically practice combining these patterns?”

These will feed directly into Week 7, where you’ll focus on **Dynamic Programming (1D & simple 2D)** and start recognizing when a problem is better viewed as DP instead of greedy or search.

If you’d like, I can next create a **Week 7** day‑by‑day plan focusing on core DP patterns and representative LeetCode problems.
