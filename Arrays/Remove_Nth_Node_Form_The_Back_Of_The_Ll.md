---
created: 2026-05-15
revisions:
  - 2026-05-17
  - 2026-05-22
  - 2026-05-30
  - 2026-06-14
---

# Remove Nth Node From The End Of The List

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #twopointers [[Two Pointers]]
  - #dummy-node [[Dummy Node]]

---
## Pattern

Two Pointers (Fast & Slow)  
Dummy Node Technique  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

To delete the $N^{th}$ node from the end in one pass, create a gap of $N$ nodes between two pointers. When the `fast` pointer reaches the end, the `slow` pointer will be exactly at the node **preceding** the target node.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Move `fast` pointer $N$ steps ahead. Then move `fast` and `slow` together until `fast` reaches the last node. Use a **Dummy Node** to handle cases where the head itself needs to be removed.

---

## Approach

### Brute Force
- Two passes: First pass to count the total length $L$. Second pass to move $L-N$ steps from the head to find the preceding node.
- **Time:** $O(L + (L-N)) \approx O(2L)$
- **Space:** $O(1)$

### Optimal (One Pass)
1. Initialize a `dummy` node pointing to `head`.
2. Set `fast` and `slow` pointers at `dummy`.
3. Advance `fast` pointer $N$ steps ahead.
4. Move both `fast` and `slow` one step at a time until `fast.next` is `None`.
5. `slow.next` is now the node to be deleted. Update `slow.next = slow.next.next`.
6. Return `dummy.next`.

---

## Code (Python)

```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        # Dummy node handles edge case: removing the head node
        dummy = ListNode(0, head)
        slow = fast = dummy
        
        # 1. Create the gap of N between slow and fast
        for _ in range(n):
            fast = fast.next
            
        # 2. Move both until fast reaches the last node
        while fast.next:
            slow = slow.next
            fast = fast.next
            
        # 3. Delete the Nth node from end
        slow.next = slow.next.next
        
        return dummy.next
```

---

## Dry Run (Smart Example)

**Input:** `head = [1, 2, 3, 4, 5], n = 2`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Init | `slow=D, fast=D` | Dummy (D) points to 1. |
| Gap | `fast` moves 2 steps | `fast` is at node (2). `slow` is at D. |
| Loop 1 | `slow=1, fast=3` | Both move 1 step. |
| Loop 2 | `slow=2, fast=4` | Both move 1 step. |
| Loop 3 | `slow=3, fast=5` | `fast.next` is None. Stop. |
| Delete | `3.next = 5` | Node (4) is skipped. |

---

## Edge Cases

- **N = List Length:** Removing the head node (Dummy node solves this).
- **Single Node List (N=1):** Returns an empty list.
- **N = 1:** Removing the tail node.
- **List with 2 nodes, N=2:** Removing the first node.

---

## Mistakes

- **User Mistake:** No specific note provided (Initial documentation gap).
- **Off-by-one:** Stopping `fast` at `None` instead of the last node (requires careful pointer handling).
- **Null Pointer:** Forgetting to check `fast.next` if not using a dummy node.
- **Not using Dummy:** Makes deleting the head node a messy special `if` case.

---

## Complexity

Time: O(L) → Single traversal of the list where L is the number of nodes.  
Space: O(1) → Only two pointers and a dummy node used regardless of list size.

---

## Similar Problems

- [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) - Easy
- [Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/) - Medium
- [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) - Easy
- [Rotate List](https://leetcode.com/problems/rotate-list/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #linkedlist #twopointers #leetcode-medium  
  - [[Linked List]] [[Two Pointers]]
  - **Revision Date:** 2026-05-15
  - **Problem Link:** [LeetCode - Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-17)
- [ ] Day 7 Revision (2026-05-22)
- [ ] Day 15 Revision (2026-05-30)
- [ ] Day 30 Revision (2026-06-14)
