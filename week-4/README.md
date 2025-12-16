Here is your **Day 1–Day 7 plan for Week 4**, focused on:

- Stacks & Queues (including typical LeetCode uses)
- Linked Lists (implementation + key patterns)

Assume ~2–3 hours per day; adjust as needed.

---

## Day 1 – Stack & Queue Fundamentals in Java

**Goals:**
- Understand the concepts and Java implementations of stack & queue.
- Implement basic operations and see where they’re used.

### 1. Concept Primer (20–30 min)

Understand:

- **Stack** (LIFO – last in, first out)
  - Operations: `push`, `pop`, `peek`
  - Use cases: parentheses validation, undo, DFS, backtracking.
- **Queue** (FIFO – first in, first out)
  - Operations: `offer/add`, `poll/remove`, `peek`
  - Use cases: BFS, scheduling tasks, streaming data.

In Java (preferred modern usage):
- Stack:
  - `Deque<Integer> stack = new ArrayDeque<>();`
  - `stack.push(x)`, `stack.pop()`, `stack.peek()`.
- Queue:
  - `Queue<Integer> queue = new ArrayDeque<>();`
  - `queue.offer(x)`, `queue.poll()`, `queue.peek()`.

### 2. Basic Stack Practice (45–60 min)

Create class: `week4.day1.StackBasics`.

**Exercises:**

1. Implement a method to reverse an array using a stack:
   ```java
   public static int[] reverseWithStack(int[] arr) {
       Deque<Integer> stack = new ArrayDeque<>();
       for (int x : arr) stack.push(x);
       int i = 0;
       while (!stack.isEmpty()) {
           arr[i++] = stack.pop();
       }
       return arr;
   }
   ```

2. Convert a decimal number to binary using a stack:
   - Push remainders of division by 2.
   - Pop to build binary string.

3. Implement `boolean isBalancedParentheses(String s)` with a stack:
   - Only `(` and `)` to start.
   - Push `(`, pop on `)`, check correctness.

### 3. Basic Queue Practice (30–45 min)

Create class: `week4.day1.QueueBasics`.

**Exercises:**

1. Simulate simple queue usage:
   - Enqueue integers 1–5.
   - Dequeue all and print in order.
2. Implement a method that:
   - Takes an `int[] arr`
   - Enqueues all elements
   - Dequeues and prints them one by one.

---

## Day 2 – LeetCode Stacks: Valid Parentheses & Min Stack

**Goals:**
- Use a stack to solve classic bracket problems.
- Implement a stack with extra functionality.

### 1. LeetCode: Valid Parentheses (20, Easy) (45–60 min)

Create: `week4.day2.LC20ValidParentheses`.

**Approach:**
- Use `Deque<Character> stack = new ArrayDeque<>();`
- For each char `c`:
  - If opening bracket `(`, `{`, `[`: push.
  - If closing: check if stack not empty and top matches; else return false.
- At the end, stack must be empty.

**Concepts reinforced:**
- Mapping opening ↔ closing brackets.
- Typical stack for syntax checking.

### 2. LeetCode: Min Stack (155, Easy) (60–75 min)

Create: `week4.day2.LC155MinStack`.

Requirements:
- `push(x)`, `pop()`, `top()`, `getMin()` all O(1).

**Approach:**
- Use two stacks:
  - `stack`: actual values
  - `minStack`: track current min at each level
- On `push(x)`:
  - `stack.push(x)`
  - `minStack.push(min(x, minStack.peek()))` (or push x if empty)
- On `pop()`:
  - Pop from both.

**Concepts reinforced:**
- Keeping auxiliary information in parallel stack.
- Design of data structures.

### 3. Quick Review (15–20 min)

- Summarize for yourself:
  - When to consider a stack?
  - Difference between `Stack` class vs `Deque` (prefer `Deque`).

---

## Day 3 – Monotonic Stack: Daily Temperatures

**Goals:**
- Learn the monotonic stack pattern.
- Solve an important Medium stack problem.

### 1. Concept Primer: Monotonic Stack (20–30 min)

Monotonic stack:
- Stack that keeps elements in increasing or decreasing order.
- Common use: “next greater element”, “next smaller element”.

Pattern:
- Iterate indices:
  - While stack not empty and current element is “greater than” element at top index:
    - Pop index, compute result for that index.
  - Push current index.

### 2. LeetCode: Daily Temperatures (739, Medium) (60–90 min)

Create: `week4.day3.LC739DailyTemperatures`.

**Problem:**
- Given temperatures, for each day find how many days until a warmer temp (or 0 if none).

**Approach (monotonic decreasing stack of indices):**
- `int n = temperatures.length;`
- `int[] ans = new int[n];`
- `Deque<Integer> stack = new ArrayDeque<>();` // stores indices
- For `i` from 0 to n-1:
  - While stack not empty and `temperatures[i] > temperatures[stack.peek()]`:
    - `int idx = stack.pop();`
    - `ans[idx] = i - idx;`
  - Push current index `i`.

Concepts reinforced:
- Monotonic stack (storing indices).
- Using stack to store candidates for future comparisons.

### 3. Optional: Next Greater Element I (496, Easy) (30–45 min)

If time allows, create: `week4.day3.LC496NextGreaterElement`.

- Similar pattern to Daily Temperatures, but simpler.

---

## Day 4 – Linked List Fundamentals: Node, Traversal, Insert, Delete

**Goals:**
- Understand singly-linked list structure.
- Implement basic operations manually.

### 1. Concept Primer (20–30 min)

Singly-linked list:
```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}
```

- Head node reference.
- No random access by index; must traverse.
- Insert/delete involves pointer changes.

### 2. Implement Basic List Operations (60–75 min)

Create: `week4.day4.LinkedListBasics`.

Define `ListNode` and write methods:

1. `ListNode insertAtHead(ListNode head, int val)`
2. `ListNode insertAtTail(ListNode head, int val)`
   - Traverse to end, attach new node.
3. `void printList(ListNode head)`
4. `ListNode deleteFirstOccurrence(ListNode head, int target)`
   - Handle deletion at head carefully (head may change).
   - Otherwise track `prev` and `curr`.

Test:
- Build a list from array `{1, 2, 3}` using `insertAtTail`.
- Print, delete a value, print again.

### 3. Two-Pointer Concept on Linked Lists (15–20 min)

Understand “fast/slow pointers”:
- `slow` moves 1 step at a time.
- `fast` moves 2 steps.
- Used to:
  - Find middle of list.
  - Detect cycles (later).

No need to code yet; just get intuition.

---

## Day 5 – Fundamental Linked List LeetCode Problems

**Goals:**
- Reverse a singly-linked list.
- Merge two sorted linked lists.
- Practice pointer manipulation.

### 1. LeetCode: Reverse Linked List (206, Easy) (45–60 min)

Create: `week4.day5.LC206ReverseLinkedList`.

Iterative approach:

```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode nextTemp = curr.next;
        curr.next = prev;
        prev = curr;
        curr = nextTemp;
    }
    return prev;
}
```

Concepts reinforced:
- Pointer juggling: `prev`, `curr`, `next`.
- Reversing links one by one.

### 2. LeetCode: Merge Two Sorted Lists (21, Easy) (45–60 min)

Create: `week4.day5.LC21MergeTwoSortedLists`.

**Approach:**
- Use dummy head:
  ```java
  ListNode dummy = new ListNode(-1);
  ListNode tail = dummy;
  ```
- While both lists not null:
  - Attach smaller node to `tail.next`.
  - Move tail, move that list.
- Attach remaining nodes if one list ends.

Concepts reinforced:
- Dummy head pattern (avoids head edge-case).
- Working with multiple list pointers.

### 3. Optional: LeetCode – Remove Linked List Elements (203, Easy) (30–45 min)

Create: `week4.day5.LC203RemoveElements`.

- Use dummy head:
  - `dummy.next = head;`
  - Traverse with `prev` and `curr`, skip nodes where `curr.val == val`.

---

## Day 6 – Two-Pointer Linked List Problems: Cycles & Nth from End

**Goals:**
- Use fast/slow pointers.
- Solve core linked list patterns.

### 1. LeetCode: Linked List Cycle (141, Easy) (45–60 min)

Create: `week4.day6.LC141LinkedListCycle`.

**Approach:**
- Fast/slow pointers:
  - `slow = head`, `fast = head`.
  - While `fast != null && fast.next != null`:
    - `slow = slow.next;`
    - `fast = fast.next.next;`
    - If `slow == fast` → cycle exists.
- If loop finishes, no cycle.

Concepts reinforced:
- Fast/slow pattern.
- Using pointer equality to detect cycles.

### 2. LeetCode: Remove Nth Node From End of List (19, Medium) (60–75 min)

Create: `week4.day6.LC19RemoveNthFromEnd`.

**Approach (two pointers + dummy):**
- Dummy head: `dummy.next = head`.
- `first = dummy`, `second = dummy`.
- Move `first` `n+1` steps ahead.
- Move both one step at a time until `first` hits null.
- Now `second` is right before node to remove:
  - `second.next = second.next.next;`
- Return `dummy.next`.

Concepts reinforced:
- Offsetting pointers.
- Handling head removals cleanly via dummy.

### 3. Optional: Middle of the Linked List (876, Easy) (30–45 min)

Create: `week4.day6.LC876MiddleOfLinkedList`.

- Fast/slow to find middle:
  - When `fast` reaches end, `slow` is at middle.

---

## Day 7 – Integration, Review, and Independent Practice

**Goals:**
- Consolidate stack/queue and linked list concepts.
- Practice re-solving core problems from memory.

### 1. Quick Written Review (20–30 min)

Without IDE or notes, write (on paper or text file):

1. `ListNode` definition.
2. Pseudocode for:
   - Reversing a linked list.
   - Detecting a cycle with fast/slow.
3. Stack/queue snippet:
   - Create stack via `Deque<Integer>`.
   - Create queue via `Queue<Integer>`.

Then compare with your existing code.

### 2. Re-solve Core Problems From Scratch (60–90 min)

In **new files**, attempt these without copying code:

1. **Valid Parentheses (20, Easy)** – stack
2. **Min Stack (155, Easy)** – design + stacks
3. **Reverse Linked List (206, Easy)**
4. **Merge Two Sorted Lists (21, Easy)**
5. **Linked List Cycle (141, Easy)**
6. **Remove Nth Node From End of List (19, Medium)** (stretch if time)

For each:
- Spend up to ~25–30 minutes thinking before checking any hint.
- After solving, write:
  - Pattern used (stack / fast-slow / dummy node).
  - Time complexity (usually O(n)).
  - Space complexity (usually O(1), except for auxiliary stacks).

### 3. Reflection & Prep for Week 5 (15–30 min)

Ask yourself:

1. Do I feel comfortable:
   - Creating and traversing a linked list?
   - Reversing and merging lists?
   - Using fast/slow pointers?
2. Can I recognize:
   - Problems that scream “stack” (e.g., parentheses, next greater element)?
   - Problems that scream “linked list + two pointers”?

Note down:
- Any problems you found confusing.
- Any pointer bugs you hit frequently (e.g., forgetting to move `curr`, mishandling head).

This will help reinforce these in **Week 5**, where you’ll move on to:

- Trees & Binary Search Trees
- DFS/BFS on trees (which will use your queue knowledge)
- Recursive thinking on tree structures.

If you want next, I can:
- Generate a similar **7‑day plan for Week 5 (Trees & BSTs)**, or
- Provide a **Linked List + Stack/Queue cheat sheet** with templates and common pitfalls.
