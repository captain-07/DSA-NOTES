---
created: 2026-07-16
revisions:
  - 2026-07-18
  - 2026-07-23
  - 2026-07-31
  - 2026-08-15
---

# Subset Sum I

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Microsoft #Paytm #Samsung
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #recursion [[Recursion]], #backtracking [[Backtracking]], #bit-manipulation [[Bit Manipulation]]

---
## Pattern

Recursion (Subsets / Pick & Don't Pick) or Bitmask Power Set

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

To find all subset sums, generate every possible subset. For each element at index `i`, we have two binary choices: either include it in the current subset sum, or exclude it. This generates all $2^N$ subsets (the Power Set).

---
## ⚡ Quick Recall (VERY IMPORTANT)

For every element: `helper(idx + 1, current_sum + arr[idx])` (pick) and `helper(idx + 1, current_sum)` (don't pick).

---
## Approach

### Brute Force (Power Set via Bitmasking)
Generate all $2^N$ subsets using bit representation from `0` to `2^N - 1`. If the $j$-th bit of the counter $i$ is set, include $arr[j]$ in the sum.
- Time Complexity: $O(N \cdot 2^N)$
- Space Complexity: $O(1)$ auxiliary (excluding output list)

### Optimal (Recursive Backtracking / Pick & Don't Pick)
Use a recursive function that traverses from index `0` to `N-1`. Maintain a `current_sum`. At each step, branch into two calls: one including the element, and one excluding it. Append `current_sum` to the result when the index reaches $N$. Sort the final results.
- Time Complexity: $O(2^N + 2^N \log(2^N))$ due to sorting $2^N$ sums.
- Space Complexity: $O(N)$ recursion stack space.

---
## Code (Python)

```python
class Solution:
    def subsetSums(self, arr: list[int], n: int) -> list[int]:
        ans = []

        def generate_sums(index: int, current_sum: int):
            # Base Case: processed all elements
            if index == n:
                ans.append(current_sum)
                return

            # Element Picked
            generate_sums(index + 1, current_sum + arr[index])

            # Element Not Picked
            generate_sums(index + 1, current_sum)

        generate_sums(0, 0)
        ans.sort()
        return ans
```

---
## Dry Run (Smart Example)

Input: `arr = [5, 2, 1]`, `n = 3`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `idx=0, sum=0` | Start. Call branch 1 (pick 5): `idx=1, sum=5`. Call branch 2 (don't pick): `idx=1, sum=0`. |
| 2 | `idx=1, sum=5` | For branch 1: Call pick 2 (`idx=2, sum=7`), call don't pick 2 (`idx=2, sum=5`). |
| 3 | `idx=2, sum=7` | For subset containing {5, 2}: Call pick 1 (`idx=3, sum=8`), call don't pick 1 (`idx=3, sum=7`). |
| 4 | `idx=3` (Base) | Recursion depth met. Leaves append `8` and `7` to `ans`. All other paths resolve similarly. |
| 5 | Post-process | `ans` before sorting: `[8, 7, 6, 5, 3, 2, 1, 0]`. Sorted `ans` = `[0, 1, 2, 3, 5, 6, 7, 8]`. |

---
## Edge Cases

- **Empty Array / $N = 0$:** Output `[0]` (the sum of the empty set).
- **Single Element Array `[x]`:** Output `[0, x]`.
- **Duplicates in input `[2, 2]`:** Generate all combinations even if sums duplicate: `[0, 2, 2, 4]`.
- **Negative Elements `[-1, 2]`:** The algorithm naturally handles sign transitions: `[0, -1, 2, 1]`.

---
## Mistakes

- **Power Set Misunderstanding:** Failing to see that a power set has size $2^N$ and represents all combinations of picking vs. not picking each element.
- **Sorting Too Early:** Sorting the input array does not optimize this recursion; sort the final sum list at the very end.
- **Missing Empty Subset:** Forgetting that the empty subset sum `0` must be included in the output.

---
## Complexity

Time: $O(2^N \log(2^N))$ → $2^N$ recursion states generated, plus sorting the final output of size $2^N$.
Space: $O(N)$ → Auxiliary stack space for recursion of depth $N$ (excluding the output array).

---
## Similar Problems

- [Subsets](https://leetcode.com/problems/subsets/) - Medium
- [Subsets II](https://leetcode.com/problems/subsets-ii/) - Medium
- [Combination Sum](https://leetcode.com/problems/combination-sum/) - Medium
- [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #recursion #backtracking
- [[Recursion]] [[Backtracking]] [[Subset Problems]]
- **Revision Date:** 2026-07-16
- **Problem Link:** [GeeksforGeeks - Subset Sums](https://www.geeksforgeeks.org/problems/subset-sums2234/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-18)
- [ ] Day 7 Revision (2026-07-23)
- [ ] Day 15 Revision (2026-07-31)
- [ ] Day 30 Revision (2026-08-15)
