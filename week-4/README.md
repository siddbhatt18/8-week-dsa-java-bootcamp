# Week 4: Linked Lists - Daily Structured Plan

## 📅 **DAY 1: Linked List Fundamentals & Implementation**

### 🌅 **Morning Session (45 minutes)**
#### Understanding Linked Lists
- **Core Concepts:**
  - Node structure and references
  - Singly vs Doubly vs Circular linked lists
  - Arrays vs Linked Lists tradeoffs
  - Memory representation

#### Node Implementation & Basic Operations:
```java
// Basic Node class
class ListNode {
    int val;
    ListNode next;
    
    ListNode() {}
    
    ListNode(int val) { 
        this.val = val; 
    }
    
    ListNode(int val, ListNode next) { 
        this.val = val; 
        this.next = next; 
    }
}

// Linked List basic operations
class LinkedListBasics {
    // Creating a linked list
    public ListNode createList(int[] values) {
        if (values.length == 0) return null;
        
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;
        
        for (int val : values) {
            current.next = new ListNode(val);
            current = current.next;
        }
        
        return dummy.next;
    }
    
    // Traversing a linked list
    public void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }
    
    // Finding length
    public int getLength(ListNode head) {
        int length = 0;
        ListNode current = head;
        while (current != null) {
            length++;
            current = current.next;
        }
        return length;
    }
    
    // Search for a value
    public boolean contains(ListNode head, int target) {
        ListNode current = head;
        while (current != null) {
            if (current.val == target) {
                return true;
            }
            current = current.next;
        }
        return false;
    }
    
    // Get nth node (0-indexed)
    public ListNode getNthNode(ListNode head, int n) {
        ListNode current = head;
        for (int i = 0; i < n && current != null; i++) {
            current = current.next;
        }
        return current;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Insertion and Deletion Operations
```java
class LinkedListModification {
    // Insert at beginning - O(1)
    public ListNode insertAtHead(ListNode head, int val) {
        ListNode newNode = new ListNode(val);
        newNode.next = head;
        return newNode;
    }
    
    // Insert at end - O(n)
    public ListNode insertAtTail(ListNode head, int val) {
        ListNode newNode = new ListNode(val);
        
        if (head == null) {
            return newNode;
        }
        
        ListNode current = head;
        while (current.next != null) {
            current = current.next;
        }
        current.next = newNode;
        
        return head;
    }
    
    // Insert at position
    public ListNode insertAtPosition(ListNode head, int val, int position) {
        if (position == 0) {
            return insertAtHead(head, val);
        }
        
        ListNode current = head;
        for (int i = 0; i < position - 1 && current != null; i++) {
            current = current.next;
        }
        
        if (current == null) {
            return head; // Position out of bounds
        }
        
        ListNode newNode = new ListNode(val);
        newNode.next = current.next;
        current.next = newNode;
        
        return head;
    }
    
    // Delete from beginning - O(1)
    public ListNode deleteFromHead(ListNode head) {
        if (head == null) return null;
        return head.next;
    }
    
    // Delete from end - O(n)
    public ListNode deleteFromTail(ListNode head) {
        if (head == null || head.next == null) {
            return null;
        }
        
        ListNode current = head;
        while (current.next.next != null) {
            current = current.next;
        }
        current.next = null;
        
        return head;
    }
    
    // Delete by value
    public ListNode deleteByValue(ListNode head, int val) {
        if (head == null) return null;
        
        if (head.val == val) {
            return head.next;
        }
        
        ListNode current = head;
        while (current.next != null && current.next.val != val) {
            current = current.next;
        }
        
        if (current.next != null) {
            current.next = current.next.next;
        }
        
        return head;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Dummy Node Pattern
```java
// Understanding the power of dummy nodes
class DummyNodePattern {
    // Without dummy node - complex edge cases
    public ListNode removeElementsNoDummy(ListNode head, int val) {
        // Handle head changes
        while (head != null && head.val == val) {
            head = head.next;
        }
        
        if (head == null) return null;
        
        ListNode current = head;
        while (current.next != null) {
            if (current.next.val == val) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }
        
        return head;
    }
    
    // With dummy node - cleaner code
    public ListNode removeElementsWithDummy(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode current = dummy;
        while (current.next != null) {
            if (current.next.val == val) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }
        
        return dummy.next;
    }
}
```

### 📝 **Day 1 Checklist**
- [ ] Understand node structure and references
- [ ] Implement basic traversal operations
- [ ] Master insertion at head/tail/position
- [ ] Master deletion operations
- [ ] Understand dummy node advantages

---

## 📅 **DAY 2: Linked List Reversal Techniques**

### 🌅 **Morning Session (45 minutes)**
#### Iterative Reversal
```java
class LinkedListReversal {
    // Basic iterative reversal
    public ListNode reverseListIterative(ListNode head) {
        ListNode prev = null;
        ListNode current = head;
        
        while (current != null) {
            ListNode nextTemp = current.next;  // Store next
            current.next = prev;               // Reverse pointer
            prev = current;                    // Move prev forward
            current = nextTemp;                // Move current forward
        }
        
        return prev;
    }
    
    // Reversal with visualization
    public ListNode reverseWithSteps(ListNode head) {
        /*
        Initial: 1 -> 2 -> 3 -> 4 -> null
        Step 1:  null <- 1    2 -> 3 -> 4 -> null
        Step 2:  null <- 1 <- 2    3 -> 4 -> null
        Step 3:  null <- 1 <- 2 <- 3    4 -> null
        Step 4:  null <- 1 <- 2 <- 3 <- 4
        */
        
        ListNode prev = null;
        ListNode current = head;
        
        while (current != null) {
            System.out.println("Reversing node: " + current.val);
            ListNode nextTemp = current.next;
            current.next = prev;
            prev = current;
            current = nextTemp;
        }
        
        return prev;
    }
    
    // Reverse first K nodes
    public ListNode reverseFirstK(ListNode head, int k) {
        if (head == null || k <= 1) return head;
        
        ListNode prev = null;
        ListNode current = head;
        ListNode nextTemp = null;
        
        int count = 0;
        while (current != null && count < k) {
            nextTemp = current.next;
            current.next = prev;
            prev = current;
            current = nextTemp;
            count++;
        }
        
        // Connect remaining list
        if (head != null) {
            head.next = current;
        }
        
        return prev;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Recursive Reversal
```java
class RecursiveReversal {
    // Basic recursive reversal
    public ListNode reverseListRecursive(ListNode head) {
        // Base case
        if (head == null || head.next == null) {
            return head;
        }
        
        // Recursive case
        ListNode reversedList = reverseListRecursive(head.next);
        head.next.next = head;
        head.next = null;
        
        return reversedList;
    }
    
    // Recursive reversal with explanation
    public ListNode reverseRecursiveExplained(ListNode head) {
        /*
        Call stack for list 1->2->3->null:
        
        reverseList(1)
          reverseList(2)
            reverseList(3)
              return 3 (base case)
            3.next = 2, 2.next = null
            return 3
          2.next = 1, 1.next = null  
          return 3
        return 3
        
        Result: 3->2->1->null
        */
        
        if (head == null || head.next == null) {
            System.out.println("Base case reached: " + 
                             (head == null ? "null" : head.val));
            return head;
        }
        
        System.out.println("Processing node: " + head.val);
        ListNode reversedList = reverseListRecursive(head.next);
        
        System.out.println("Reversing connection for: " + head.val);
        head.next.next = head;
        head.next = null;
        
        return reversedList;
    }
    
    // Reverse between positions
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if (head == null || left == right) return head;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        
        // Move to node before left position
        for (int i = 1; i < left; i++) {
            prev = prev.next;
        }
        
        // Reverse the sublist
        ListNode current = prev.next;
        for (int i = left; i < right; i++) {
            ListNode nextNode = current.next;
            current.next = nextNode.next;
            nextNode.next = prev.next;
            prev.next = nextNode;
        }
        
        return dummy.next;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
  - Implement both iterative and recursive solutions
- **Bonus:** [92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)

### 📝 **Day 2 Checklist**
- [ ] Master iterative reversal with three pointers
- [ ] Understand recursive reversal logic
- [ ] Implement partial list reversal
- [ ] Complete Reverse Linked List (both ways)
- [ ] Understand space complexity differences

---

## 📅 **DAY 3: Fast and Slow Pointer Pattern**

### 🌅 **Morning Session (45 minutes)**
#### Floyd's Tortoise and Hare Algorithm
```java
class FastSlowPointers {
    // Find middle of linked list
    public ListNode findMiddle(ListNode head) {
        if (head == null) return null;
        
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;      // Move 1 step
            fast = fast.next.next;  // Move 2 steps
        }
        
        return slow;  // Middle node
    }
    
    // Find middle (first of two middle nodes for even length)
    public ListNode findMiddleFirstOfTwo(ListNode head) {
        if (head == null) return null;
        
        ListNode slow = head;
        ListNode fast = head.next;  // Start fast one ahead
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
    }
    
    // Detect cycle in linked list
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        
        ListNode slow = head;
        ListNode fast = head.next;
        
        while (slow != fast) {
            if (fast == null || fast.next == null) {
                return false;  // No cycle
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return true;  // Cycle detected
    }
    
    // Find cycle start node
    public ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null) {
            return null;
        }
        
        // Phase 1: Detect if cycle exists
        ListNode slow = head;
        ListNode fast = head;
        boolean hasCycle = false;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                hasCycle = true;
                break;
            }
        }
        
        if (!hasCycle) return null;
        
        // Phase 2: Find cycle start
        slow = head;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        
        return slow;  // Cycle start node
    }
    
    // Find cycle length
    public int getCycleLength(ListNode head) {
        ListNode cycleStart = detectCycle(head);
        if (cycleStart == null) return 0;
        
        int length = 1;
        ListNode current = cycleStart.next;
        while (current != cycleStart) {
            length++;
            current = current.next;
        }
        
        return length;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Advanced Fast-Slow Applications
```java
class AdvancedFastSlow {
    // Check if linked list is palindrome
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        
        // Find middle using fast-slow
        ListNode slow = head;
        ListNode fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        // Reverse second half
        ListNode secondHalf = reverseList(slow.next);
        
        // Compare first and second half
        ListNode p1 = head;
        ListNode p2 = secondHalf;
        boolean isPalin = true;
        
        while (p2 != null) {
            if (p1.val != p2.val) {
                isPalin = false;
                break;
            }
            p1 = p1.next;
            p2 = p2.next;
        }
        
        // Restore list (optional)
        slow.next = reverseList(secondHalf);
        
        return isPalin;
    }
    
    private ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode current = head;
        
        while (current != null) {
            ListNode next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        
        return prev;
    }
    
    // Find nth node from end
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode fast = dummy;
        ListNode slow = dummy;
        
        // Move fast n+1 steps ahead
        for (int i = 0; i <= n; i++) {
            fast = fast.next;
        }
        
        // Move both pointers until fast reaches end
        while (fast != null) {
            slow = slow.next;
            fast = fast.next;
        }
        
        // Skip the nth node from end
        slow.next = slow.next.next;
        
        return dummy.next;
    }
    
    // Reorder list: L0→L1→…→Ln-1→Ln to L0→Ln→L1→Ln-1→L2→Ln-2→…
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) return;
        
        // Find middle
        ListNode slow = head;
        ListNode fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        // Reverse second half
        ListNode second = reverseList(slow.next);
        slow.next = null;
        
        // Merge two lists
        ListNode first = head;
        while (second != null) {
            ListNode temp1 = first.next;
            ListNode temp2 = second.next;
            
            first.next = second;
            second.next = temp1;
            
            first = temp1;
            second = temp2;
        }
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
- **Then:** [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

### 📝 **Day 3 Checklist**
- [ ] Master fast-slow pointer technique
- [ ] Understand cycle detection algorithm
- [ ] Implement finding middle node
- [ ] Complete cycle detection problem
- [ ] Solve palindrome linked list

---

## 📅 **DAY 4: Merge and Sort Operations**

### 🌅 **Morning Session (45 minutes)**
#### Merging Linked Lists
```java
class MergeOperations {
    // Merge two sorted lists
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;
        
        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                current.next = l1;
                l1 = l1.next;
            } else {
                current.next = l2;
                l2 = l2.next;
            }
            current = current.next;
        }
        
        // Attach remaining nodes
        current.next = (l1 != null) ? l1 : l2;
        
        return dummy.next;
    }
    
    // Merge two sorted lists recursively
    public ListNode mergeTwoListsRecursive(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        
        if (l1.val <= l2.val) {
            l1.next = mergeTwoListsRecursive(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoListsRecursive(l1, l2.next);
            return l2;
        }
    }
    
    // Merge K sorted lists - Divide and Conquer
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        
        return mergeHelper(lists, 0, lists.length - 1);
    }
    
    private ListNode mergeHelper(ListNode[] lists, int start, int end) {
        if (start == end) {
            return lists[start];
        }
        
        int mid = start + (end - start) / 2;
        ListNode left = mergeHelper(lists, start, mid);
        ListNode right = mergeHelper(lists, mid + 1, end);
        
        return mergeTwoLists(left, right);
    }
    
    // Merge K sorted lists - Priority Queue
    public ListNode mergeKListsPQ(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;
        
        PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);
        
        // Add all heads to priority queue
        for (ListNode head : lists) {
            if (head != null) {
                pq.offer(head);
            }
        }
        
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;
        
        while (!pq.isEmpty()) {
            ListNode smallest = pq.poll();
            current.next = smallest;
            current = current.next;
            
            if (smallest.next != null) {
                pq.offer(smallest.next);
            }
        }
        
        return dummy.next;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Sorting Linked Lists
```java
class SortOperations {
    // Merge sort for linked list
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        // Find middle using fast-slow
        ListNode mid = getMid(head);
        ListNode rightHead = mid.next;
        mid.next = null;
        
        // Recursively sort both halves
        ListNode left = sortList(head);
        ListNode right = sortList(rightHead);
        
        // Merge sorted halves
        return merge(left, right);
    }
    
    private ListNode getMid(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
    }
    
    private ListNode merge(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;
        
        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                current.next = l1;
                l1 = l1.next;
            } else {
                current.next = l2;
                l2 = l2.next;
            }
            current = current.next;
        }
        
        current.next = (l1 != null) ? l1 : l2;
        return dummy.next;
    }
    
    // Insertion sort for linked list
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        ListNode current = head;
        
        while (current != null) {
            ListNode next = current.next;
            
            // Find insertion position
            ListNode prev = dummy;
            while (prev.next != null && prev.next.val < current.val) {
                prev = prev.next;
            }
            
            // Insert current node
            current.next = prev.next;
            prev.next = current;
            
            current = next;
        }
        
        return dummy.next;
    }
    
    // Partition list around value x
    public ListNode partition(ListNode head, int x) {
        ListNode beforeHead = new ListNode(0);
        ListNode before = beforeHead;
        ListNode afterHead = new ListNode(0);
        ListNode after = afterHead;
        
        while (head != null) {
            if (head.val < x) {
                before.next = head;
                before = before.next;
            } else {
                after.next = head;
                after = after.next;
            }
            head = head.next;
        }
        
        after.next = null;
        before.next = afterHead.next;
        
        return beforeHead.next;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
- **Challenge:** [148. Sort List](https://leetcode.com/problems/sort-list/)

### 📝 **Day 4 Checklist**
- [ ] Master merging two sorted lists
- [ ] Understand merge k lists approaches
- [ ] Implement merge sort for linked list
- [ ] Complete merge two sorted lists
- [ ] Attempt sort list problem

---

## 📅 **DAY 5: Complex Linked List Problems**

### 🌅 **Morning Session (45 minutes)**
#### Advanced List Manipulations
```java
class ComplexOperations {
    // Copy list with random pointer
    class Node {
        int val;
        Node next;
        Node random;
        
        public Node(int val) {
            this.val = val;
            this.next = null;
            this.random = null;
        }
    }
    
    // Approach 1: Using HashMap
    public Node copyRandomList(Node head) {
        if (head == null) return null;
        
        HashMap<Node, Node> map = new HashMap<>();
        
        // First pass: create all nodes
        Node current = head;
        while (current != null) {
            map.put(current, new Node(current.val));
            current = current.next;
        }
        
        // Second pass: connect pointers
        current = head;
        while (current != null) {
            Node copy = map.get(current);
            copy.next = map.get(current.next);
            copy.random = map.get(current.random);
            current = current.next;
        }
        
        return map.get(head);
    }
    
    // Approach 2: Interweaving nodes (O(1) space)
    public Node copyRandomListOptimal(Node head) {
        if (head == null) return null;
        
        // Step 1: Create copy nodes and interweave
        Node current = head;
        while (current != null) {
            Node copy = new Node(current.val);
            copy.next = current.next;
            current.next = copy;
            current = copy.next;
        }
        
        // Step 2: Set random pointers
        current = head;
        while (current != null) {
            if (current.random != null) {
                current.next.random = current.random.next;
            }
            current = current.next.next;
        }
        
        // Step 3: Separate lists
        Node dummy = new Node(0);
        Node copyPrev = dummy;
        current = head;
        
        while (current != null) {
            Node copy = current.next;
            current.next = copy.next;
            copyPrev.next = copy;
            
            copyPrev = copy;
            current = current.next;
        }
        
        return dummy.next;
    }
    
    // Add two numbers represented as linked lists
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;
        int carry = 0;
        
        while (l1 != null || l2 != null || carry != 0) {
            int val1 = (l1 != null) ? l1.val : 0;
            int val2 = (l2 != null) ? l2.val : 0;
            
            int sum = val1 + val2 + carry;
            carry = sum / 10;
            
            current.next = new ListNode(sum % 10);
            current = current.next;
            
            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }
        
        return dummy.next;
    }
    
    // Add two numbers II (most significant digit first)
    public ListNode addTwoNumbersII(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<>();
        Stack<Integer> s2 = new Stack<>();
        
        // Push all digits to stacks
        while (l1 != null) {
            s1.push(l1.val);
            l1 = l1.next;
        }
        while (l2 != null) {
            s2.push(l2.val);
            l2 = l2.next;
        }
        
        ListNode head = null;
        int carry = 0;
        
        while (!s1.isEmpty() || !s2.isEmpty() || carry != 0) {
            int val1 = s1.isEmpty() ? 0 : s1.pop();
            int val2 = s2.isEmpty() ? 0 : s2.pop();
            
            int sum = val1 + val2 + carry;
            carry = sum / 10;
            
            ListNode node = new ListNode(sum % 10);
            node.next = head;
            head = node;
        }
        
        return head;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### List Rotation and Swapping
```java
class RotationSwapping {
    // Rotate list to the right by k places
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null || k == 0) {
            return head;
        }
        
        // Find length and tail
        ListNode tail = head;
        int length = 1;
        while (tail.next != null) {
            tail = tail.next;
            length++;
        }
        
        // Connect tail to head (make circular)
        tail.next = head;
        
        // Find new tail (length - k % length - 1)
        k = k % length;
        int stepsToNewTail = length - k;
        ListNode newTail = head;
        
        for (int i = 1; i < stepsToNewTail; i++) {
            newTail = newTail.next;
        }
        
        ListNode newHead = newTail.next;
        newTail.next = null;
        
        return newHead;
    }
    
    // Swap nodes in pairs
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        
        while (prev.next != null && prev.next.next != null) {
            ListNode first = prev.next;
            ListNode second = prev.next.next;
            
            // Swap
            first.next = second.next;
            second.next = first;
            prev.next = second;
            
            // Move to next pair
            prev = first;
        }
        
        return dummy.next;
    }
    
    // Reverse nodes in k-group
    public ListNode reverseKGroup(ListNode head, int k) {
        // Check if we have k nodes
        ListNode current = head;
        int count = 0;
        while (current != null && count < k) {
            current = current.next;
            count++;
        }
        
        if (count < k) return head;
        
        // Reverse k nodes
        current = head;
        ListNode prev = null;
        ListNode next = null;
        count = 0;
        
        while (count < k) {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
            count++;
        }
        
        // Recursively process remaining list
        if (next != null) {
            head.next = reverseKGroup(next, k);
        }
        
        return prev;
    }
    
    // Remove duplicates from sorted list
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) return null;
        
        ListNode current = head;
        while (current.next != null) {
            if (current.val == current.next.val) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }
        
        return head;
    }
    
    // Remove all duplicates (keep only unique)
    public ListNode deleteDuplicatesII(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode prev = dummy;
        while (head != null) {
            if (head.next != null && head.val == head.next.val) {
                int dupVal = head.val;
                while (head != null && head.val == dupVal) {
                    head = head.next;
                }
                prev.next = head;
            } else {
                prev = prev.next;
                head = head.next;
            }
        }
        
        return dummy.next;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
- **Challenge:** [143. Reorder List](https://leetcode.com/problems/reorder-list/)

### 📝 **Day 5 Checklist**
- [ ] Master deep copy with random pointer
- [ ] Implement add two numbers variations
- [ ] Understand list rotation logic
- [ ] Complete remove nth from end
- [ ] Solve reorder list problem

---

## 📅 **DAY 6: Practice & Pattern Recognition**

### 🌅 **Morning Session (60 minutes)**
#### Comprehensive Pattern Review
```java
// LINKED LIST PATTERNS SUMMARY

class LinkedListPatterns {
    // PATTERN 1: Dummy Node
    // Use when: head might change, cleaner edge cases
    public ListNode patternDummy(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        // Operations...
        return dummy.next;
    }
    
    // PATTERN 2: Fast-Slow Pointers
    // Use when: finding middle, cycle detection, kth from end
    public void patternFastSlow(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
    }
    
    // PATTERN 3: Previous-Current-Next
    // Use when: reversing, deleting, inserting
    public void patternThreePointers(ListNode head) {
        ListNode prev = null;
        ListNode current = head;
        while (current != null) {
            ListNode next = current.next;
            // Operations with prev, current, next
            prev = current;
            current = next;
        }
    }
    
    // PATTERN 4: Recursion
    // Use when: elegant solution needed, stack space available
    public ListNode patternRecursion(ListNode head) {
        if (head == null || head.next == null) {
            return head;  // Base case
        }
        ListNode result = patternRecursion(head.next);
        // Process current node
        return result;
    }
    
    // PATTERN 5: Multiple Pass
    // Use when: need list length, preprocessing required
    public void patternMultiplePass(ListNode head) {
        // First pass: gather information
        int length = 0;
        ListNode current = head;
        while (current != null) {
            length++;
            current = current.next;
        }
        
        // Second pass: use information
        current = head;
        for (int i = 0; i < length / 2; i++) {
            current = current.next;
        }
    }
}
```

### 🌞 **Afternoon Session (90 minutes)**
#### Problem-Solving Marathon
**Solve these independently:**

```java
// 1. Find intersection of two linked lists
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    // Your implementation
    // Hint: Use length difference or two-pointer cycle
}

// 2. Odd even linked list
public ListNode oddEvenList(ListNode head) {
    // Your implementation
    // Group odd indices together followed by even indices
}

// 3. Split linked list in parts
public ListNode[] splitListToParts(ListNode head, int k) {
    // Your implementation
    // Split list into k parts of equal size (or as equal as possible)
}

// 4. Flatten a multilevel doubly linked list
public Node flatten(Node head) {
    // Your implementation
    // Use recursion or stack
}
```

### 🌙 **Evening Session (45 minutes)**
#### LeetCode Challenge Problems
- **Complete these problems:**
  1. [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)
  2. [328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/)
  3. [725. Split Linked List in Parts](https://leetcode.com/problems/split-linked-list-in-parts/)

### 📝 **Day 6 Checklist**
- [ ] Review all five core patterns
- [ ] Complete intersection problem
- [ ] Solve odd even list
- [ ] Implement split list in parts
- [ ] Identify personal weak areas

---

## 📅 **DAY 7: Week Review & Advanced Challenges**

### 🌅 **Morning Session (60 minutes)**
#### Knowledge Assessment Quiz
```java
// SELF-ASSESSMENT QUESTIONS

/*
1. Time & Space Complexity
What's the complexity of:
- Reversing a linked list iteratively: Time O(?), Space O(?)
- Reversing a linked list recursively: Time O(?), Space O(?)
- Finding middle with fast-slow: Time O(?), Space O(?)
- Merge sort on linked list: Time O(?), Space O(?)

2. Debug this code:
*/
public ListNode removeElements(ListNode head, int val) {
    while (head != null && head.val == val) {
        head = head.next;
    }
    ListNode current = head;
    while (current.next != null) {  // Bug?
        if (current.next.val == val) {
            current.next = current.next.next;
        }
        current = current.next;  // Bug?
    }
    return head;
}

/*
3. Choose the best approach:
Problem: Check if linked list has a palindrome
a) Copy to array and check
b) Reverse entire list and compare
c) Find middle, reverse second half, compare
d) Use stack for all elements

4. Memory leak scenario:
When can memory leaks occur with linked lists in Java?

5. Why use dummy node?
List 3 specific scenarios where dummy node simplifies code
*/
```

### 🌞 **Afternoon Session (90 minutes)**
#### Advanced Challenge Problems
```java
class AdvancedChallenges {
    // LRU Cache implementation
    class LRUCache {
        class DNode {
            int key, value;
            DNode prev, next;
            DNode(int k, int v) {
                key = k;
                value = v;
            }
        }
        
        private HashMap<Integer, DNode> map;
        private DNode head, tail;
        private int capacity;
        
        public LRUCache(int capacity) {
            this.capacity = capacity;
            map = new HashMap<>();
            head = new DNode(0, 0);
            tail = new DNode(0, 0);
            head.next = tail;
            tail.prev = head;
        }
        
        public int get(int key) {
            if (!map.containsKey(key)) return -1;
            
            DNode node = map.get(key);
            removeNode(node);
            addToHead(node);
            return node.value;
        }
        
        public void put(int key, int value) {
            if (map.containsKey(key)) {
                DNode node = map.get(key);
                node.value = value;
                removeNode(node);
                addToHead(node);
            } else {
                if (map.size() >= capacity) {
                    DNode lru = tail.prev;
                    removeNode(lru);
                    map.remove(lru.key);
                }
                DNode newNode = new DNode(key, value);
                map.put(key, newNode);
                addToHead(newNode);
            }
        }
        
        private void removeNode(DNode node) {
            node.prev.next = node.next;
            node.next.prev = node.prev;
        }
        
        private void addToHead(DNode node) {
            node.next = head.next;
            node.prev = head;
            head.next.prev = node;
            head.next = node;
        }
    }
    
    // Design browser history
    class BrowserHistory {
        class Page {
            String url;
            Page prev, next;
            Page(String url) {
                this.url = url;
            }
        }
        
        private Page current;
        
        public BrowserHistory(String homepage) {
            current = new Page(homepage);
        }
        
        public void visit(String url) {
            Page newPage = new Page(url);
            current.next = newPage;
            newPage.prev = current;
            current = newPage;
        }
        
        public String back(int steps) {
            while (steps > 0 && current.prev != null) {
                current = current.prev;
                steps--;
            }
            return current.url;
        }
        
        public String forward(int steps) {
            while (steps > 0 && current.next != null) {
                current = current.next;
                steps--;
            }
            return current.url;
        }
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Week 4 Complete Reference
```java
// WEEK 4 MASTERY CHECKLIST

/* ========== ESSENTIAL OPERATIONS ========== */
// 1. Traversal: while (node != null)
// 2. Insertion: newNode.next = current.next; current.next = newNode
// 3. Deletion: current.next = current.next.next
// 4. Reversal: prev = null, current = head, reverse pointers
// 5. Merge: dummy node + comparison

/* ========== KEY PATTERNS ========== */
// 1. DUMMY NODE
//    - Simplifies edge cases
//    - Head modifications
//    - Merging lists

// 2. FAST-SLOW POINTERS
//    - Find middle: fast = 2x speed
//    - Detect cycle: meet = cycle exists
//    - Kth from end: gap of k nodes

// 3. RECURSION
//    - Elegant reversal
//    - Tree-like operations
//    - Watch stack space

// 4. MULTIPLE POINTERS
//    - Previous-Current-Next for reversal
//    - Partition operations
//    - In-place modifications

/* ========== PROBLEM TYPES ========== */
// Basic: Reverse, merge, delete, insert
// Intermediate: Cycle, palindrome, reorder
// Advanced: Deep copy, LRU cache, k-group operations

/* ========== COMPLEXITY ANALYSIS ========== */
// Most operations: O(n) time
// With recursion: O(n) space (call stack)
// With HashMap: O(n) extra space
// Sorting: O(n log n) time

/* ========== COMMON MISTAKES ========== */
// 1. NullPointerException - always check null
// 2. Lost reference - save next before modifying
// 3. Infinite loop - ensure pointer advancement
// 4. Off-by-one - careful with counting
// 5. Memory leak - circular references (rare in Java)

/* ========== INTERVIEW TIPS ========== */
// 1. Draw the list and pointer movements
// 2. Handle edge cases (null, single node)
// 3. Consider dummy node for cleaner code
// 4. Think about multiple passes if needed
// 5. Ask about modifying original list
```

### 📝 **Day 7 Final Checklist**
- [ ] Score at least 4/5 on assessment quiz
- [ ] Complete all Week 4 core problems
- [ ] Implement LRU Cache or similar design
- [ ] Create comprehensive notes
- [ ] Ready for Week 5: Binary Trees

---

## 🎯 **End of Week 4 Milestones**

### You Should Now Be Able To:
✅ Implement all basic linked list operations  
✅ Apply fast-slow pointer technique confidently  
✅ Reverse lists (iteratively and recursively)  
✅ Detect and handle cycles  
✅ Merge and sort linked lists  
✅ Solve medium/hard linked list problems  

### Problems Completed (Minimum):
- ✅ Reverse Linked List
- ✅ Merge Two Sorted Lists
- ✅ Linked List Cycle
- ✅ Remove Nth Node From End
- ✅ Palindrome Linked List
- ✅ Reorder List
- ✅ Sort List (attempted)

### Core Skills Developed:
1. **Pointer Manipulation** - Managing references
2. **Pattern Recognition** - Identifying approach quickly
3. **Edge Case Handling** - Null, single node, etc.
4. **Space Optimization** - In-place operations
5. **Recursion Application** - When and how to use

### Prepare for Week 5:
- Trees build on linked list concepts
- Node references similar to ListNode
- Recursion heavily used in trees
- Review recursion basics if needed

## 💪 **Week 4 Reflection Questions**
1. What's the most challenging aspect of linked lists?
2. Which pattern (dummy/fast-slow/recursion) is most useful?
3. How do linked lists compare to arrays in your mind?
4. What problem gave you the deepest understanding?
5. How confident are you with pointer manipulation now?

## 🎉 **Excellent Progress!**
Linked Lists are fundamental to understanding more complex data structures like trees and graphs. Your mastery of pointer manipulation, fast-slow techniques, and recursive thinking will directly transfer to tree problems next week. The ability to visualize and manipulate references is a crucial skill that separates strong programmers from beginners. You've built a solid foundation - keep up the momentum!
