**Week 3 Focus:**  
- Singly linked lists (implementation + pointer manipulation)  
- Fast/slow pointers, dummy nodes  
- Stack & queue fundamentals  
- Classic stack problems: parentheses, Min Stack  
- Apply patterns on LeetCode while still thinking independently

Assume ~2–3 hours/day. Adjust time, but keep the order and the habit of **thinking before coding**.

---

## Day 1 – Intro to Linked Lists (Basics & Traversal)

### 1. Concept Study: What is a Linked List? (25–35 min)

On paper / in notes:

- Contrast with arrays:
  - **Array:** contiguous memory, O(1) access by index, expensive insert/delete in middle.
  - **Singly Linked List:** nodes scattered in memory, each node holds `val` and `next` pointer.  
    - Access by index is O(n).
    - Insert/delete at known node is O(1).

Draw a simple list:
- `1 -> 3 -> 5 -> null`  
Label `head`, and show how you’d traverse it: `current = head`, move `current = current.next`.

### 2. Java Implementation of ListNode & Simple Operations (45–60 min)

Create `Week3Day1.java`:

1. **Define ListNode class**
   ```java
   class ListNode {
       int val;
       ListNode next;
       ListNode(int val) {
           this.val = val;
           this.next = null;
       }
   }
   ```

2. **Utility: Build List from Array**
   - Method: `ListNode buildList(int[] arr)`
   - Steps:
     - If array empty, return `null`.
     - Create `head = new ListNode(arr[0])`.
     - Keep a `current` pointer; loop through array, attach `current.next = new ListNode(arr[i])`.

3. **Utility: Print List**
   - Method: `void printList(ListNode head)`
   - Traverse from head, print `val` until `null`.

4. **Traverse and Count Length**
   - Method: `int length(ListNode head)`
   - Use a `count` variable and a `current` pointer.

**Write comments**:
- Time complexity for `length` (O(n)).
- Why access by index is not O(1) like arrays.

### 3. Practice: Insert at Head / Tail (30–40 min)

Add methods:

1. **Insert at Head**
   - Method: `ListNode insertAtHead(ListNode head, int val)`
   - Create new node, set `node.next = head`, return `node` as new head.

2. **Insert at Tail**
   - Method: `ListNode insertAtTail(ListNode head, int val)`
   - If head is null → new node is head.
   - Else traverse to end and attach `next`.

**Think:**  
Which operation is naturally O(1) vs O(n)? Why?

### 4. Reflection (10–15 min)

On paper:
- Explain why linked lists are good for frequent insertions/deletions in the middle.
- Explain why they’re bad when you need random access by index.

---

## Day 2 – Reverse Linked List (Core Skill)

### 1. Quick Review (10–15 min)

From memory, **without looking**:
- Write the `ListNode` class.
- Sketch the `buildList(int[] arr)` method (just logic, not perfect code).

### 2. Concept: Reversing a Singly Linked List (25–35 min)

On paper:

- Draw `1 -> 2 -> 3 -> null`, and imagine reversing to `3 -> 2 -> 1 -> null`.
- You need to **reverse the direction of arrows**.

Think about three pointers:
- `prev` (previous node)
- `curr` (current node)
- `next` (temporarily store `curr.next` before changing it)

Pseudo‑steps:

```text
prev = null
curr = head
while curr != null:
    next = curr.next
    curr.next = prev
    prev = curr
    curr = next
return prev  // new head
```

### 3. Implement: Reverse Linked List (45–60 min)

In `Week3Day2.java`:

1. **Method: `ListNode reverseList(ListNode head)`**
   - Implement iteratively using the three-pointer logic.
   - Test with:
     - Empty list (`null`)
     - Single-node list
     - Multiple-node list (`1 -> 2 -> 3`)

2. **Optional: Recursive Version (for understanding)**
   - High‑level idea:
     - Reverse from `head.next` onward, then attach `head` at the end.
   - Pseudo:
     ```java
     if (head == null || head.next == null) return head;
     ListNode newHead = reverseList(head.next);
     head.next.next = head;
     head.next = null;
     return newHead;
     ```

### 4. LeetCode: Reverse Linked List (Easy) (30–45 min)

1. **Try to solve on LeetCode from scratch using your iterative approach.**
2. Keep in mind:
   - Don’t rush; picture the pointers in your head or draw them.
3. After submission:
   - Compare your solution to LeetCode’s editorial or top solutions.
   - Note any differences in clarity or style.

### 5. Reflection (10–15 min)

On paper:
- Write a **plain English explanation** of your iterative reverse algorithm (no code).
- Mark the time and space complexity.

---

## Day 3 – Merge Two Sorted Lists + Dummy Nodes

### 1. Quick Review (10–15 min)

- From memory, outline the reverse logic (prev/curr/next).
- Don’t look at old code; try to speak/write it in bullet points.

### 2. Concept: Merging Two Sorted Linked Lists (25–35 min)

Problem idea (write it out):
- Given two sorted linked lists `l1` and `l2`, merge them into a single sorted list.

On paper, think:

- Approach:
  - Make a **dummy node** to simplify pointer handling.
  - Keep a `tail` pointer that always points to the end of the merged list.
  - While `l1 != null` and `l2 != null`:
    - Compare `l1.val` and `l2.val`.
    - Append the smaller one to `tail.next`, move that list’s pointer.
    - Move `tail`.

Why dummy node?
- Avoid special treatment of “head is null initially” — you always attach to `dummy.next`.

### 3. Implement: Merge Two Sorted Lists (45–60 min)

In `Week3Day3.java`:

1. **Method: `ListNode mergeTwoLists(ListNode l1, ListNode l2)`**
   - Use dummy node:
     ```java
     ListNode dummy = new ListNode(0);
     ListNode tail = dummy;
     ```
   - Loop:
     ```java
     while (l1 != null && l2 != null) {
         if (l1.val < l2.val) {
             tail.next = l1;
             l1 = l1.next;
         } else {
             tail.next = l2;
             l2 = l2.next;
         }
         tail = tail.next;
     }
     // Append remaining
     if (l1 != null) tail.next = l1;
     if (l2 != null) tail.next = l2;
     return dummy.next;
     ```

2. Test locally:
   - `l1 = 1 -> 3 -> 5`, `l2 = 2 -> 4 -> 6`.
   - Edge cases: one list is null.

### 4. LeetCode: Merge Two Sorted Lists (Easy) (30–45 min)

- Solve on LeetCode using your dummy‑node pattern.
- Then (if time) consider a recursive version and read one.

### 5. Concept: Fast/Slow Pointers (Intro) (15–20 min)

On paper:

- Idea:
  - `slow` moves one step at a time.
  - `fast` moves two steps at a time.
- Uses:
  - Detect cycle
  - Find middle of list

Draw:
- `1 -> 2 -> 3 -> 4 -> 5 -> null`
  - After moves:
    - `slow`: 1, 2, 3
    - `fast`: 1, 3, 5
  - When `fast` reaches end, `slow` at middle.

---

## Day 4 – Linked List Cycle + Fast/Slow Pointers

### 1. Quick Review (10–15 min)

From memory:
- Write pseudo‑code for `mergeTwoLists`.
- Note where dummy node is used and why.

### 2. Concept: Detect Linked List Cycle (20–30 min)

On paper:

- Problem:
  - Given head of a linked list, determine if it has a cycle (node pointing back).

Two approaches:
1. **HashSet**:
   - Track visited nodes.
   - If you see a node you’ve seen before → cycle.
   - O(n) time, O(n) space.

2. **Floyd’s Cycle Detection (fast/slow)**:
   - Use `slow` and `fast` pointers.
   - If there is a cycle, they will eventually meet.
   - If `fast` reaches `null`, no cycle.
   - O(n) time, O(1) space.

### 3. Implement: Linked List Cycle (45–60 min)

In `Week3Day4.java`:

1. **Method: `boolean hasCycleHashSet(ListNode head)`**
   - Use `HashSet<ListNode>` to store visited nodes.

2. **Method: `boolean hasCycle(ListNode head)` (Floyd)**
   - Initialize:
     ```java
     ListNode slow = head;
     ListNode fast = head;
     ```
   - While:
     - Move `slow = slow.next`
     - Move `fast = fast.next.next` (check for null along the way)
     - If `slow == fast` → cycle.

3. **Testing:**
   - Build a simple list and manually create a cycle:
     ```java
     ListNode head = buildList(new int[]{1,2,3,4});
     head.next.next.next.next = head.next; // create cycle
     ```

### 4. LeetCode: Linked List Cycle (Easy) (30–45 min)

- Solve using Floyd’s algorithm on LeetCode.
- Then read any alternate solutions for perspective.

### 5. Short Custom Task: Find Middle of List (15–20 min)

- Method: `ListNode middleNode(ListNode head)`
  - Use fast/slow:
    - `slow` moves 1 step, `fast` moves 2.
    - When `fast` is null or `fast.next` is null, `slow` is middle.
- Think: How is this similar to cycle detection?

---

## Day 5 – Stacks: Concept & Valid Parentheses

### 1. Concept: Stack (20–30 min)

On paper:

- Definition:
  - LIFO: Last‑In, First‑Out.
- Operations:
  - `push`, `pop`, `peek`, `isEmpty`.
- Java implementation:
  - Prefer `Deque<T>` (e.g., `ArrayDeque`) rather than `Stack` class.
  ```java
  Deque<Integer> stack = new ArrayDeque<>();
  stack.push(1);
  int x = stack.pop();
  int y = stack.peek();
  ```

Use cases:
- Parentheses matching
- Undo operations
- Function call stack (recursion)

### 2. Coding: Basic Stack Usage (20–30 min)

In `Week3Day5.java`:

1. **Reverse Array Using Stack**
   - Method: `int[] reverseWithStack(int[] nums)`
   - Push all elements into a stack, then pop back into array.

2. **Check Balanced Parentheses (custom, before LC)**
   - Method: `boolean isBalanced(String s)`
   - Supported chars: `()[]{}`.
   - Logic:
     - For each char:
       - If opening bracket → push it.
       - If closing:
         - If stack empty → false.
         - Pop top; check if it matches the correct opening.

### 3. LeetCode: Valid Parentheses (Easy) (45–60 min)

1. **Think First (10–15 min):**
   - Same as your custom `isBalanced`, but align with problem statement.
   - Decide:
     - Use stack of Characters.
     - When you see `)` check if stack top is `(`; similar for `]`, `}`.

2. **Implement & Test**

3. **Reflection:**
   - Note how stack makes it easy to process nested structures.

### 4. Short Exercise (10–15 min)

On paper:
- Describe a scenario (outside LeetCode) where a stack would be useful.
- Explain why it fits LIFO behavior.

---

## Day 6 – Min Stack & Queue Basics

### 1. Quick Review (10–15 min)

- From memory, sketch the logic for `isValid(String s)` (Valid Parentheses).

### 2. Concept: Designing Min Stack (25–35 min)

Problem idea (write it down):
- Design a stack that supports:
  - `push(x)`
  - `pop()`
  - `top()`
  - `getMin()` → returns minimum element in O(1) time.

On paper, think:

- Naive: track min by scanning all elements → O(n) per `getMin`.
- Better: use **two stacks**:
  - `stack` for values.
  - `minStack` where top = minimum so far.
  - When pushing:
    - Push to `stack`.
    - For `minStack`, push `min(x, minStack.peek())` or push x when empty.
  - When popping:
    - Pop from both `stack` and `minStack`.

### 3. Implement: MinStack Class (45–60 min)

In `Week3Day6.java`:

1. Implement a class:

   ```java
   class MinStack {
       private Deque<Integer> stack;
       private Deque<Integer> minStack;

       public MinStack() { ... }

       public void push(int x) { ... }
       public void pop() { ... }
       public int top() { ... }
       public int getMin() { ... }
   }
   ```

2. Test locally:
   - Sequence:
     - push(2), push(0), push(3), push(0)
     - getMin() → ?
     - pop(), getMin() → ?
   - Make sure minStack updates correctly.

### 4. LeetCode: Min Stack (Medium) (30–45 min)

- Paste your implementation, adjust to LC’s signature.
- Submit and verify.

### 5. Concept: Queue Basics (15–20 min)

On paper:

- Queue is FIFO: First‑In, First‑Out.
- Java usage:
  ```java
  Queue<Integer> q = new LinkedList<>();
  q.offer(1); // add
  int x = q.poll(); // remove
  int head = q.peek();
  ```
- Soon used for BFS, but today just get comfortable with the API.

**Short Coding Task (Optional, 15–20 min):**
- Implement basic queue operations, print elements after several `offer`/`poll` operations.

---

## Day 7 – Consolidation: Linked Lists + Stacks

### 1. Concept Review (30–40 min)

Without looking at prior code, on paper:

- Draw and label:
  - A simple linked list
  - `prev`, `curr`, `next` during reversal
  - `slow` and `fast` pointers for finding cycle or middle

- Write short definitions:
  - Singly linked list
  - Stack
  - Queue
  - Dummy node
  - Fast/slow pointers

### 2. Re‑implement from Memory (60–75 min)

In `Week3Review.java`, re‑implement these, no copy/paste:

1. **Reverse Linked List**
   - `ListNode reverseList(ListNode head)`

2. **Merge Two Sorted Lists**
   - `ListNode mergeTwoLists(ListNode l1, ListNode l2)`

3. **Detect Cycle (Floyd)**
   - `boolean hasCycle(ListNode head)`

4. **Valid Parentheses**
   - `boolean isValid(String s)`

5. **MinStack**
   - As class with push/pop/top/getMin.

After each:
- Add comments:
  - Time complexity.
  - Space complexity.
  - 1–2 line intuition.

### 3. Short LeetCode Session (60–75 min)

On LeetCode, try to solve (or re‑solve) these from scratch:

1. **Reverse Linked List (Easy)** – aim for clean, concise code.
2. **Merge Two Sorted Lists (Easy)** – use dummy node pattern confidently.
3. **Linked List Cycle (Easy)** – use fast/slow.
4. **Valid Parentheses (Easy)** – stack approach.

Give each at least ~15 minutes thinking time if you get stuck. Only peek at solutions after a genuine attempt.

### 4. End‑of‑Week Reflection (15–20 min)

In your notebook:

1. **List patterns learned this week:**
   - Linked list pointer manipulation (reverse, merge)
   - Dummy node usage
   - Fast/slow pointers (cycle, middle)
   - Stack for matching structures (parentheses)
   - Stack + extra-stack for MinStack

2. **Comfort ratings (1–5):**
   - Reversing linked lists
   - Using fast/slow pointers
   - Using stacks for problems
   - Implementing custom data structures (like MinStack)

3. **Questions for Next Week:**
   - Example:
     - “How to use stacks/queues for more complex problems like monotonic stacks?”
     - “How are queues used in BFS and tree traversals?”
     - “How to systematically debug pointer bugs in linked list code?”

You’ll use these to guide Week 4 (binary search, sorting, more stacks, and starting to connect these structures to search/optimization problems).

---

If you want, I can next turn **Week 4** into a similar day‑by‑day plan focusing on **binary search, sorting, and monotonic stacks**, with a set of LeetCode problems to reinforce them.
