---
created: 2026-05-27
revisions:
  - 2026-05-29
  - 2026-06-03
  - 2026-06-11
  - 2026-06-26
---

# Sort A Linked List Of 0'S 1'S And 2'S

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #Flipkart #MakeMyTrip #Qualcomm

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #sorting [[Sorting]]
  - #pointers [[Two Pointers]]

## Pattern

Dummy Nodes + Linked List Partitioning  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Create three separate dummy nodes to act as heads for lists of 0s, 1s, and 2s. Traverse the original list once, appending each node to its corresponding dummy list, then concatenate the three lists in order.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use 3 Dummy Heads (Zero, One, Two) → Partition in 1 pass → Link: `Zero.next = One` and `One.next = Two`.

---

## Approach

### Brute Force
- Count frequencies of 0s, 1s, and 2s in one pass.
- In a second pass, overwrite node values based on counts.
- **Time:** O(N), **Space:** O(1) (but involves data replacement).

### Better
- *Not applicable* (The counting approach is usually considered the "Better" approach in terms of simplicity, but "Optimal" for constraints where data modification is allowed).

### Optimal (No Data Replacement)
1. Initialize three dummy nodes: `zeroHead`, `oneHead`, `twoHead`.
2. Use three pointers (`zero`, `one`, `two`) to track the tail of each list.
3. Traverse the list: if `val == 0`, attach to `zero.next`; if `1`, to `one.next`; else `two.next`.
4. Connect `zeroTail.next` to `oneHead.next` (if exists, else `twoHead.next`).
5. Connect `oneTail.next` to `twoHead.next`.
6. Ensure `twoTail.next = None` to avoid cycles.

---

## Code (Python)

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        
        # Dummy nodes to start three independent lists
        zero_head = ListNode(-1)
        one_head = ListNode(-1)
        two_head = ListNode(-1)
        
        # Tails for the three lists
        zero = zero_head
        one = one_head
        two = two_head
        
        curr = head
        while curr:
            if curr.val == 0:
                zero.next = curr
                zero = zero.next
            elif curr.val == 1:
                one.next = curr
                one = one.next
            else:
                two.next = curr
                two = two.next
            curr = curr.next
            
        # Linking the lists: Zero -> One -> Two
        # Handle case where 1s might be missing
        one.next = two_head.next
        zero.next = one_head.next if one_head.next else two_head.next
        two.next = None # Important to terminate the list
        
        return zero_head.next
```

---

## Dry Run (Smart Example)

**Input:** `1 -> 2 -> 0 -> 1`

| Step | Current Val | Lists State | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 1 | `One: 1` | Node 1 attached to One dummy. |
| 2 | 2 | `Two: 2` | Node 2 attached to Two dummy. |
| 3 | 0 | `Zero: 0` | Node 0 attached to Zero dummy. |
| 4 | 1 | `One: 1 -> 1` | Second 1 attached to One list. |
| End | - | `0 -> 1 -> 1 -> 2` | Linked Zero Tail to One Head, One Tail to Two Head. |

---

## Edge Cases

- **Empty List:** `head is None` → return `None`.
- **Single Element:** Return `head`.
- **Missing Numbers:** No 0s, no 1s, or no 2s (handled by `one_head.next` logic).
- **All Same Values:** `0 -> 0 -> 0` correctly populates only one dummy list.

---

## Mistakes

- **Forgetting to terminate:** Not setting `two.next = None` leading to infinite loops/cycles.
- **Incorrect Linking:** Directly linking to dummy nodes instead of `dummy.next`.
- **Data Replacement:** Interviewers often forbid changing `node.val`; ensure you move pointers.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** O(N) → Single traversal of the list.
- **Space:** O(1) → Only three dummy nodes and a few pointers used (no extra storage for N elements).

---

## Similar Problems

- [Sort Colors (Arrays)](https://leetcode.com/problems/sort-colors/) - Medium
- [Partition List](https://leetcode.com/problems/partition-list/) - Medium
- [Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/) - Medium

---

## Tags and Properties
- #dsa #important #revisit
- #linkedlist [[Linked List]]
- #sorting [[Sorting]]
- **Revision Date:** 2026-05-27
- **Problem Link:** [Sort List of 0s, 1s and 2s - GeeksforGeeks](https://www.geeksforgeeks.org/problems/given-a-linked-list-of-0s-1s-and-2s-sort-it/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-29)
- [ ] Day 7 Revision (2026-06-03)
- [ ] Day 15 Revision (2026-06-11)
- [ ] Day 30 Revision (2026-06-26)
