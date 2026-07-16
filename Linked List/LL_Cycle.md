---
created: 2026-05-10
revisions:
  - 2026-05-12
  - 2026-05-17
  - 2026-05-25
  - 2026-06-09
---

# Linked List Cycle

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Apple #Adobe #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #twopointers [[Two Pointers]]
  - #hashmap [[HashMap]]

---
## Pattern

Two Pointers (Fast & Slow) / Floyd’s Cycle-Finding Algorithm

---
## Difficulty

Easy | #easy

---

## ⚡ Key Idea (Core Insight)

Use two pointers moving at different speeds. If a cycle exists, the **Fast pointer** (moving 2 steps) will eventually "lap" the **Slow pointer** (moving 1 step) and they will meet at the same node. If Fast reaches `None`, no cycle exists.

---

## ⚡ Quick Recall (VERY IMPORTANT)

**Tortoise and Hare:** Slow moves 1, Fast moves 2. If `slow == fast`, return `True`.

---

## Approach

### Brute Force
- Iterate through the list and keep track of a maximum node count (e.g., 10,001 if constraints say max nodes = 10k). If you exceed it, a cycle exists.
- **Time:** O(N) | **Space:** O(1)

### Better (Hash Set)
- Traverse the list and store each **node reference** in a Hash Set. Before moving to the next node, check if the current node is already in the set.
- **Time:** O(N) | **Space:** O(N)

### Optimal (Floyd’s Cycle-Finding)
1. Initialize `slow` and `fast` pointers at `head`.
2. Loop while `fast` and `fast.next` are not `None`.
3. Move `slow` by 1 step: `slow = slow.next`.
4. Move `fast` by 2 steps: `fast = fast.next.next`.
5. If `slow == fast`, a cycle is detected.
6. If the loop ends, return `False`.

---

## Code (Python)

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        # Initialize both pointers at the head
        slow = fast = head
        
        # Traverse until fast reaches the end of the list
        while fast and fast.next:
            slow = slow.next          # Moves 1 step
            fast = fast.next.next     # Moves 2 steps
            
            # If they meet, there is a cycle
            if slow == fast:
                return True
        
        # If fast reaches None, no cycle exists
        return False
```

---

## Dry Run (Smart Example)

**Input:** `head = [3, 2, 0, -4]`, `pos = 1` (Cycle at node with value 2)

| Step | Slow Pointer (Value) | Fast Pointer (Value) | Explanation |
| :--- | :--- | :--- | :--- |
| 0 | 3 | 3 | Initial state at head. |
| 1 | 2 | 0 | Slow moves to 2, Fast moves to 0. |
| 2 | 0 | 2 | Slow moves to 0, Fast laps around to 2. |
| 3 | -4 | -4 | **Meeting Point!** Cycle detected. |

---

## Edge Cases

- **Empty List (`head is None`):** Fast/Slow pointers handle this; loop won't start. Returns `False`.
- **Single Node, No Cycle:** `fast.next` will be `None`. Returns `False`.
- **Single Node, Self Cycle:** `slow` and `fast` will meet on first iteration. Returns `True`.
- **Two Nodes, No Cycle:** `fast.next.next` will be `None`. Returns `False`.

---

## Mistakes

- **Incorrect Hash Set Storage:** Storing only the node `value` instead of the `node` reference. (Nodes can have duplicate values; references are unique).
- **Missing Null Checks:** Forgetting to check `while fast and fast.next`.
- **Pointer Initialization:** Starting `fast` at `head.next` without checking if `head` exists first.
- **User Mistake:** Attempting to store the entire node data/value instead of the node reference/object identity in a set, leading to incorrect cycle detection if values repeat.

---

## Complexity

Time: O(N) → In the worst case (cycle at the end or no cycle), we visit each node once or twice.  
Space: O(1) → Only two pointers are used regardless of list size.

---

## Similar Problems

- [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) - Medium
- [Happy Number](https://leetcode.com/problems/happy-number/) - Easy
- [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) - Medium
- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) - Easy

---

## Tags and Properties
- #dsa #important #revisit
- #linkedlist [[Linked List]]
- #floydscycle [[Floyd's Cycle-Finding Algorithm]]
- #fastandslow [[Fast and Slow Pointers]]
- **Revision Date:** 2026-05-10
- **Problem Link:** [LeetCode - Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-12)
- [ ] Day 7 Revision (2026-05-17)
- [ ] Day 15 Revision (2026-05-25)
- [ ] Day 30 Revision (2026-06-09)
