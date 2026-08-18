---
created: 2026-07-13
revisions:
  - 2026-07-15
  - 2026-07-20
  - 2026-07-28
  - 2026-08-12
---

# Combination Sum II

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Adobe

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #backtracking [[Backtracking]]
  - #sorting [[Sorting]]

## Pattern

Backtracking + Sorting for Duplicate Elimination

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

To avoid duplicate combinations without using extra space, sort the array first. During recursion, iterate through candidate elements using a `for` loop and skip any element if it is identical to the previous one at the *same* recursion depth.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort the input. Use a `for` loop from `start` to `len(candidates)`. Skip duplicates using `if i > start and candidates[i] == candidates[i-1]: continue`. Recurse with `i + 1`.

---

## Approach

### Brute Force
- Generate all possible subsets using recursion, sort each valid subset, and insert them into a Set to eliminate duplicates.
- **Time Complexity:** O(2^N * N log N)

### Better
- Standard backtracking without sorting to generate paths, checking sum at each step, and using a Set to filter unique combinations.
- **Time Complexity:** O(2^N * N)

### Optimal
- Sort candidates first.
- Implement helper method using a `for` loop to check options from `start` to `end`.
- If `candidates[i] == candidates[i-1]` and `i > start`, skip it.
- Prune the branch if `candidates[i] > target`.
- Recurse with index `i + 1` and `target - candidates[i]`.
- **Time Complexity:** O(2^N * N)

---

## Code (Python)

```python
class Solution:
    def combinationSum2(self, candidates: list[int], target: int) -> list[list[int]]:
        candidates.sort()
        result = []
        self.backtrack(candidates, target, 0, [], result)
        return result

    def backtrack(self, candidates: list[int], target: int, start: int, path: list[int], result: list[list[int]]):
        if target == 0:
            result.append(list(path))
            return

        for i in range(start, len(candidates)):
            # Skip duplicates at the same recursion depth
            if i > start and candidates[i] == candidates[i - 1]:
                continue

            # Prune branches when remaining candidates exceed the target
            if candidates[i] > target:
                break

            path.append(candidates[i])
            # Recurse with next index (i + 1) since each element can be used once
            self.backtrack(candidates, target - candidates[i], i + 1, path, result)
            path.pop()
```

---

## Dry Run (Smart Example)

Input: `candidates = [2, 5, 2, 1, 2]`, `target = 5`
Sorted candidates: `[1, 2, 2, 2, 5]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| **1** | `start=0`, `target=5`, `path=[]` | Loop `i=0` (`val=1`). Recurse with `start=1, target=4, path=[1]`. |
| **2** | `start=1`, `target=4`, `path=[1]` | Loop `i=1` (`val=2`). Recurse with `start=2, target=2, path=[1, 2]`. |
| **3** | `start=2`, `target=2`, `path=[1, 2]` | Loop `i=2` (`val=2`). Recurse with `start=3, target=0, path=[1, 2, 2]`. Target is 0, save path `[1, 2, 2]`. Backtrack to `path=[1, 2]`. |
| **4** | `start=2`, `target=2`, `path=[1, 2]` | Loop `i=3` (`val=2`). Skip because `i > start` (3 > 2) and `candidates[3] == candidates[2]`. Loop `i=4` (`val=5` > 2), break. Backtrack to `path=[1]`. |
| **5** | `start=1`, `target=4`, `path=[1]` | Loop `i=2` (`val=2`). Skip because `i > start` (2 > 1) and `candidates[2] == candidates[1]`. |

---

## Edge Cases

- **Target smaller than min element:** The loop breaks immediately (returns `[]`).
- **All candidates identical:** The duplicate check ensures only unique combinations of the duplicate elements are selected.
- **No valid combinations:** Returns `[]` after searching all viable paths.
- **Single element array:** Returns `[[element]]` if element matches target, else `[]`.

---

## Mistakes

- **Forgetting to sort:** Sorting is mandatory for the adjacent duplicate check `candidates[i] == candidates[i-1]` to work.
- **Not using a for loop:** Using direct index inclusion/exclusion (binary decision tree) makes it extremely hard to skip duplicates efficiently.
- **Incorrect duplicate check condition:** Using `i > 0` instead of `i > start`. `i > start` ensures we skip duplicates at the *same* recursion level, but allows the same duplicate value to be chosen across different depths.

---

## Complexity

- **Time:** O(2^N * N) → In the worst case, we generate all subsets. Copying a valid combination to results takes O(N) time.
- **Space:** O(N) → Max recursion stack depth is N.

---

## Similar Problems

- [Combination Sum](https://leetcode.com/problems/combination-sum/) - Medium
- [Subsets II](https://leetcode.com/problems/subsets-ii/) - Medium
- [Permutations II](https://leetcode.com/problems/permutations-ii/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #backtracking [[Backtracking]]
- #sorting [[Sorting]]
- **Problem Link:** [LeetCode - Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-15)
- [ ] Day 7 Revision (2026-07-20)
- [ ] Day 15 Revision (2026-07-28)
- [ ] Day 30 Revision (2026-08-12)
