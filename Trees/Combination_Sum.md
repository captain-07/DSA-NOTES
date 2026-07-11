---
created: 2026-07-11
revisions:
  - 2026-07-13
  - 2026-07-18
  - 2026-07-26
  - 2026-08-10
---

# Combination Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  #Google #Amazon #Microsoft #Meta #Apple

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  #backtracking [[Backtracking]], #recursion [[Recursion]]

## Pattern

Backtracking (Pick / No Pick Decision Tree)

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

Use recursive backtracking. At each candidate, make two choices: **Pick** (add to path, subtract from target, stay at same index for reuse) or **No Pick** (skip, move to next index).

---
## ⚡ Quick Recall (VERY IMPORTANT)

State space exploration via `backtrack(idx, target, path)`: recurse with `(idx, target - candidates[idx], path + [candidates[idx]])` (then pop!), and recurse with `(idx + 1, target, path)`.

---
## Approach

### Brute Force
Generate all combinations up to length `target / min(candidates)` and check if their sum matches `target`.
Time: $O(N^K)$ where $K = \text{target}/\text{min}$.

### Better
N/A (Standard backtracking is the optimal approach).

### Optimal
1. Sort `candidates` to allow early pruning (if current candidate exceeds remaining target, stop further recursion for that branch).
2. Recursively explore two branches:
   - **Pick:** Check if candidate fits. Append to path, recursively call with same index, then pop to backtrack.
   - **No Pick:** Move to the next index.
3. Base cases: Target is 0 (valid path found, add copy to result); Target < 0 or index out of bounds (stop).

---
## Code (Python)

```python
class Solution:
    def combinationSum(self, candidates: list[int], target: int) -> list[list[int]]:
        results = []
        candidates.sort()  # Sort to enable early pruning

        def backtrack(index: int, current_target: int, path: list[int]):
            if current_target == 0:
                results.append(list(path))  # Store copy of valid path
                return

            if index >= len(candidates):
                return

            # Choice 1: Pick the current element (unlimited reuse)
            if candidates[index] <= current_target:
                path.append(candidates[index])
                # Recursion staying at 'index' allows reuse
                backtrack(index, current_target - candidates[index], path)
                path.pop()  # Backtrack: pop last element to restore state

            # Choice 2: No Pick / Skip the current element
            backtrack(index + 1, current_target, path)

        backtrack(0, target, [])
        return results
```

---
## Dry Run (Smart Example)

Input: `candidates = [2, 3]`, `target = 5`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `idx=0, tgt=5, path=[]` | Pick 2. Target becomes 3. Recurse on `idx=0`. |
| 2 | `idx=0, tgt=3, path=[2]` | Pick 2. Target becomes 1. Recurse on `idx=0`. |
| 3 | `idx=0, tgt=1, path=[2,2]` | Candidate 2 > target 1. Early prune. Pop. Recurse `idx=1, tgt=1` (No Pick). |
| 4 | `idx=1, tgt=1, path=[2,2]` | Candidate 3 > target 1. Return. Pop. Recurse `idx=1, tgt=3` (No Pick). |
| 5 | `idx=1, tgt=3, path=[2]` | Pick 3. Target becomes 0. Recurse. Save `[2,3]`. Pop 3. Recurse `idx=2, tgt=3` (No Pick). |
| 6 | `idx=2, tgt=3, path=[2]` | Index out of bounds. Return. Pop 2. Recurse `idx=1, tgt=5` (No Pick). |

---
## Edge Cases

- `target` is smaller than all candidates: Handled by candidate search boundaries, returns empty.
- Candidate list contains single element: Handles clean recursive reduction/rejection.
- Target is achievable only by multiple repeats: Correctly handled by remaining on same index.

---
## Mistakes

- **Backtracking Pop Omission:** Forgetting to pop the last element from the temporary path list after picking it and recursing, causing invalid candidates to persist in subsequent branches.
- **Copy Reference Bug:** Appending `path` instead of `list(path)` to the results list.
- **No Pruning:** Not sorting, which prevents early termination on branch paths where candidate exceeds remaining target.

---
## Complexity

Time: $O(N^{\frac{T}{M} + 1})$ where $N$ is candidate count, $T$ is target, and $M$ is min value in candidates.
Space: $O(\frac{T}{M})$ for recursive call stack and tracking path.

---
## Similar Problems

- [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/) - Medium
- [Combination Sum III](https://leetcode.com/problems/combination-sum-iii/) - Medium
- [Subsets](https://leetcode.com/problems/subsets/) - Medium

---
## Tags and Properties
- #dsa #important #revisit #backtracking #recursion
- Concepts: [[Backtracking]], [[Recursion]]
- Revision Date: 2026-07-11
- **Problem Link:** [LeetCode - Combination Sum](https://leetcode.com/problems/combination-sum/)

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-13)
- [ ] Day 7 Revision (2026-07-18)
- [ ] Day 15 Revision (2026-07-26)
- [ ] Day 30 Revision (2026-08-10)
