---
created: 2026-05-27
revisions:
  - 2026-05-29
  - 2026-06-03
  - 2026-06-11
  - 2026-06-26
---

# Add Two Numbers In Linked List

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Meta #Apple #Adobe #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #math [[Math]]
  - #simulation [[Simulation]]

## Pattern

Linked List Traversal + Math Simulation (Carry Logic)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Simulate elementary school addition digit-by-digit from head to tail. Since lists are already reversed (Least Significant Digit first), we process them linearly while maintaining a `carry` variable.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use a **Dummy Head** to build the result list and a **while loop** that runs as long as `l1`, `l2`, **OR** `carry` exists.

---

## Approach

### Brute Force
- Convert both linked lists to integers, add them, and convert the sum back to a linked list.
- **Time:** $O(N + M)$
- **Constraint:** Fails for very large numbers (Integer Overflow).

### Optimal
1. Initialize a `dummy` node and a `curr` pointer.
2. Initialize `carry = 0`.
3. Loop while `l1`, `l2`, or `carry` is non-zero:
   - Extract values (default to 0 if list is exhausted).
   - `total = val1 + val2 + carry`.
   - `carry = total // 10`.
   - Create new node with `total % 10`.
4. Return `dummy.next`.
- **Time:** $O(\max(N, M))$
- **Space:** $O(\max(N, M))$ (for result list)

---

## Code (Python)

```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0)
        curr = dummy
        carry = 0
        
        # Continue if lists aren't empty OR if there's a leftover carry
        while l1 or l2 or carry:
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0
            
            # Calculate sum and carry
            total = val1 + val2 + carry
            carry = total // 10
            new_val = total % 10
            
            # Update result list
            curr.next = ListNode(new_val)
            curr = curr.next
            
            # Move input pointers
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
            
        return dummy.next
```

---

## Dry Run (Smart Example)

**Input:** `l1 = [9, 9]`, `l2 = [1]` (Represents 99 + 1 = 100)

| Step | l1.val | l2.val | Carry | Total | Result Node | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 9 | 1 | 0 | 10 | 0 | Carry becomes 1 |
| 2 | 9 | 0 | 1 | 10 | 0 | Carry stays 1; l1 ends |
| 3 | 0 | 0 | 1 | 1 | 1 | Remaining carry handled |
| **End** | - | - | 0 | - | **[0, 0, 1]** | Final list: 100 |

---

## Edge Cases

- **Unequal Lengths:** One list finishes before the other (handled by `val = l.val if l else 0`).
- **Final Carry:** The last addition results in a carry (handled by `while ... or carry`).
- **All Nines:** `[9, 9]` + `[1]` results in a longer list.
- **Single Zero:** `[0]` + `[0]` = `[0]`.

---

## Mistakes

- **Final Carry:** Forgetting to create a new node for the last carry after the lists are exhausted.
- **Null Pointer:** Accessing `.val` on a `None` node.
- **User Mistake:** No specific note provided. (Ensure carry logic is reviewed).

---

## Complexity

Time: $O(\max(N, M))$ → We traverse each node of the longer list exactly once.  
Space: $O(\max(N, M))$ → The length of the new list is at most $\max(N, M) + 1$.

---

## Similar Problems

- [Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/) - Medium (Numbers NOT reversed)
- [Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/) - Medium
- [Add Strings](https://leetcode.com/problems/add-strings/) - Easy
- [Plus One](https://leetcode.com/problems/plus-one/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #simulation
  - #linkedlist [[Linked List]]
  - #math [[Math]]
  - **Revision Date:** 2026-05-27
  - **Problem Link:** [LeetCode - Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-29)
- [ ] Day 7 Revision (2026-06-03)
- [ ] Day 15 Revision (2026-06-11)
- [ ] Day 30 Revision (2026-06-26)
