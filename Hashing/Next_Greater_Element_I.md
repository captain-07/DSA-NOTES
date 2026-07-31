---
created: 2026-07-31
revisions:
  - 2026-08-02
  - 2026-08-07
  - 2026-08-15
  - 2026-08-30
---

# Next Greater Element I

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Bloomberg

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #stack [[Stack]]
  - #hashmap [[HashMap]]
  - #monotonic-stack [[Monotonic Stack]]

---
## Pattern

Monotonic Decreasing Stack + HashMap lookup.

---
## Difficulty

Easy
#easy

---
## ⚡ Key Idea (Core Insight)

Process `nums2` from left to right. Maintain a monotonic decreasing stack of elements. When we find a number larger than the stack's top, it is the Next Greater Element (NGE) for that top element. Store this mapping in a hashmap.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Decrease-to-increase transition triggers NGE resolution. Pop smaller elements from stack to HashMap; lookup `nums1` in HashMap.

---
## Approach

### Brute Force
For each element in `nums1`, find its position in `nums2`, then scan right in `nums2` to find the first larger element.
- **Time:** $O(N \times M)$ where $N = \text{len}(nums1)$, $M = \text{len}(nums2)$.
- **Space:** $O(1)$.

### Optimal
Use a monotonic decreasing stack to find the NGE for all elements in `nums2` in a single pass. Store the results in a dictionary `nge_map`. Then, map elements of `nums1` to their NGEs using `nge_map` (defaulting to -1 if not found).
- **Time:** $O(M + N)$ where $M = \text{len}(nums2)$, $N = \text{len}(nums1)$.
- **Space:** $O(M)$ to store the stack and the map.

---
## Code (Python)

```python
class Solution:
    def nextGreaterElement(self, nums1: list[int], nums2: list[int]) -> list[int]:
        # Stores element -> its next greater element
        nge_map = {}
        stack = []

        # Build the map using a monotonic decreasing stack
        for num in nums2:
            # If current element is greater than the element on top of stack,
            # we found its next greater element.
            while stack and num > stack[-1]:
                smaller_num = stack.pop()
                nge_map[smaller_num] = num
            # Push current element to stack to find its greater element later
            stack.append(num)

        # Build the result for nums1 using the map
        result = []
        for num in nums1:
            # If it's not in the map, there's no greater element (default to -1)
            result.append(nge_map.get(num, -1))

        return result
```

---
## Dry Run (Smart Example)

Input: `nums1 = [4, 1]`, `nums2 = [2, 1, 3, -1, 4]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `num = 2`, `stack = [2]`, `nge_map = {}` | Stack is empty, append `2`. |
| 2 | `num = 1`, `stack = [2, 1]`, `nge_map = {}` | `1 < 2`, stack is decreasing. Append `1`. |
| 3 | `num = 3`, `stack = [3]`, `nge_map = {1: 3, 2: 3}` | `3 > 1` (pop 1, map `1 -> 3`). `3 > 2` (pop 2, map `2 -> 3`). Append `3`. |
| 4 | `num = -1`, `stack = [3, -1]`, `nge_map = {1: 3, 2: 3}` | `-1 < 3`, stack is decreasing. Append `-1`. |
| 5 | `num = 4`, `stack = [4]`, `nge_map = {1: 3, 2: 3, -1: 4, 3: 4}` | `4 > -1` (pop -1, map `-1 -> 4`). `4 > 3` (pop 3, map `3 -> 4`). Append `4`. |

Result for `nums1 = [4, 1]` lookup: `nge_map.get(4, -1) = -1`, `nge_map.get(1, -1) = 3` $\rightarrow$ `[-1, 3]`.

---
## Edge Cases

- **Negative numbers present:** Monotonic stack works correctly as it relies on relative comparison ($>$ operator).
- **No greater element exists:** Stack items remain unpopped; lookup defaults to `-1` correctly.
- **Single element arrays:** Loops execute once, returns `[-1]`.

---
## Mistakes

- Overcomplicating the stack by storing indices instead of actual element values. Since elements in `nums2` are unique, storing values directly keeps the code clean and simple.
- Forgetting to handle elements remaining in the stack (implicitly handled by `.get(num, -1)`).
- Confusing monotonic increasing vs. decreasing stack logic.

---
## Complexity

Time: O(N + M) → We iterate through `nums2` of size M once, pushing/popping each element at most once ($O(M)$), and iterate through `nums1` of size N once ($O(N)$).
Space: O(M) → The stack and the hashmap store at most $M$ elements.

---
## Similar Problems

- [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/) - Medium
- [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) - Medium
- [Next Greater Element III](https://leetcode.com/problems/next-greater-element-iii/) - Medium
- [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/) - Hard

---
## Tags and Properties

- #dsa #important #revisit
- #stack [[Stack]]
- #hashmap [[HashMap]]
- #monotonic-stack [[Monotonic Stack]]
- **Revision Date:** 2026-07-31
- **Problem Link:** [LeetCode - Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-02)
- [ ] Day 7 Revision (2026-08-07)
- [ ] Day 15 Revision (2026-08-15)
- [ ] Day 30 Revision (2026-08-30)
