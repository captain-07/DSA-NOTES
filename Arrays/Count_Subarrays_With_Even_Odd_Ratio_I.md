---
created: 2026-08-03
revisions:
  - 2026-08-05
  - 2026-08-10
  - 2026-08-18
  - 2026-09-02
---

# Count Subarrays With Even Odd Ratio I

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Uber

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #prefix-sum [[Prefix Sum]], #fenwick-tree [[Fenwick Tree]], #hashmap [[HashMap]]

## Pattern

Prefix Sum + HashMap / Fenwick Tree

---
## Difficulty

Medium | #medium

---
## ⚡ Key Idea (Core Insight)

Convert the ratio constraint $\text{even\_count} / \text{odd\_count} \le k$ into a prefix sum inequality: $\text{even\_count} - k \times \text{odd\_count} \le 0$.
Assign even numbers a value of $+1$ and odd numbers a value of $-k$. The problem reduces to counting subarrays with sum $\le 0$.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Transform array ($Even \to 1$, $Odd \to -k$). Compute prefix sums and count indices $i < j$ such that $P[i] \ge P[j]$.

---
## Approach

### Brute Force
Check all subarrays, count even and odd numbers, and verify the ratio.
- **Time Complexity:** $O(N^3)$
- **Space Complexity:** $O(1)$

### Better (No Fenwick Tree - Highly Intuitive)
Transform the array, build the prefix sums, and count pairs $P[i] \ge P[j]$ using two nested loops.
- **Time Complexity:** $O(N^2)$
- **Space Complexity:** $O(N)$
- *Note:* Highly preferred in interview situations due to its simplicity and readability.

### Optimal (Fenwick Tree / BIT)
Use a Fenwick tree (Binary Indexed Tree) to count the number of elements in prefix sum array that are $\ge P[j]$ in $O(\log N)$ time per element, utilizing coordinate compression.
- **Time Complexity:** $O(N \log N)$
- **Space Complexity:** $O(N)$

---
## Code (Python)

```python
class Solution:
    def countSubarraysN2(self, nums: list[int], k: int) -> int:
        # O(N^2) Solution: Understandable and interview-friendly
        n = len(nums)
        transformed = [1 if x % 2 == 0 else -k for x in nums]

        # Build prefix sums
        pref = [0] * (n + 1)
        for i in range(n):
            pref[i + 1] = pref[i] + transformed[i]

        ans = 0
        # Count pairs pref[i] >= pref[j] for i < j
        for j in range(1, n + 1):
            for i in range(j):
                if pref[i] >= pref[j]:
                    ans += 1
        return ans

    def countSubarraysOptimal(self, nums: list[int], k: int) -> int:
        # O(N log N) Solution using Fenwick Tree
        n = len(nums)
        transformed = [1 if x % 2 == 0 else -k for x in nums]

        pref = [0] * (n + 1)
        for i in range(n):
            pref[i + 1] = pref[i] + transformed[i]

        # Coordinate compression
        unique_vals = sorted(list(set(pref)))
        val_map = {val: idx + 1 for idx, val in enumerate(unique_vals)}

        bit = [0] * (len(unique_vals) + 1)

        def update(idx: int, val: int):
            while idx < len(bit):
                bit[idx] += val
                idx += idx & -idx

        def query(idx: int) -> int:
            s = 0
            while idx > 0:
                s += bit[idx]
                idx -= idx & -idx
            return s

        ans = 0
        for idx, p in enumerate(pref):
            compressed_idx = val_map[p]
            if idx > 0:
                # Count elements strictly less than pref[j] and subtract from total
                less_than = query(compressed_idx - 1)
                ans += idx - less_than
            update(compressed_idx, 1)

        return ans
```

---
## Dry Run (Smart Example)

Input: `nums = [2, 1, 4]`, `k = 2`. Transformed: `[1, -2, 1]`. Prefix sums: `P = [0, 1, -1, 0]`.

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `j = 1` (P[1] = 1) | Pair (P[0]=0, P[1]=1) $\implies 0 \ge 1$ (False). Count = 0. |
| 2 | `j = 2` (P[2] = -1) | Pairs: (P[0], P[2]) $\implies 0 \ge -1$ (True), (P[1], P[2]) $\implies 1 \ge -1$ (True). Count = 2. |
| 3 | `j = 3` (P[3] = 0) | Pairs: (P[0], P[3]) $\implies 0 \ge 0$ (True), (P[1], P[3]) $\implies 1 \ge 0$ (True), (P[2], P[3]) $\implies -1 \ge 0$ (False). Count = 2 + 2 = 4. |

---
## Edge Cases

- **All Even Elements:** Sum is always positive; ratio is never satisfied. Count is 0.
- **All Odd Elements:** Sum is always negative; all subarrays are valid.
- **Empty Array / Size 1:** Correctly handled by the bounds of prefix sum array.

---
## Mistakes

- Over-engineering with a Fenwick Tree during a live interview when the $O(N^2)$ solution is much more understandable and sufficient for the constraints.
- Forgetting the base prefix sum $P[0] = 0$, which represents the empty subarray.
- Off-by-one errors when setting up Fenwick tree indexing.

---
## Complexity

Time: O(N^2) for the understandable solution; O(N log N) for the Fenwick Tree optimization.
Space: O(N) to store prefix sums and coordinate mapping.

---
## Similar Problems

- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium
- [Count Subarrays With Score Less Than K](https://leetcode.com/problems/count-subarrays-with-score-less-than-k/) - Hard
- [Count of Range Sum](https://leetcode.com/problems/count-of-range-sum/) - Hard

---
## Tags and Properties

- #dsa #important #revisit
- #subarray #prefixsum [[Prefix Sum]] [[Fenwick Tree]]
- **Revision Date:** 2026-08-03
- **Problem Link:** [Count Subarrays With Even Odd Ratio I](https://leetcode.com/problems/count-subarrays-with-even-odd-ratio-i/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-05)
- [ ] Day 7 Revision (2026-08-10)
- [ ] Day 15 Revision (2026-08-18)
- [ ] Day 30 Revision (2026-09-02)
