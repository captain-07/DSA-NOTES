---
created: 2026-07-24
revisions:
  - 2026-07-26
  - 2026-07-31
  - 2026-08-08
  - 2026-08-23
---

# Power Set Bit Manipulation

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Apple

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #bitmanipulation [[Bit Manipulation]]
  - #backtracking [[Backtracking]]

## Pattern

Bitmasking / Subset Generation

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

An array of size $N$ has $2^N$ subsets. We map each subset to a binary number from $0$ to $2^N - 1$. The $j$-th bit of the binary representation of number $i$ dictates whether the element at index $j$ (`nums[j]`) is included (1) or excluded (0).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Iterate `i` from $0$ to $(2^N - 1)$. For each `i`, construct a subset by adding `nums[j]` if `i & (1 << j)` is non-zero.

---

## Approach

### Brute Force
- Recursion / Backtracking to explore inclusion/exclusion at each index.
- Time Complexity: $O(N \cdot 2^N)$
- Space Complexity: $O(N)$ recursion stack depth.

### Optimal
- Iterative bitmasking from $0$ to $(1 \ll N) - 1$.
- Time Complexity: $O(N \cdot 2^N)$
- Space Complexity: $O(1)$ auxiliary space.

---

## Code (Python)

```python
class Solution:
    def subsets(self, nums: list[int]) -> list[list[int]]:
        n = len(nums)
        power_set_size = 1 << n  # 2^n subsets
        result = []

        for i in range(power_set_size):
            subset = []
            for j in range(n):
                # Check if the j-th bit of bitmask i is set
                if i & (1 << j):
                    subset.append(nums[j])
            result.append(subset)

        return result
```

---

## Dry Run (Smart Example)

Input: `nums = [3, -1]` ($N = 2$, `power_set_size = 4`)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `i = 0 (00)` | `0 & (1<<0) = 0`, `0 & (1<<1) = 0`. Subset: `[]`. |
| 2 | `i = 1 (01)` | `1 & (1<<0) = 1` (Include `3`), `1 & (1<<1) = 0`. Subset: `[3]`. |
| 3 | `i = 2 (10)` | `2 & (1<<0) = 0`, `2 & (1<<1) = 2` (Include `-1`). Subset: `[-1]`. |
| 4 | `i = 3 (11)` | `3 & (1<<0) = 1` (Include `3`), `3 & (1<<1) = 2` (Include `-1`). Subset: `[3, -1]`. |

---

## Edge Cases

- Empty array `nums = []` -> returns `[[]]`.
- Array of size 1 `nums = [0]` -> returns `[[], [0]]`.
- Elements with negative values or duplicates -> handled correctly because we branch on indices, not values.

---

## Mistakes

- **Misunderstanding `i & (1 << j)`**:
  - `1 << j` creates a bitmask with a single set bit at index `j` (e.g., `j=2` -> `0100` in binary).
  - `i & (1 << j)` performs a bitwise AND. It isolates the $j$-th bit of `i`. If it evaluates to any non-zero value, the $j$-th bit is active.
  - **Trap**: Do not compare it to 1 (i.e. `(i & (1 << j)) == 1` is false for $j > 0$). Instead, use `if i & (1 << j):` or compare to `!= 0`.
- **Precedence Error**: Writing `i & 1 << j` without parenthesis. Python evaluates shift operations before bitwise AND, but explicit grouping `i & (1 << j)` prevents logical errors.

---

## Complexity

Time: $O(N \cdot 2^N)$ -> Outer loop runs $2^N$ times; inner loop runs $N$ times.
Space: $O(1)$ -> Excludes output memory; only uses $O(N)$ for temporary subset container storage.

---

## Similar Problems

- [Subsets](https://leetcode.com/problems/subsets/) - Medium
- [Subsets II](https://leetcode.com/problems/subsets-ii/) - Medium
- [Letter Case Permutation](https://leetcode.com/problems/letter-case-permutation/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #bitmanipulation #powerset
  - [[Bit Manipulation]]
  - [[Subsets]]
  - Revision Date: 2026-07-24
  - **Problem Link:** [LeetCode Subsets](https://leetcode.com/problems/subsets/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-26)
- [ ] Day 7 Revision (2026-07-31)
- [ ] Day 15 Revision (2026-08-08)
- [ ] Day 30 Revision (2026-08-23)
