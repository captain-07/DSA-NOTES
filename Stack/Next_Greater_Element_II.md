---
created: 2026-08-02
revisions:
  - 2026-08-04
  - 2026-08-09
  - 2026-08-17
  - 2026-09-01
---

# Next Greater Element II

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Google #Microsoft #Bloomberg #Adobe
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #monotonicstack [[Monotonic Stack]], #array [[Array]]

---
## Pattern
Monotonic Stack + Circular Array Simulation (Modulo Indexing)

---
## Difficulty
Medium #medium

---
## ⚡ Key Idea (Core Insight)
Simulate array circularity by virtually doubling the array traversal (up to index `2N - 1`). Use a monotonic decreasing stack to store indices, popping them as you find larger elements to determine their next greater element.

---
## ⚡ Quick Recall (VERY IMPORTANT)
Loop `2N` times, resolve elements via `i % N` using a monotonic decreasing stack of indices.

---
## Approach

### Brute Force
- For each element, search the rest of the array and wrap around from the start using modulo index arithmetic.
- Time Complexity: O(N²)

### Better
- Physically double the array (concatenating it to itself) and use a standard Monotonic Stack.
- Time Complexity: O(N) but requires O(N) auxiliary space for the doubled array.

### Optimal
- Process indices virtually from `0` to `2N - 1` using `idx = i % N`.
- Maintain a monotonic decreasing stack of indices.
- While the stack is not empty and `nums[stack[-1]] < nums[idx]`, pop the index and update `res[popped_index] = nums[idx]`.
- Push the index to the stack only if we are in the first pass (`i < N`).

---
## Code (Python)

```python
class Solution:
    def nextGreaterElements(self, nums: list[int]) -> list[int]:
        n = len(nums)
        res = [-1] * n
        stack = []  # Stores indices

        # Traverse virtually up to 2 * n
        for i in range(2 * n):
            idx = i % n
            # Pop elements from stack if the current element is greater
            while stack and nums[stack[-1]] < nums[idx]:
                res[stack.pop()] = nums[idx]

            # Only push indices during the first traversal
            if i < n:
                stack.append(idx)

        return res
```

---
## Dry Run (Smart Example)

Input: `nums = [3, 8, 4, 1, 2]`, `n = 5`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| i=0 (idx=0) | stack=[0], res=[-1,-1,-1,-1,-1] | `nums[0]=3` pushed to stack. |
| i=1 (idx=1) | stack=[1], res=[8,-1,-1,-1,-1] | `nums[1]=8 > 3`, pop 0, set `res[0]=8`. Push 1. |
| i=2 (idx=2) | stack=[1, 2], res=[8,-1,-1,-1,-1] | `nums[2]=4 < 8`, push 2. |
| i=3 (idx=3) | stack=[1, 2, 3], res=[8,-1,-1,-1,-1] | `nums[3]=1 < 4`, push 3. |
| i=4 (idx=4) | stack=[1, 2, 4], res=[8,-1,2,-1,-1] | `nums[4]=2 > 1`, pop 3, set `res[3]=2`. Push 4. |
| i=5 (idx=0) | stack=[1, 2], res=[8,-1,2,-1,3] | Wrap-around: `nums[0]=3 > 2`, pop 4, set `res[4]=3`. |
| i=6 (idx=1) | stack=[] | `nums[1]=8 > 4`, pop 2, set `res[2]=8`. Stack has `1` (`nums[1]=8`), no pop. |

---
## Edge Cases
- **Single Element**: `[5]` → returns `[-1]`.
- **All Identical Elements**: `[3, 3, 3]` → returns `[-1, -1, -1]`.
- **Strictly Decreasing**: `[4, 3, 2, 1]` → only the maximum `4` yields `-1`; others wrap around to find their next greater.
- **Strictly Increasing**: `[1, 2, 3, 4]` → standard stack resolves all except the maximum `4`.

---
## Mistakes
- **Avoiding Virtual Optimization**: Stating "the idea of creating a circular array by doubling it is awesome" and physically copying the array. Use virtual indexing `i % n` instead to save O(N) space.
- **Pushing Values instead of Indices**: Storing raw values in the stack instead of their indices, preventing direct updates to the result array.
- **Non-Strict Comparison**: Using `nums[stack[-1]] <= nums[idx]` when the next greater element must be strictly larger.

---
## Complexity
Time: O(N) → Each index is pushed to the stack at most once and popped at most once.
Space: O(N) → Stack stores up to `N` indices in the worst-case (strictly decreasing array).

---
## Similar Problems
- [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/) - Easy
- [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) - Medium
- [Next Greater Element III](https://leetcode.com/problems/next-greater-element-iii/) - Medium
- [Online Stock Span](https://leetcode.com/problems/online-stock-span/) - Medium

---
## Tags and Properties
- #dsa #important #revisit #monotonicstack #circulararray
- Concept Links: [[Monotonic Stack]], [[Circular Array]]
- **Revision Date:** 2026-08-02
- **Problem Link:** [LeetCode 503 - Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-04)
- [ ] Day 7 Revision (2026-08-09)
- [ ] Day 15 Revision (2026-08-17)
- [ ] Day 30 Revision (2026-09-01)
