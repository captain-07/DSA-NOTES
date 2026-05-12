---
created: 2026-05-12
revisions:
  - 2026-05-14
  - 2026-05-19
  - 2026-05-27
  - 2026-06-11
---

# Linked Cycle Ii

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Adobe #Bloomberg #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #twopointers [[Two Pointers]]
  - #floydscycle [[Floyd's Cycle-Finding Algorithm]]

---
## Pattern

Two Pointers (Slow & Fast) + Mathematical Offset

---
## Difficulty

Medium  
#medium

---
## ⚡ Key Idea (Core Insight)

1.  **Intersection:** Use Slow and Fast pointers to detect a cycle.
2.  **Mathematical Equilibrium:** If $L_1$ is the distance from `head` to `entry`, and $L_2$ is from `entry` to `meeting point`, then $L_1$ is mathematically equivalent to the distance from `meeting point` to `entry` (modulo cycle length).
3.  **Phase 2:** Reset one pointer to `head`, keep the other at the `meeting point`. Move both at speed 1; they meet at the cycle start.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Find meeting point $\rightarrow$ Reset `slow` to `head` $\rightarrow$ Move both at same speed $\rightarrow$ Meeting point is the answer.

---
## Approach

### Brute Force
- Use a **HashSet** to store node references while traversing.
- Return the first node already present in the set.
- **Complexity:** Time $O(N)$, Space $O(N)$.

### Optimal (Floyd's Algorithm)
1.  Initialize `slow` and `fast` at `head`.
2.  Move `slow` by 1 step, `fast` by 2 steps.
3.  If they meet, a cycle exists.
4.  Reset `slow` to `head`. Move `slow` and `fast` 1 step at a time.
5.  The node where they meet is the start of the cycle.
- **Complexity:** Time $O(N)$, Space $O(1)$.

---
## Code (Python)

```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return None
        
        slow, fast = head, head
        
        # Phase 1: Finding the intersection point
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
            if slow == fast:
                # Phase 2: Finding the entry point
                slow = head
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
                
        return None
```

---
## Dry Run (Smart Example)

**Input:** `head = [3,2,0,-4]`, pos = 1 (Cycle at node 2)

| Step | Slow Pointer (Value) | Fast Pointer (Value) | Explanation |
| :--- | :--- | :--- | :--- |
| 0 | 3 (Head) | 3 (Head) | Initialization |
| 1 | 2 | 0 | Fast moves 2x |
| 2 | 0 | 2 | Fast wraps around cycle |
| 3 | -4 | -4 | **Intersection Found!** |
| 4 | 3 (Reset) | -4 (Keep) | Reset Slow to Head |
| 5 | 2 | 2 | **Meet at Cycle Entry!** |

---
## Edge Cases

- **No Cycle:** `fast` or `fast.next` becomes `None`.
- **Single Node Cycle:** Node points to itself.
- **Entire List is Cycle:** Tail points to `head`.
- **Empty List:** `head` is `None`.

---
## Mistakes

- **Null Checks:** Forgetting to check `fast` and `fast.next` before moving.
- **User Mistake (The Proof):** Why is $L_1 = \text{Dist}(\text{Meeting} \to \text{Entry})$?
  - Let $L_1$ = distance from head to entry.
  - Let $L_2$ = distance from entry to meeting point.
  - Let $C$ = cycle length.
  - Slow distance = $L_1 + L_2$.
  - Fast distance = $L_1 + L_2 + nC$ (where $n$ is loops).
  - Since $Fast = 2 \times Slow$: $L_1 + L_2 + nC = 2(L_1 + L_2)$.
  - Simplify: $nC = L_1 + L_2 \rightarrow \mathbf{L_1 = nC - L_2}$.
  - This proves $L_1$ is equal to the remaining distance in the cycle from the meeting point.

---
## Complexity

Time: O(N) → Linear traversal of the list.  
Space: O(1) → Only two pointers used.

---
## Similar Problems

- [Linked List Cycle I](https://leetcode.com/problems/linked-list-cycle/) - Easy
- [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) - Medium
- [Circular Array Loop](https://leetcode.com/problems/circular-array-loop/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #linkedlist #top-interview-questions
- [[Linked List]] [[Two Pointers]]
- **Problem Link:** [LeetCode - Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-14)
- [ ] Day 7 Revision (2026-05-19)
- [ ] Day 15 Revision (2026-05-27)
- [ ] Day 30 Revision (2026-06-11)
