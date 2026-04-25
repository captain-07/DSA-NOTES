---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Rearrange Array Elements By Sign

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Meta #Adobe #Google

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]]
  - #twopointers [[Two Pointers]]
  - #simulation [[Simulation]]

## Pattern

Two Pointers (Independent Indexing)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Since the array contains an equal number of positive and negative integers and relative order must be preserved, we can pre-allocate a result array and use two independent pointers (`pos_idx = 0`, `neg_idx = 1`) to place elements in a single pass.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Initialize `pos = 0`, `neg = 1`. Iterate once: if `num > 0`, place at `pos` and `pos += 2`; else place at `neg` and `neg += 2`.

---

## Approach

### Brute Force
- Separate all positive and negative numbers into two auxiliary lists, then merge them into the result array.
- **Time:** $O(N)$ | **Space:** $O(N)$

### Optimal
- Single-pass approach. Initialize an empty result array of size $N$. 
- Use two pointers to track the next available even (positive) and odd (negative) indices.
- **Time:** $O(N)$ | **Space:** $O(N)$ (Result array)

---

## Code (Python)

```python
class Solution:
    def rearrangeArray(self, nums: list[int]) -> list[int]:
        n = len(nums)
        # Pre-allocate result array for efficiency
        ans = [0] * n
        
        pos_idx, neg_idx = 0, 1
        
        for num in nums:
            if num > 0:
                ans[pos_idx] = num
                pos_idx += 2
            else:
                ans[neg_idx] = num
                neg_idx += 2
                
        return ans
```

---

## Dry Run (Smart Example)

**Input:** `nums = [3, 1, -2, -5, 2, -4]`

| Step | Current Num | `pos_idx` | `neg_idx` | `ans` state | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 3 | 0 -> 2 | 1 | `[3, 0, 0, 0, 0, 0]` | Positive: place at 0, move to 2 |
| 2 | 1 | 2 -> 4 | 1 | `[3, 0, 1, 0, 0, 0]` | Positive: place at 2, move to 4 |
| 3 | -2 | 4 | 1 -> 3 | `[3, -2, 1, 0, 0, 0]` | Negative: place at 1, move to 3 |
| 4 | -5 | 4 | 3 -> 5 | `[3, -2, 1, -5, 0, 0]` | Negative: place at 3, move to 5 |
| 5 | 2 | 4 -> 6 | 5 | `[3, -2, 1, -5, 2, 0]` | Positive: place at 4, move to 6 |
| 6 | -4 | 6 | 5 -> 7 | `[3, -2, 1, -5, 2, -4]` | Negative: place at 5, move to 7 |

---

## Edge Cases

- **Minimum Size:** `[1, -1]` - Should handle correctly with index increments.
- **Already Arranged:** `[1, -1, 2, -2]` - Algorithm logic remains identical.
- **All Positives first:** `[1, 2, 3, -1, -2, -3]` - Stability is key; pointers ensure relative order.

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Stability:** Forgetting that relative order must be preserved (cannot use standard partition logic like Quicksort).
- **In-place obsession:** Attempting $O(1)$ space. While possible, it usually leads to $O(N^2)$ time or complex pointer manipulation that violates the stability requirement.

---

## Complexity

Time: O(N) → Single traversal of the input array.  
Space: O(N) → Required for the output array (Extra space not used besides result).

---

## Similar Problems

- [Sort Colors](https://leetcode.com/problems/sort-colors/) - Medium
- [Move Zeroes](https://leetcode.com/problems/move-zeroes/) - Easy
- [Rotate Array](https://leetcode.com/problems/rotate-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #leetcode2149
  - [[Arrays]] [[Two Pointers]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Rearrange Array Elements By Sign](https://leetcode.com/problems/rearrange-array-elements-by-sign/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
