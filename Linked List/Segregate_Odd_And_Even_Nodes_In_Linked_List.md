---
created: 2026-05-15
revisions:
  - 2026-05-17
  - 2026-05-22
  - 2026-05-30
  - 2026-06-14
---

# Segregate Odd And Even Nodes In Linked List

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Facebook #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #twopointers [[Two Pointers]]
  - #inplace [[In-place Manipulation]]

## Pattern

Two Pointers (Parallel Traversal)  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Maintain two separate chains—one for nodes at odd indices and one for even indices—by re-linking `next` pointers in a single pass. The tail of the odd list must eventually point to the head of the even list.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use `odd` and `even` pointers. In each step: `odd.next = even.next`, then move `odd`; `even.next = odd.next`, then move `even`. Finally, `odd.next = even_head`.

---

## Approach

### Brute Force
- Traverse the list and store values in an array. Create a new list by first picking odd-indexed values then even-indexed values.
- **Time:** O(N)
- **Space:** O(N)

### Optimal
- Use two pointers `odd` (starting at `head`) and `even` (starting at `head.next`).
- Save `even_head = even` to reconnect the lists later.
- Loop while `even` and `even.next` exist to safely jump pointers.
- Re-link pointers: `odd.next = odd.next.next` (which is `even.next`) and `even.next = even.next.next`.
- **Time:** O(N)
- **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def oddEvenList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # Edge case: Empty or single node list
        if not head or not head.next:
            return head
        
        # Initialize pointers
        odd = head
        even = head.next
        # Save the start of the even list to connect later
        even_head = even 
        
        # Traverse until the end of the list
        while even and even.next:
            # Connect current odd to next odd (skipping the even node)
            odd.next = even.next
            odd = odd.next
            
            # Connect current even to next even (skipping the odd node)
            even.next = odd.next
            even = even.next
            
        # Append even list to the end of odd list
        odd.next = even_head
        
        return head
```

---

## Dry Run (Smart Example)

**Input:** `[2, 1, 3, 5, 6, 4]`

| Step | Pointers (Odd, Even) | Action | Resulting Links |
| :--- | :--- | :--- | :--- |
| Init | `odd=2`, `even=1` | `even_head = 1` | `2 -> 1 -> 3 -> 5 -> 6 -> 4` |
| 1 | `odd=3`, `even=5` | `2.next=3`, `1.next=5` | `2 -> 3`, `1 -> 5` |
| 2 | `odd=6`, `even=4` | `3.next=6`, `5.next=4` | `3 -> 6`, `5 -> 4` |
| End | `even.next` is `None` | `6.next = even_head(1)` | `2 -> 3 -> 6 -> 1 -> 5 -> 4` |

---

## Edge Cases

- **Empty List (`[]`):** Return `None` immediately.
- **Single Node (`[1]`):** Return `head` (already segregated).
- **Two Nodes (`[1, 2]`):** Pointers initialize and loop doesn't run; returns `1 -> 2`.
- **Odd/Even length lists:** Handled by the `while even and even.next` condition.

---

## Mistakes

- **Incorrect Loop Condition:** Using `while odd and odd.next` (even pointer moves faster, so it must be the boundary check).
- **Losing even_head:** Forgetting to store the reference to the first even node before moving the `even` pointer.
- **Null Pointer Access:** **User Mistake:** Saving `even_head = head.next` before checking if `head` is null. This leads to `AttributeError: 'NoneType' object has no attribute 'next'`.
- **Broken Chain:** Forgetting to set the last even node's `next` to `None` (usually handled automatically by the loop logic but worth verifying).

---

## Complexity

Time: O(N) → Each node is visited exactly once.  
Space: O(1) → Only a few pointers are used regardless of input size.

---

## Similar Problems

- [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) - Easy
- [Split Linked List in Parts](https://leetcode.com/problems/split-linked-list-in-parts/) - Medium
- [Reorder List](https://leetcode.com/problems/reorder-list/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #linkedlist #twopointers #inplace
  - [[Linked List]] [[Two Pointers]]
  - **Revision Date:** 2026-05-15
  - **Problem Link:** [LeetCode - Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/)

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-17)
- [ ] Day 7 Revision (2026-05-22)
- [ ] Day 15 Revision (2026-05-30)
- [ ] Day 30 Revision (2026-06-14)
