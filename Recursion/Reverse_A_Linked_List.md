---
created: 2026-05-09
revisions:
  - 2026-05-11
  - 2026-05-16
  - 2026-05-24
  - 2026-06-08
---

# Reverse A Linked List

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #recursion [[Recursion]]
  - #pointers [[Pointers]]

---
## Pattern

Pointer Manipulation (Three Pointers) / Recursive Backtracking

---
## Difficulty

Easy | #easy

---

## ⚡ Key Idea (Core Insight)

The list is reversed by changing the `next` pointer of each node to point to its predecessor. To avoid losing the rest of the list during this swap, you must store the reference to the "next" node before breaking the current link.

---

## ⚡ Quick Recall (VERY IMPORTANT)

**Iterative:** `nxt = curr.next`, `curr.next = prev`, `prev = curr`, `curr = nxt`.  
**Recursive:** Reverse the sub-list, then `head.next.next = head` and `head.next = None`.

---

## Approach

### Brute Force
- Traverse the list and store node values in an array or stack.
- Create a new linked list or overwrite existing values in reverse order.
- **Complexity:** Time: O(N), Space: O(N)

### Optimal (Iterative)
- Use three pointers: `prev` (None), `curr` (head), and `nxt` (None).
- Iterate through the list, re-linking `curr.next` to `prev`.
- **Complexity:** Time: O(N), Space: O(1)

### Optimal (Recursive)
- Reach the end of the list (base case).
- As the recursion unwinds, point the next node's `next` back to the current node.
- **Complexity:** Time: O(N), Space: O(N) (due to call stack)

---

## Code (Python)

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseListIterative(self, head: ListNode) -> ListNode:
        prev, curr = None, head
        
        while curr:
            nxt = curr.next     # 1. Save next
            curr.next = prev    # 2. Reverse link
            prev = curr         # 3. Move prev forward
            curr = nxt          # 4. Move curr forward
            
        return prev # New head

    def reverseListRecursive(self, head: ListNode) -> ListNode:
        # Base Case: Empty list or single node
        if not head or not head.next:
            return head
        
        # Reverse the rest of the list
        new_head = self.reverseListRecursive(head.next)
        
        # 1 -> 2 -> 3  => make 2 point to 1
        head.next.next = head
        head.next = None
        
        return new_head
```

---

## Dry Run (Smart Example)

**Input:** `1 -> 2 -> 3 -> None`

| Step | `prev` | `curr` | `nxt` | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| Initial | `None` | `1` | `None` | Starting position. |
| 1 | `1` | `2` | `2` | `1.next` becomes `None`. `prev` moves to `1`. |
| 2 | `2` | `3` | `3` | `2.next` becomes `1`. `prev` moves to `2`. |
| 3 | `3` | `None` | `None` | `3.next` becomes `2`. `prev` moves to `3`. |
| End | `3` | `None` | `None` | `curr` is None, return `prev` (3). |

---

## Edge Cases

- **Empty List (`head = None`):** Should return `None` immediately.
- **Single Node:** Should return the node itself (already "reversed").
- **Two Nodes:** Simplest case to verify if `prev` and `head` transitions are correct.
- **Large List:** Ensure no stack overflow for recursive approach (though usually fine for ~1000 nodes).

---

## Mistakes

- **Losing the Tail:** Forgetting to save `curr.next` before overwriting it.
- **Returning the Wrong Head:** Returning `curr` (which becomes `None`) instead of `prev`.
- **Circular Links:** Forgetting to set `head.next = None` in recursion, leading to infinite loops.
- **Approach Confusion:** Mixing iterative state (like a while loop) inside a recursive function or vice versa.
- **Recursion Base Case:** Not handling the `not head.next` condition, causing a `NoneType` error when trying to access `head.next.next`.

---

## Complexity

- **Time:** O(N) → Every node is visited exactly once.
- **Space:** 
  - Iterative: O(1) → Constant extra space for pointers.
  - Recursive: O(N) → Implicit call stack depth proportional to list length.

---

## Similar Problems

- [Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/) - Medium
- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) - Easy
- [Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/) - Hard
- [Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #linkedlist #top-interview-questions
- [[Linked List]] [[Recursion]] [[Pointers]]
- **Revision Date:** 2026-05-09
- **Problem Link:** [LeetCode - Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-11)
- [ ] Day 7 Revision (2026-05-16)
- [ ] Day 15 Revision (2026-05-24)
- [ ] Day 30 Revision (2026-06-08)
