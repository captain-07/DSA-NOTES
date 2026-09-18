---
created: 2026-09-18
revisions:
  - 2026-09-20
  - 2026-09-25
  - 2026-10-03
  - 2026-10-18
---

# Find The Duplicate Number

---

## Metadata & Placement Tags

- **Folder:** Arrays
- **Target Companies:** #Amazon #Microsoft #Google #Facebook #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #twopointers [[Two Pointers]], #floydscycle [[Floyd's Cycle Detection]], #binarysearch [[Binary Search]], #bitmanipulation [[Bit Manipulation]]

## Pattern

Floyd's Cycle Detection (Fast & Slow Pointers) / Negative Marking (Array as Hash Map)

---

## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

The array of size $n+1$ with values from $1$ to $n$ can be viewed as a linked list where `nums[i]` points to index `nums[i]`. Because a duplicate value exists, multiple indices point to the same value, creating a cycle. Floyd's Tortoise and Hare algorithm finds the cycle's entrance, which is the duplicate number.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Treat array indices as pointers (`nums[i]` $\rightarrow$ `nums[nums[i]]`). Use fast/slow pointers to find cycle intersection, then reset slow to head to locate cycle entry.

---

## Approach

### Brute Force
- Sort array and scan adjacent elements.
- Time: $O(n \log n)$, Space: $O(1)$ (or $O(n)$ depending on sort algorithm).

### Better (Negative Marking)
- Iterate array, negate value at index `abs(num)`. If value at index `abs(num)` is already negative, `abs(num)` is duplicate.
- Time: $O(n)$, Space: $O(1)$. Modifies input array (violates $O(1)$ read-only constraint of LeetCode 287).

### Optimal (Floyd's Cycle Detection)
1. Initialize `slow = nums[0]` and `fast = nums[0]`.
2. Move `slow` by 1 step (`slow = nums[slow]`) and `fast` by 2 steps (`fast = nums[nums[fast]]`) until they meet.
3. Reset `slow` to `nums[0]`.
4. Move both `slow` and `fast` by 1 step until they meet again.
5. The meeting point is the duplicate number.

---

## Code (Python)

```python
class Solution:
    def findDuplicate(self, nums: list[int]) -> int:
        # Step 1: Initialize slow and fast pointers
        slow_pointer = nums[0]
        fast_pointer = nums[0]

        # Step 2: Find the intersection point in the cycle
        while True:
            slow_pointer = nums[slow_pointer]
            fast_pointer = nums[nums[fast_pointer]]
            if slow_pointer == fast_pointer:
                break

        # Step 3: Find the entrance to the cycle (the duplicate number)
        slow_pointer = nums[0]
        while slow_pointer != fast_pointer:
            slow_pointer = nums[slow_pointer]
            fast_pointer = nums[fast_pointer]

        return slow_pointer
```

---

## Dry Run (Smart Example)

Input: `nums = [1, 3, 4, 2, 2]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| **Phase 1 Start** | `slow = 1`, `fast = 1` | Start at index 0. |
| **Phase 1 Iteration** | `slow = 3`, `fast = 2` | `slow = nums[1]=3`, `fast = nums[nums[1]]=2`. |
| **Phase 1 Iteration** | `slow = 2`, `fast = 4` | `slow = nums[3]=2`, `fast = nums[nums[2]]=4`. |
| **Phase 1 Meet** | `slow = 4`, `fast = 4` | `slow = nums[2]=4`, `fast = nums[nums[4]]=4`. Meeting point reached! |
| **Phase 2 Reset** | `slow = 1`, `fast = 4` | Reset `slow` to `nums[0]`. |
| **Phase 2 Step 1** | `slow = 3`, `fast = 2` | `slow = nums[1]=3`, `fast = nums[4]=2`. |
| **Phase 2 Step 2** | `slow = 2`, `fast = 2` | `slow = nums[3]=2`, `fast = nums[2]=2`. Duplicate found! |

---

## Edge Cases

- **Duplicate appears more than twice:** e.g., `[2, 2, 2, 2, 2]` $\rightarrow$ Fast/slow pointers handle multi-in-degree nodes naturally.
- **Duplicate at boundaries:** e.g., `[1, 1]` or `[3, 1, 3, 4, 2]` $\rightarrow$ Correctly detects start/end cycle points.
- **Minimum length array ($n=1$):** e.g., `[1, 1]` $\rightarrow$ Correctly loops back immediately.

---

## Mistakes

- **The Negative Marking Technique:** Modifying array elements (`nums[abs(x)] = -nums[abs(x)]`) works in $O(n)$ time and $O(1)$ space, but **violates the read-only restriction** of the problem. Always ask the interviewer if mutating the array is permitted.
- **Confusing Array Values with Indices:** Forgetting that values are $1$-indexed and act as pointer addresses into $0$-indexed array.
- **Incorrect Fast Pointer Steps:** Advancing `fast` as `fast += 2` instead of `nums[nums[fast]]`.

---

## Complexity

Time: $O(n)$ $\rightarrow$ Cycle detection traverses nodes linearly.
Space: $O(1)$ $\rightarrow$ Uses only two pointer variables without modifying input array.

---

## Similar Problems

- [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) - Medium
- [First Missing Positive](https://leetcode.com/problems/first-missing-positive/) - Hard
- [Find all Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/) - Easy
- [Set Mismatch](https://leetcode.com/problems/set-mismatch/) - Easy

---

## Tags and Properties

- #dsa #important #revisit
- #arrays #fastslowpointers #floydscycle
- [[Two Pointers]] [[Floyd's Cycle Detection]] [[Array Mutation]]
- **Revision Date:** 2026-09-18
- **Problem Link:** [Find the Duplicate Number - LeetCode](https://leetcode.com/problems/find-the-duplicate-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-20)
- [ ] Day 7 Revision (2026-09-25)
- [ ] Day 15 Revision (2026-10-03)
- [ ] Day 30 Revision (2026-10-18)
