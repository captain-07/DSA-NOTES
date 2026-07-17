---
created: 2026-07-17
revisions:
  - 2026-07-19
  - 2026-07-24
  - 2026-08-01
  - 2026-08-16
---

# Combination Sum Iii

---

## Metadata & Placement Tags

- **Target Companies:** #Google #Amazon #Microsoft #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #backtracking [[Backtracking]], #recursion [[Recursion]]

---
## Pattern

Backtracking (Combinations with Constraints)

---
## Difficulty

Medium #medium

---
## ⚡ Key Idea (Core Insight)

Use backtracking to explore combinations of size $k$ that sum to $n$ using digits 1–9. To prevent using the same number multiple times or generating duplicate permutations, enforce a strict ascending order by passing a `start_num` parameter to the recursion, allowing only numbers larger than the current one to be selected next.

---
## ⚡ Quick Recall (VERY IMPORTANT)

To prevent duplicates and maintain combination order: Iterate $i$ from `start_num` to 9, and recurse with `start_num = i + 1`.

---
## Approach

### Brute Force
Generate all $2^9 = 512$ subsets of the set $\{1, 2, 3, 4, 5, 6, 7, 8, 9\}$, then filter those of size $k$ that sum to $n$.
- **Time Complexity:** $O(2^9 \cdot k) \approx O(1)$
- **Space Complexity:** $O(k)$

### Better
Not applicable (Backtracking with pruning is already the optimal standard approach for generating combinations).

### Optimal
1. Define a helper method that takes `start_num`, the current `path` of chosen numbers, and the `remaining_sum`.
2. **Base Cases:**
   - If `len(path) == k` and `remaining_sum == 0`, append a copy of `path` to the results.
   - If `len(path) > k` or `remaining_sum < 0`, prune the branch and return.
3. **Transition:** Loop $i$ from `start_num` to 9. Add $i$ to `path`, recurse with `i + 1` (to prevent reuse), and backtrack by popping $i$.

---
## Code (Python)

```python
class Solution:
    def combinationSum3(self, k: int, n: int) -> list[list[int]]:
        results = []
        # Start backtracking from digit 1, with an empty path and target n
        self.backtrack(1, k, n, [], results)
        return results

    def backtrack(self, start_num: int, k: int, remaining: int, path: list[int], results: list[list[int]]):
        # Base case: valid combination found
        if len(path) == k:
            if remaining == 0:
                results.append(list(path))
            return

        # Pruning: if remaining sum becomes negative
        if remaining < 0:
            return

        # Try choosing numbers from start_num up to 9
        for i in range(start_num, 10):
            path.append(i)
            # Recurse with i + 1 to ensure numbers are not repeated and remain sorted
            self.backtrack(i + 1, k, remaining - i, path, results)
            # Backtrack
            path.pop()
```

---
## Dry Run (Smart Example)

Input: `k = 2`, `n = 6`

| Step | Variables (`start_num`, `remaining`, `path`) | Explanation |
| :--- | :--- | :--- |
| 1 | `start_num=1, remaining=6, path=[]` | Root call. Starts loop from $i=1$. |
| 2 | `start_num=2, remaining=5, path=[1]` | Picked 1. Loop starts from $i=2$. |
| 3 | `start_num=3, remaining=3, path=[1, 2]` | Picked 2. Length reached $k=2$, but `remaining=3 != 0`. Backtrack. |
| 4 | `start_num=4, remaining=2, path=[1, 3]` | Backtracked 2, picked 3. Length reached $k=2$, `remaining=2 != 0`. Backtrack. |
| 5 | `start_num=6, remaining=0, path=[1, 5]` | Backtracked 4, picked 5. Length $k=2$, `remaining=0`. Valid! Save `[1, 5]`. |
| 6 | `start_num=3, remaining=4, path=[2]` | Backtracked all under `path=[1]`. Picked 2. Loop starts from $i=3$. |
| 7 | `start_num=5, remaining=0, path=[2, 4]` | Picked 4. Length $k=2$, `remaining=0`. Valid! Save `[2, 4]`. |

---
## Edge Cases

- **$n$ is too small or too large:** e.g., $k=3, n=2$ (impossible, min sum is $1+2+3=6$) or $n=45$ (max possible sum for $k=9$ is 45) -> Handled by pruning and base cases.
- **$k > 9$:** Impossible as digits are 1–9 and cannot be repeated -> Handled naturally since recursion terminates when `start_num > 9`.
- **$k=1$:** Single element check -> Correctly handles and returns $[[n]]$ if $n \le 9$.

---
## Mistakes

- **Reusing digits:** Forgetting to pass `i + 1` to the next recursion call, leading to numbers repeating within a combination (e.g., `[2, 2]`).
- **Generating permutations:** Starting the loop from 1 in every recursive step instead of `start_num`, which produces duplicates like `[1, 5]` and `[5, 1]`. The strict ascending index restriction $i+1$ guarantees unique sorted combinations.
- **Missing pruning:** Not returning early when the current sum exceeds $n$, resulting in unnecessary search space exploration.

---
## Complexity

- **Time:** $O(\binom{9}{k})$ → We choose $k$ unique numbers out of 9, leading to at most $\frac{9!}{k!(9-k)!}$ combinations.
- **Space:** $O(k)$ → The recursion stack depth and path list store at most $k$ elements.

---
## Similar Problems

- [Combination Sum](https://leetcode.com/problems/combination-sum/) - Medium
- [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/) - Medium
- [Combinations](https://leetcode.com/problems/combinations/) - Medium
- [Subsets](https://leetcode.com/problems/subsets/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #backtracking #combinations
- Obsidian Links: [[Backtracking]], [[Recursion]]
- **Revision Date:** 2026-07-17
- **Problem Link:** [LeetCode - Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-19)
- [ ] Day 7 Revision (2026-07-24)
- [ ] Day 15 Revision (2026-08-01)
- [ ] Day 30 Revision (2026-08-16)
