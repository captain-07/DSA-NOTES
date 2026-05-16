---
created: 2026-05-17
revisions:
  - 2026-05-19
  - 2026-05-24
  - 2026-06-01
  - 2026-06-16
---

# Delete The Middle Node In Ll

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #Google #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #twopointers [[Two Pointers]]
  - #fastandslowpointers [[Fast and Slow Pointers]]

## Pattern

Fast and Slow Pointers (Tortoise and Hare)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

To delete a node, you must reach the **node preceding it**. By initializing the `fast` pointer two steps ahead of `slow` (or using a `prev` pointer), `slow` will land on the node exactly before the middle when `fast` reaches the end of the list.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Handle the single-node case first (`return None`). Initialize `slow = head` and `fast = head.next.next`. Move `slow` by 1 and `fast` by 2 until `fast` hits the end. `slow.next` is now the target.

---

## Approach

### Brute Force
- Count total nodes ($N$) in the first pass. 
- Traverse again to the $(N/2 - 1)$-th node.
- **Complexity:** $O(N)$ time (two passes), $O(1)$ space.

### Optimal
- Use **Two Pointers**. 
- If the list has only one node, return `None`.
- Initialize `slow` at `head` and `fast` at `head.next.next`.
- While `fast` and `fast.next` exist:
    - `slow = slow.next`
    - `fast = fast.next.next`
- `slow.next = slow.next.next` (deletes the middle node).
- **Complexity:** $O(N)$ time (single pass), $O(1)$ space.

---

## Code (Python)

```python
class Solution:
    def deleteMiddle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # Edge case: list has only one node
        if not head or not head.next:
            return None
        
        # Initialize slow at head and fast two steps ahead
        # This ensures slow stops at (middle - 1)
        slow = head
        fast = head.next.next
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        
        # slow is now the node BEFORE the middle node
        slow.next = slow.next.next
        
        return head
```

---

## Dry Run (Smart Example)

**Input:** `[1, 3, 4, 7, 1, 2, 6]` (Length = 7, Middle index = 3, Value = 7)

| Step | slow (val) | fast (val) | Explanation |
| :--- | :--- | :--- | :--- |
| Init | 1 | 4 | `slow=head`, `fast=head.next.next` |
| 1 | 3 | 1 | `slow` moves to 3, `fast` moves to 1 |
| 2 | 4 | 6 | `slow` moves to 4, `fast` moves to 6 |
| End | 4 | 6 | `fast.next` is None, loop terminates |
| Del | 4 | 6 | `slow.next` (7) is skipped. `4.next` becomes `1`. |

**Result:** `[1, 3, 4, 1, 2, 6]`

---

## Edge Cases

- **Single Node:** `[1]` → Middle is index 0. Return `None`.
- **Two Nodes:** `[1, 2]` → Middle is index 1. `slow` stays at `head`, `slow.next = None`. Return `[1]`.
- **Even Length:** `[1, 2, 3, 4]` → Middle is index 2 (value 3). `slow` should stop at 2.
- **Already Empty:** Return `None`.

---

## Mistakes

- **User Mistake:** Starting with `fast = head.next.next` and `slow = head` without checking if `head.next` exists (leads to AttributeError).
- **Parity Error:** Getting the middle index wrong for even-length lists ($n/2$ vs $n/2 - 1$).
- **Memory Leak:** In languages like C++, forgetting to free the deleted node's memory.
- **Off-by-one:** Stopping `slow` exactly at the middle node instead of the node before it.

---

## Complexity

Time: $O(N)$ → Single traversal of the linked list.  
Space: $O(1)$ → No extra data structures used; only pointers.

---

## Similar Problems

- [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) - Easy
- [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) - Medium
- [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) - Easy
- [Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #linkedlist #fastandslow
- [[Linked List]] [[Two Pointers]]
- **Revision Date:** May 17, 2026
- **Problem Link:** [LeetCode - Delete the Middle Node of a Linked List](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-19)
- [ ] Day 7 Revision (2026-05-24)
- [ ] Day 15 Revision (2026-06-01)
- [ ] Day 30 Revision (2026-06-16)
