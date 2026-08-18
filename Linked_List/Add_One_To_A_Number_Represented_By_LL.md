---
created: 2026-05-27
revisions:
  - 2026-05-29
  - 2026-06-03
  - 2026-06-11
  - 2026-06-26
---

# Add One To A Number Represented By LL

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Flipkart #Accolite #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]], #recursion [[Recursion]], #pointers [[Pointers]]

## Pattern

Reverse and Add  
Backtracking (Recursion)  
Sentinel Node (Last Non-Nine)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The challenge is carry propagation from right to left in a singly linked list. The **Optimal** insight is to find the **rightmost node that is not 9**. Incrementing this node and setting all subsequent nodes to 0 correctly handles the "plus one" logic in a single pass without reversing the list.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the **last non-9 node**. Increment it, set all following nodes to 0. If all are 9s, add a new `1` at the head.

---

## Approach

### Brute Force
- Convert LL to an integer, add 1, then convert back to LL.
- **Complexity:** O(N) time, but fails due to **Integer Overflow** for long lists.

### Better (Reverse-Add-Reverse)
- 1. Reverse the list to bring LSD (Least Significant Digit) to the front.
- 2. Iterate and add 1 with carry logic.
- 3. Reverse the list again to restore order.
- **Complexity:** O(N) time (3 passes), O(1) space.

### Optimal (Sentinel / Last Non-Nine)
- 1. Create a `dummy` node (value 0) pointing to `head` (handles 999 -> 1000 case).
- 2. Track `last_not_nine` node during a single traversal.
- 3. Increment `last_not_nine.val` by 1.
- 4. Set all `val` of nodes after `last_not_nine` to 0.
- **Complexity:** O(N) time (1 pass), O(1) space.

---

## Code (Python)

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def addOne(self, head: ListNode) -> ListNode:
        # Step 1: Sentinel node to handle carry-out at the head (e.g., 99 -> 100)
        dummy = ListNode(0)
        dummy.next = head
        
        last_not_nine = dummy
        curr = head
        
        # Step 2: Traverse to find the rightmost node that isn't a 9
        while curr:
            if curr.val != 9:
                last_not_nine = curr
            curr = curr.next
            
        # Step 3: Increment the last non-9 node
        last_not_nine.val += 1
        
        # Step 4: All subsequent nodes must become 0
        curr = last_not_nine.next
        while curr:
            curr.val = 0
            curr = curr.next
            
        # If dummy was incremented (case 999 -> 1000), return dummy, else head
        return dummy if dummy.val == 1 else dummy.next
```

---

## Dry Run (Smart Example)

**Input:** `1 -> 2 -> 9 -> 9`

| Step | Node Checked | `last_not_nine` | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `dummy(0)` | `dummy(0)` | Initialization |
| 2 | `1` | `node(1)` | 1 != 9, update pointer |
| 3 | `2` | `node(2)` | 2 != 9, update pointer |
| 4 | `9` | `node(2)` | 9 == 9, skip update |
| 5 | `9` | `node(2)` | 9 == 9, skip update |
| 6 | Increment | `node(3)` | `last_not_nine.val` becomes 3 |
| 7 | Zeroing | `1 -> 3 -> 0 -> 0` | Set all nodes after `node(3)` to 0 |

**Result:** `1 -> 3 -> 0 -> 0`

---

## Edge Cases

- **All 9s (e.g., 9 -> 9):** Requires adding a new node at the start (1 -> 0 -> 0).
- **Single Digit < 9 (e.g., 5):** Simply becomes 6.
- **Single Digit 9:** Becomes 1 -> 0.
- **Trailing 9s (e.g., 1 -> 8 -> 9):** Correctly increments 8 to 9 and 9 to 0.

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Overflow:** Forgetting that converting LL to `int` will fail for very large numbers.
- **Carry Propagation:** Forgetting to handle the final carry that might require a new head node.
- **In-place vs. New List:** Not clarifying if the original list can be modified.

---

## Complexity

Time: O(N) → Single pass traversal to find the node.  
Space: O(1) → Constant extra space (only pointers used).

---

## Similar Problems

- [Plus One](https://leetcode.com/problems/plus-one/) - Easy
- [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/) - Medium
- [Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/) - Medium
- [Multiply Strings](https://leetcode.com/problems/multiply-strings/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #linkedlist #sentinel  
  - [[Linked List]] [[Recursion]] [[Sentinel Node]]
  - **Revision Date:** 2026-05-27
  - **Problem Link:** [Plus One Linked List - LeetCode](https://leetcode.com/problems/plus-one-linked-list/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-29)
- [ ] Day 7 Revision (2026-06-03)
- [ ] Day 15 Revision (2026-06-11)
- [ ] Day 30 Revision (2026-06-26)
