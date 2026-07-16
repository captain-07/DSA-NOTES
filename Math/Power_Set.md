---
created: 2026-07-10
revisions:
  - 2026-07-12
  - 2026-07-17
  - 2026-07-25
  - 2026-08-09
---

# Power Set

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Apple

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #backtracking [[Backtracking]], #bitmanipulation [[Bit Manipulation]]

---
## Pattern

Backtracking (State Space Search) OR Bit Manipulation (Binary Simulation)

---
## Difficulty

Medium #medium

---
## ⚡ Key Idea (Core Insight)

For each element, we have a binary choice: either include it in the current subset or exclude it. Simulating this choice for all $N$ elements recursively or using binary representation generates all $2^N$ possible subsets.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Think of a binary decision tree: at each index, you branch by either adding the element to your running list or skipping it.

---
## Approach

### Brute Force
- N/A (Subset generation is inherently exponential; there is no non-exponential brute force).
- Time Complexity: O(2^N * N)

### Optimal 1: Backtracking (Decision Tree)
- Traverse indices from 0 to N-1. At each step, recursively branch into two paths: one including `nums[index]` and one excluding it.
- Time Complexity: O(2^N * N)

### Optimal 2: Bit Manipulation
- An array of size $N$ has $2^N$ subsets. Map numbers from $0$ to $2^N - 1$ to subset bitmasks: if the $j$-th bit of $i$ is 1, include `nums[j]`.
- Time Complexity: O(2^N * N)

---
## Code (Python)

```python
class Solution:
    def subsets(self, nums: list[int]) -> list[list[int]]:
        # Approach 1: Backtracking (Decision Tree)
        self.result = []
        self.backtrack(nums, 0, [])
        return self.result

    def backtrack(self, nums: list[int], index: int, current_path: list[int]):
        # Base Case: processed all elements
        if index == len(nums):
            self.result.append(current_path.copy())
            return

        # Choice 1: Include nums[index]
        current_path.append(nums[index])
        self.backtrack(nums, index + 1, current_path)

        # Choice 2: Exclude nums[index] (Backtrack)
        current_path.pop()
        self.backtrack(nums, index + 1, current_path)

    def subsets_bitmask(self, nums: list[int]) -> list[list[int]]:
        # Approach 2: Bit Manipulation
        n = len(nums)
        result = []
        # Total 2^n subsets
        for i in range(1 << n):
            subset = []
            for j in range(n):
                # If j-th bit is set, include nums[j]
                if (i >> j) & 1:
                    subset.append(nums[j])
            result.append(subset)
        return result
```

---
## Dry Run (Smart Example)

Input: `nums = [1, 2]` using Backtracking

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `index=0`, `path=[]` | Start. Include `nums[0]` (1). Move to `index=1`, `path=[1]`. |
| 2 | `index=1`, `path=[1]` | Include `nums[1]` (2). Move to `index=2`, `path=[1, 2]`. |
| 3 | `index=2`, `path=[1, 2]` | Base Case: append `[1, 2]` to result. Return, pop 2. |
| 4 | `index=1`, `path=[1]` | Exclude `nums[1]`. Move to `index=2`, `path=[1]`. |
| 5 | `index=2`, `path=[1]` | Base Case: append `[1]` to result. Return, pop 1. |
| 6 | `index=0`, `path=[]` | Exclude `nums[0]`. Move to `index=1`, `path=[]`. |
| 7 | `index=1`, `path=[]` | Include `nums[1]` (2). Move to `index=2`, `path=[2]`. |
| 8 | `index=2`, `path=[2]` | Base Case: append `[2]` to result. Return, pop 2. |
| 9 | `index=1`, `path=[]` | Exclude `nums[1]`. Move to `index=2`, `path=[]`. |
| 10 | `index=2`, `path=[]` | Base Case: append `[]` to result. Return. Done. |

---
## Edge Cases

- `nums` is empty (`[]`): Returns `[[]]`.
- Single element `[1]`: Returns `[[], [1]]`.
- Elements containing negative values: Solved identically since indices determine inclusion.

---
## Mistakes

- User Mistake: "did'nt understand anything" (Unable to visualize the state space. Think of it as a tree of yes/no decisions for each item).
- Forgetting to copy the current path (`current_path.copy()`) before adding it to the final output list, resulting in all empty lists in the result.
- Confusing subsets with contiguous subarrays.

---
## Complexity

Time: O(N * 2^N) → $2^N$ total subsets, each taking O(N) to build and copy.
Space: O(N) → Maximum depth of the recursion stack is $N$.

---
## Similar Problems

- [Subsets II](https://leetcode.com/problems/subsets-ii/) - Medium
- [Combinations](https://leetcode.com/problems/combinations/) - Medium
- [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #backtracking #bitmanipulation
- [[Backtracking]] [[Bit Manipulation]] [[Recursion]]
- Revision Date: 2026-07-10
- **Problem Link:** [LeetCode Subsets](https://leetcode.com/problems/subsets/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-12)
- [ ] Day 7 Revision (2026-07-17)
- [ ] Day 15 Revision (2026-07-25)
- [ ] Day 30 Revision (2026-08-09)
