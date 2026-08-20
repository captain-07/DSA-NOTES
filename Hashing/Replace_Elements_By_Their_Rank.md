---
created: 2026-08-20
revisions:
  - 2026-08-22
  - 2026-08-27
  - 2026-09-04
  - 2026-09-19
---

# Replace Elements By Their Rank

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Bloomberg #Adobe

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #sorting [[Sorting]], #hashmap [[HashMap]], #array [[Array]]

## Pattern

Sorting + Hash Map

---
## Difficulty

Easy
#easy

---
## ⚡ Key Idea (Core Insight)

The rank of an element corresponds to its 1-based position in a sorted sequence of unique elements. Extract unique values, sort them, and map them to their ranks.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Unique-sort the array, map values to their 1-based index using a hash map, and replace elements in the original array.

---
## Approach

### Brute Force
- Iterate through each element and count how many elements in the array are strictly smaller than it, then add 1.
- Time: O(N^2), Space: O(1)

### Optimal
- Create a sorted list of unique elements using a set.
- Map each element in the sorted list to its rank (1-based index) using a Hash Map.
- Map the original array to the ranks stored in the Hash Map.
- Time: O(N log N), Space: O(N)

---
## Code (Python)

```python
class Solution:
    def arrayRankTransform(self, arr: list[int]) -> list[int]:
        # Step 1: Remove duplicates and sort
        sorted_unique = sorted(set(arr))

        # Step 2: Map element to rank (1-based index)
        rank_map = {num: rank + 1 for rank, num in enumerate(sorted_unique)}

        # Step 3: Replace original elements with their ranks
        return [rank_map[num] for num in arr]
```

---
## Dry Run (Smart Example)

Input: `arr = [40, 10, -5, 10]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `arr = [40, 10, -5, 10]` | Input array containing duplicate (`10`) and negative (`-5`). |
| 2 | `sorted_unique = [-5, 10, 40]` | Duplicates are removed and values are sorted. |
| 3 | `rank_map = {-5: 1, 10: 2, 40: 3}` | Map values to their relative ranks. |
| 4 | Output: `[3, 2, 1, 2]` | Original array values replaced using `rank_map`. |

---
## Edge Cases

- **Empty Array:** `arr = []` returns `[]`.
- **All Elements Equal:** `arr = [10, 10, 10]` returns `[1, 1, 1]`.
- **Already Sorted:** `arr = [1, 2, 3]` returns `[1, 2, 3]`.
- **Negative Elements:** Negative numbers are sorted and ranked correctly.

---
## Mistakes

- Overcomplicating sorting logic: Use built-in `set` and `sorted` functions instead of manually tracking indices or writing complex partitioning. Keep code as simple as possible.
- Incorrectly handling duplicate ranks: Equal values must share the same rank.
- Off-by-one errors: Ensure the rank indexing starts at 1, not 0.

---
## Complexity

Time: O(N log N) → Dominated by sorting unique elements.
Space: O(N) → Storing unique elements and the lookup Hash Map.

---
## Similar Problems

- [Sort Array by Increasing Frequency](https://leetcode.com/problems/sort-array-by-increasing-frequency/) - Easy
- [Rank Teams by Votes](https://leetcode.com/problems/rank-teams-by-votes/) - Medium
- [Rank Transform of a Matrix](https://leetcode.com/problems/rank-transform-of-a-matrix/) - Hard

---
## Tags and Properties

- #dsa #important #revisit
- #sorting [[Sorting]] #hashmap [[HashMap]]
- Revision Date: 2026-08-20
- **Problem Link:** [LeetCode - Rank Transform of an Array](https://leetcode.com/problems/rank-transform-of-an-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-22)
- [ ] Day 7 Revision (2026-08-27)
- [ ] Day 15 Revision (2026-09-04)
- [ ] Day 30 Revision (2026-09-19)
