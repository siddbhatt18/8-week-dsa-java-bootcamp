Here’s your **Week 3 – Day 1 to Day 7 plan**, focused on:

- Linked Lists (construction, traversal, manipulation)
- Fast/slow pointers
- Stacks & Queues (using Java collections)
- Applying them to core LeetCode problems

Assume again ~1.5–2 hours/day. Adjust time blocks but keep the **order**: concept → implement → LeetCode → reflect.

---

## Week 3 Focus

- Singly linked lists:
  - `ListNode` definition
  - Traversal, insert, delete, reverse
  - Fast/slow pointer (middle, cycle detection)
- Stacks & queues:
  - Use `Deque` as stack/queue
  - Classic problems: parentheses, MinStack
- LeetCode problems to reinforce these skills

---

## Day 1 – Linked List Basics & Traversal

**Goal:** Understand how linked lists work and get comfortable with basic operations.

### 1. Concept: What is a Linked List? (20–30 min)

On paper / notes:

- Compare **array vs linked list**:
  - Array:
    - Contiguous memory, O(1) random access, O(n) insertion in middle.
  - Linked list:
    - Nodes with `val` and `next` reference.
    - O(1) insert/delete at head, O(n) access by index.
- Singly linked list node in Java:

  ```java
  class ListNode {
      int val;
      ListNode next;
      ListNode(int val) {
          this.val = val;
      }
  }
  ```

### 2. Implement Basic Operations (45–60 min)

Create a small `LinkedListDemo` class and implement:

1. **Build a linked list from array**
   ```java
   ListNode buildList(int[] nums) { ... }
   ```
   - Iterate through `nums`, create nodes, chain with `next`.

2. **Traverse and print a linked list**
   ```java
   void printList(ListNode head) { ... }
   ```

3. **Insert at head**
   ```java
   ListNode insertAtHead(ListNode head, int val) { ... }
   ```

4. **Find length of a linked list**
   ```java
   int length(ListNode head) { ... }
   ```

Test with a simple `main`:
- Build list from `{1,2,3,4}`.
- Print it.
- Insert at head, print again.
- Print length.

### 3. Simple Practice (30–45 min)

Implement:

1. **Search for value in list**
   ```java
   boolean contains(ListNode head, int target) { ... }
   ```

2. **Get value at index (0-based); return -1 if index too large**
   ```java
   int getAtIndex(ListNode head, int index) { ... }
   ```

**Reflection (10–15 min)**  
Write down:
- How is accessing index `i` in array vs linked list different in complexity?
- Why does a linked list make deletion easier once you already have the node?

---

## Day 2 – Reverse Linked List & Basic LeetCode

**Goal:** Master reversing a linked list and apply basic operations.

### 1. Concept: Reversing a Linked List (20–30 min)

Diagram on paper:

`head -> 1 -> 2 -> 3 -> null`

After reverse:

`3 -> 2 -> 1 -> null`

Key idea:
- Maintain `prev`, `curr`, `next`.
- Iterate while `curr != null`, reverse `curr.next` to point to `prev`.

### 2. Implement Reverse Linked List (45–60 min)

1. **Iterative reverse**
   ```java
   ListNode reverseList(ListNode head) {
       ListNode prev = null;
       ListNode curr = head;
       while (curr != null) {
           ListNode next = curr.next;
           curr.next = prev;
           prev = curr;
           curr = next;
       }
       return prev;
   }
   ```

2. **(Optional) Recursive reverse**
   ```java
   ListNode reverseListRecursive(ListNode head) {
       if (head == null || head.next == null) return head;
       ListNode newHead = reverseListRecursive(head.next);
       head.next.next = head;
       head.next = null;
       return newHead;
   }
   ```

Test:
- Build list `{1,2,3,4,5}`.
- Reverse, then print.

### 3. LeetCode Practice (60–75 min)

1. **Reverse Linked List** (`#206`, Easy)
   - Implement your iterative solution.
   - Time: O(n), Space: O(1).

2. **Remove Linked List Elements** (`#203`, Easy)
   - Remove all nodes equal to `val`.
   - Use dummy head to handle removal of head node cleanly.

3. If time, start:
   - **Middle of the Linked List** (`#876`, Easy)
     - You’ll formally study fast/slow pointers tomorrow, but try to reason:
       - Either count length then go to `len/2`, or
       - Use two pointers (fast: 2 steps, slow: 1 step).

**Reflection (10–15 min)**  
- Did reversing make sense conceptually, or did it feel like pointer juggling?
- Re-draw the reverse algorithm on paper without code.

---

## Day 3 – Fast & Slow Pointers (Middle Node, Cycle Detection)

**Goal:** Learn the fast/slow pointer technique and apply it to classic problems.

### 1. Concept: Fast & Slow Pointers (30–45 min)

Understand patterns:

- **Find middle of list**:
  - `slow` moves 1 step, `fast` moves 2 steps.
  - When `fast` reaches end, `slow` is at middle.

- **Detect cycle** (Floyd’s Cycle Detection):
  - If there’s a cycle, fast and slow will eventually meet.
  - If fast hits null, no cycle.

Draw small examples:
- 5-node list without cycle.
- 5-node list with cycle back to node 2.

### 2. Implement Fast/Slow Functions (45–60 min)

1. **Find middle node**
   ```java
   ListNode middleNode(ListNode head) {
       ListNode slow = head;
       ListNode fast = head;
       while (fast != null && fast.next != null) {
           slow = slow.next;
           fast = fast.next.next;
       }
       return slow;
   }
   ```

2. **Detect cycle in linked list**
   ```java
   boolean hasCycle(ListNode head) {
       ListNode slow = head;
       ListNode fast = head;
       while (fast != null && fast.next != null) {
           slow = slow.next;
           fast = fast.next.next;
           if (slow == fast) return true;
       }
       return false;
   }
   ```

### 3. LeetCode Practice (60–90 min)

1. **Middle of the Linked List** (`#876`, Easy)
   - Implement with fast/slow pointer.

2. **Linked List Cycle** (`#141`, Easy)
   - Implement cycle detection with fast/slow.

3. **Remove Nth Node From End of List** (`#19`, Medium)
   - Use two pointers:
     - Move `fast` n steps ahead.
     - Move both `fast` and `slow` until `fast` hits end.
     - `slow.next` is the node to remove.
   - Use dummy head to handle removing first node.

**Reflection (10–15 min)**  
- How does fast/slow reduce work compared to counting length first?
- Which fast/slow problem felt trickiest and why?

---

## Day 4 – Stack Basics & Classic Stack Problems

**Goal:** Learn how to use stacks in Java and solve bracket-based problems.

### 1. Concept: Stack & Its Use Cases (20–30 min)

- LIFO (Last In, First Out).
- Good for:
  - Parentheses matching.
  - Undo operations.
  - Reversing order.

In Java, prefer `Deque`:

```java
Deque<Character> stack = new ArrayDeque<>();
stack.push('a');     // push to top
char c = stack.pop(); // pop from top
char top = stack.peek(); // look at top
```

### 2. Implement Simple Stack-Based Functions (30–45 min)

1. **Reverse a string using stack**

```java
String reverseWithStack(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    for (char c : s.toCharArray()) {
        stack.push(c);
    }
    StringBuilder sb = new StringBuilder();
    while (!stack.isEmpty()) {
        sb.append(stack.pop());
    }
    return sb.toString();
}
```

2. **Check balanced parentheses (only `()` initially)**

```java
boolean isValidParenthesesSimple(String s) { ... }
```

- Push when you see '('.
- Pop when you see ')', if stack is empty → invalid.

### 3. LeetCode Practice (60–90 min)

1. **Valid Parentheses** (`#20`, Easy)
   - Must handle `()[]{}`.
   - Use stack:
     - Push opening brackets.
     - On closing, check top matches.

2. **Min Stack** (`#155`, Easy/Medium)
   - Design a stack that supports `getMin()` in O(1).
   - Idea:
     - Use two stacks: one for values, one for minimums; or
     - Store pairs (value, currentMin) in one stack.

**Reflection (10–15 min)**  
- When did stack operations feel natural?
- Could `Min Stack` be done with just one stack? (Yes, storing pair/value+min).

---

## Day 5 – Queue & Level-Order Thinking, Plus More Linked List

**Goal:** Learn queue usage and practice more list manipulation.

### 1. Concept: Queue & When to Use It (20–30 min)

- FIFO (First In, First Out).
- Use in:
  - BFS.
  - Task scheduling.
  - Level-order traversal (used next week for trees).

In Java:

```java
Queue<Integer> queue = new ArrayDeque<>();
queue.offer(1);  // add
int x = queue.poll(); // remove head
int head = queue.peek(); // look at head
```

### 2. Simple Queue Exercises (30–45 min)

1. **Simulate a queue of integers**
   - Enqueue {1,2,3} then dequeue and print all.

2. **Implement a stack using two queues** (optional, but good thinking exercise)
   - LeetCode has this as `#225`.

You can also quickly read about:
- `Deque` used as both stack and queue.

### 3. LeetCode Practice – Linked List Variants (60–90 min)

1. **Merge Two Sorted Lists** (`#21`, Easy)
   - Use pointers:
     - `p1` on list1, `p2` on list2.
     - Build merged using a dummy head.

2. **Palindrome Linked List** (`#234`, Easy/Medium)
   - Use:
     - Find middle (fast/slow).
     - Reverse 2nd half.
     - Compare first half and reversed second half.

3. If time: try
   - **Design Linked List** (`#707`, Medium, optional)
     - Implement a linked list class.

**Reflection (10–15 min)**  
- Which part of `Palindrome Linked List` was hardest? (often connecting/reversing halves)
- Does dummy head simplify list manipulations? How?

---

## Day 6 – Mixed Practice: Linked List Patterns + Stack/Queue

**Goal:** Consolidate multiple patterns with more problem practice.

### 1. Quick Recap (20–30 min)

Without coding, summarize in notes:

- **Reverse a linked list**: algorithm steps.
- **Find middle of list**: algorithm steps.
- **Detect cycle**: algorithm steps.
- **Check valid parentheses with stack**: core logic.

### 2. LeetCode Practice – Linked Lists (60–90 min)

Solve or re-solve:

1. **Reverse Linked List** (`#206`, Easy) – from scratch, quickly.
2. **Middle of the Linked List** (`#876`, Easy).
3. **Linked List Cycle** (`#141`, Easy).
4. **Remove Nth Node From End of List** (`#19`, Medium).

If you’re fast, add:

5. **Intersection of Two Linked Lists** (`#160`, Easy)
   - Use two pointers that switch lists when reaching null, or use set.

### 3. LeetCode Practice – Stack/Queue (30–45 min)

Pick one:

- Re-solve **Valid Parentheses** (`#20`).
- Re-solve or refine **Min Stack** (`#155`).

**Reflection (10–15 min)**  
- For each problem, name the **pattern**:
  - fast/slow?
  - pointer manipulation?
  - stack?
- Which do you find more intuitive so far: linked list pointer logic, or stack-based logic?

---

## Day 7 – Review, Integration, and Slight Stretch

**Goal:** Tie the week together and prepare to move into trees next week.

### 1. Concept Review (30–45 min)

Write short answers (2–4 sentences each):

- When do you prefer a **linked list** over an array?
- Explain the **fast/slow pointer technique** in your own words.
- Give two examples where **Stack** is ideal.
- Give two examples where **Queue** is ideal.

Also, quickly rewrite (pseudocode, not full Java) for:

- Reversing a list.
- Detecting a cycle.

### 2. Timed Re-Solves (60–90 min)

Pick 3–4 representative problems, and attempt each within **25–30 min**:

- From Linked Lists:
  - `#206 Reverse Linked List`
  - `#876 Middle of the Linked List`
  - `#141 Linked List Cycle`
  - `#21 Merge Two Sorted Lists`
- From Stack:
  - `#20 Valid Parentheses`
  - `#155 Min Stack` (if you found it tricky)

If you finish early, do an extra easy one or revisit one that felt hardest.

### 3. Stretch Problem (Optional, 30–45 min)

Try one more challenging linked-list problem:

- **Reorder List** (`#143`, Medium)
  - Steps (at high level):
    - Find middle (fast/slow).
    - Reverse second half.
    - Merge two halves alternating nodes.
  - Even partial progress is good for now.

Or:
- Read/discuss solution if you get stuck after ~30–40 minutes.

**Reflection (10–15 min)**  
- Which linked list pattern feels *most* comfortable now?
- Which still feels confusing? Note it; we can target it in future review.

---

## How Week 3 Fits Your Overall Path

By the end of this week, you should:

- Be comfortable implementing and manipulating **singly linked lists** in Java.
- Understand and apply **fast/slow pointers** for middle node and cycle detection.
- Use **stack** and **queue** idiomatically with Java collections.
- Recognize when a **linked list pattern** or **stack pattern** is appropriate in a new problem.

If you want next, I can:

- Build a **Week 4 daily plan** (Binary Search + Sorting), or  
- Provide a **Java “cheat sheet”** for all linked-list patterns we covered (reverse, middle, cycle, merge, remove Nth, palindrome).
