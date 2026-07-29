---
created: 2026-07-29
revisions:
  - 2026-07-31
  - 2026-08-05
  - 2026-08-13
  - 2026-08-28
---

# Implement Min Stack

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Bloomberg #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #stack [[Stack]]
  - #design [[Design]]

## Pattern

Stack State Tracking

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

To retrieve the minimum element in $O(1)$ time, we must couple each value in the stack with the minimum value present in the stack at or below that element's level. Because stack operations are LIFO, the minimum element at any state is deterministic and depends solely on history.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Store state snapshot: Either use a parallel stack tracking the minimums, or push `(val, current_min)` tuples to a single stack.

---
## Approach

### Brute Force
- Iterate through the entire stack to find the minimum on every `getMin()` call.
- Time: $O(N)$ for `getMin()`, $O(1)$ for push/pop. Space: $O(1)$ auxiliary.

### Better
- Store `(val, current_min)` pairs in a single stack.
- Time: $O(1)$ all operations. Space: $O(N)$ because every element stores a pair.

### Optimal 1 (Two Stacks - Conditional Push)
- Maintain a `main_stack` and a `min_stack`.
- Only push to `min_stack` if the new value is $\le$ current minimum. Only pop from `min_stack` if the popped value from `main_stack` equals the top of `min_stack`.
- Time: $O(1)$ all operations. Space: $O(N)$ worst-case, but saves space on average.

### Optimal 2 (Single Stack - Value Encoding)
- Store a modified value $2 \cdot \text{val} - \text{min\_val}$ when a new minimum is encountered to retrieve the previous minimum upon popping, using only a single integer stack and a single variable.

---
## Code (Python)

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        # Push to min_stack only if it's empty or val is a new minimum
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self) -> None:
        if self.stack:
            val = self.stack.pop()
            # Pop from min_stack if the popped value was the current minimum
            if val == self.min_stack[-1]:
                self.min_stack.pop()

    def top(self) -> int:
        return self.stack[-1] if self.stack else -1

    def getMin(self) -> int:
        return self.min_stack[-1] if self.min_stack else -1
```

---
## Dry Run (Smart Example)

Input Operations: `push(-2)`, `push(0)`, `push(-3)`, `getMin()`, `pop()`, `top()`, `getMin()`

| Step | Operation | `stack` | `min_stack` | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `push(-2)` | `[-2]` | `[-2]` | Stack is empty; `-2` becomes the min. |
| 2 | `push(0)` | `[-2, 0]` | `[-2]` | `0 > -2`, so `min_stack` is unchanged. |
| 3 | `push(-3)` | `[-2, 0, -3]` | `[-2, -3]` | `-3 <= -2`, push `-3` to `min_stack`. |
| 4 | `getMin()` | `[-2, 0, -3]` | `[-2, -3]` | Returns top of `min_stack` (`-3`). |
| 5 | `pop()` | `[-2, 0]` | `[-2]` | Popped `-3` equals top of `min_stack`, pop both. |
| 6 | `top()` | `[-2, 0]` | `[-2]` | Returns top of `stack` (`0`). |
| 7 | `getMin()` | `[-2, 0]` | `[-2]` | Returns top of `min_stack` (`-2`). |

---
## Edge Cases

- **Empty Stack:** Calling `pop()`, `top()`, or `getMin()` when the stack is empty (handled by checking stack sizes).
- **Duplicate Minimums:** Pushing duplicate minimum values (e.g., `[-2, -2]`). Handled by using `val <= self.min_stack[-1]` to push duplicates to the `min_stack`.
- **Negative Values:** Handled correctly since standard numeric comparisons support negative numbers.

---
## Mistakes

- **User Mistake:** Believing the double stack using approach is always easy to understand and space saving. While it is easy to understand, it wastes space if we push the minimum on *every* push operation. The optimization of only pushing to the `min_stack` when `val <= min_stack[-1]` is crucial for saving space.
- Failing to use `val <= min_stack[-1]` (using `<` instead), which causes duplicate minimum elements to not be pushed, resulting in incorrect state after popping.

---
## Complexity

- **Time:** $O(1)$ for all operations (`push`, `pop`, `top`, `getMin`) since we only perform stack appends and pops.
- **Space:** $O(N)$ auxiliary space in the worst case (when elements are added in descending order).

---
## Similar Problems

- [Max Stack](https://leetcode.com/problems/max-stack/) - Easy
- [Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/) - Easy
- [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/) - Hard

---
## Tags and Properties

- #dsa #important #revisit #stack [[Stack]] [[Design]]
- **Revision Date:** 2026-07-29
- **Problem Link:** [LeetCode - Implement Min Stack](https://leetcode.com/problems/min-stack/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-31)
- [ ] Day 7 Revision (2026-08-05)
- [ ] Day 15 Revision (2026-08-13)
- [ ] Day 30 Revision (2026-08-28)
