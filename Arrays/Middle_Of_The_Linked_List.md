---
created: 2026-05-09
revisions:
  - 2026-05-11
  - 2026-05-16
  - 2026-05-24
  - 2026-06-08
---

# Middle Of The Linked List

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Facebook #Qualcomm

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #twopointers [[Two Pointers]]
  - #fastandslow [[Fast and Slow Pointers]]

## Pattern

Fast and Slow Pointers (Tortoise and Hare)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Use two pointers starting at the head. Move the **slow** pointer by **one** step and the **fast** pointer by **two** steps. When the fast pointer reaches the end (`None` or last node), the slow pointer will be at the middle.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Fast moves twice as fast as Slow; when Fast finishes the race (distance $D$), Slow has covered $D/2$.

---

## Approach

### Brute Force
- Traverse the list once to count total nodes ($N$).
- Traverse a second time to the $N/2$-th node.
- **Time:** $O(N + N/2) = O(N)$
- **Space:** $O(1)$

### Optimal
- Use the **Tortoise and Hare** algorithm.
- Loop until `fast` reaches the end.
- Returning `slow` handles both even and odd lengths automatically (returning the second middle for even lengths).
- **Time:** $O(N)$ (Single pass)
- **Space:** $O(1)$

---

## Code (Python)

```python
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # Initialize both pointers at the start
        slow = fast = head
        
        # Fast moves 2 steps, Slow moves 1 step
        # Must check both fast and fast.next to avoid AttributeError
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
        return slow
```

---

## Dry Run (Smart Example)

**Input:** `[1, 2, 3, 4, 5, 6]` (Even length, should return node `4`)

| Step | Slow Value | Fast Value | Explanation |
| :--- | :--- | :--- | :--- |
| 0 | 1 | 1 | Initialization at head. |
| 1 | 2 | 3 | Slow+1, Fast+2. `fast.next` is not None. |
| 2 | 3 | 5 | Slow+1, Fast+2. `fast.next` is not None. |
| 3 | 4 | None | Slow+1, Fast+2. `fast` is now None, loop breaks. |

**Result:** Returns node with value `4`.

---

## Edge Cases

- **Single Node:** `[1]` -> Loop doesn't run, returns head (`1`).
- **Two Nodes:** `[1, 2]` -> Loop runs once, returns `2` (second middle).
- **Odd Length:** `[1, 2, 3]` -> Returns `2`.
- **Empty List:** `[]` -> Returns `None`.

---

## Mistakes

- **While Condition Logic:** Forgetting to check **both** `fast` and `fast.next` leads to `AttributeError` on `fast.next.next` when `fast` is the last node or null.
- **Null Initialization:** Initializing pointers to `None` instead of `head`.
- **Even/Odd Confusion:** Overthinking whether to return `slow` or `slow.next`. Standard `while fast and fast.next` correctly yields the second middle node for even lengths.

---

## Complexity

Time: $O(N)$ → We traverse the list exactly once.  
Space: $O(1)$ → We only use two pointer variables regardless of list size.

---

## Similar Problems

- [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) - Easy
- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) - Easy
- [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) - Medium
- [Reorder List](https://leetcode.com/problems/reorder-list/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #tortoiseandhare #pointers 
  - [[Two Pointers]] [[Linked List]]
  - **Revision Date:** 2026-05-09
  - **Problem Link:** [LeetCode 876 - Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-11)
- [ ] Day 7 Revision (2026-05-16)
- [ ] Day 15 Revision (2026-05-24)
- [ ] Day 30 Revision (2026-06-08)
