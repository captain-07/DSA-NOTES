---
created: 2026-09-19
revisions:
  - 2026-09-21
  - 2026-09-26
  - 2026-10-04
  - 2026-10-19
---

# Assign Cookies

---

## Metadata & Placement Tags

- **Folder:** Greedy
- **Target Companies:**
  - #Amazon #Google #Microsoft #Apple #Bloomberg

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #greedy [[Greedy]]
  - #twopointers [[Two Pointers]]
  - #sorting [[Sorting]]

## Pattern

Two Pointers + Sorting (Greedy Allocation)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Sort both children's greed factors `g` and cookie sizes `s` in ascending order. Use a greedy approach to satisfy the child with the smallest greed factor using the smallest possible cookie that meets or exceeds their requirement.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort both arrays, advance cookie pointer every step, and advance child pointer only when the cookie satisfies the child (`s[cookie_idx] >= g[child_idx]`).

---

## Approach

### Brute Force
- Try every permutation of cookie assignments to find the maximum satisfied children.
- Time Complexity: O(N! * M) where N is number of children and M is number of cookies.

### Better
- Sort the cookies array and for each child, use binary search to find the smallest valid cookie, removing it once used.
- Time Complexity: O(M log M + N * M) due to array element removals.

### Optimal
- Sort both `g` and `s`.
- Use two pointers: `child_idx` for children and `cookie_idx` for cookies.
- Iterate through cookies: if `s[cookie_idx] >= g[child_idx]`, move `child_idx` forward.
- Always move `cookie_idx` forward.
- Return `child_idx` as the total count of satisfied children.

---

## Code (Python)

```python
class Solution:
    def findContentChildren(self, g: list[int], s: list[int]) -> int:
        # Sort both greed factors and cookie sizes
        g.sort()
        s.sort()

        child_idx = 0
        cookie_idx = 0

        # Traverse both arrays using two pointers
        while child_idx < len(g) and cookie_idx < len(s):
            # If current cookie can satisfy current child's greed
            if s[cookie_idx] >= g[child_idx]:
                child_idx += 1  # Move to the next child
            cookie_idx += 1     # Always try the next cookie

        return child_idx
```

---

## Dry Run (Smart Example)

Input: `g = [1, 2, 3]`, `s = [1, 1]`
Sorted: `g = [1, 2, 3]`, `s = [1, 1]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `child_idx = 0` (`g[0]=1`), `cookie_idx = 0` (`s[0]=1`) | `s[0] >= g[0]` (1 >= 1) is True. Child 0 satisfied. `child_idx` becomes 1, `cookie_idx` becomes 1. |
| 2 | `child_idx = 1` (`g[1]=2`), `cookie_idx = 1` (`s[1]=1`) | `s[1] >= g[1]` (1 >= 2) is False. Cookie too small. `child_idx` remains 1, `cookie_idx` becomes 2. |
| 3 | `child_idx = 1`, `cookie_idx = 2` | `cookie_idx == len(s)`. Loop terminates. Result is `child_idx = 1`. |

---

## Edge Cases

- `len(s) == 0`: No cookies available; loop exits immediately, returns `0`.
- `len(g) == 0`: No children to satisfy; returns `0`.
- All cookie sizes smaller than minimum greed: Returns `0`.
- All cookie sizes larger than maximum greed: Satisfies `min(len(g), len(s))` children.

---

## Mistakes

- User Mistake: No specific note provided.
- Forgetting to sort both arrays before applying the two-pointer greedy traversal.
- Wasting larger cookies on children with low greed instead of using the smallest possible matching cookie.
- Incrementing `child_idx` when a cookie is insufficient (cookie is consumed/skipped, not the child).

---

## Complexity

Time: O(N log N + M log M) → dominated by sorting both arrays of sizes N and M.
Space: O(1) or O(N + M) → auxiliary space depends on the sorting algorithm implementation.

---

## Similar Problems

- [Array Partition](https://leetcode.com/problems/array-partition/) - Easy
- [Maximum Units on a Truck](https://leetcode.com/problems/maximum-units-on-a-truck/) - Easy
- [Boats to Save People](https://leetcode.com/problems/boats-to-save-people/) - Medium
- [Bag of Tokens](https://leetcode.com/problems/bag-of-tokens/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #greedy #twopointers #sorting
- [[Greedy]] [[Two Pointers]] [[Sorting]]
- **Last Revised:** 2026-09-19
- **Problem Link:** [Assign Cookies - LeetCode](https://leetcode.com/problems/assign-cookies/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-21)
- [ ] Day 7 Revision (2026-09-26)
- [ ] Day 15 Revision (2026-10-04)
- [ ] Day 30 Revision (2026-10-19)
