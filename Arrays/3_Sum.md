---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# 3 Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #twopointers [[Two Pointers]]
  - #sorting [[Sorting]]
  - #arrays [[Arrays]]

---
## Pattern

Sorting + Two Pointers (Fixed Pivot)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

To avoid $O(N^3)$ and handle duplicates efficiently, **sort the array**. Fix one element `i` and treat the remaining problem as a **Target Sum (Two Sum II)** problem using two pointers on the suffix `[i+1, n-1]`.

---

## ⚡ Quick Recall

Sort → Fix `i` → Skip duplicate `i` → `L=i+1`, `R=n-1` → Skip duplicate `L`/`R` after finding a triplet.

---

## Approach

### Brute Force
- Triple nested loops checking every combination `(i, j, k)`.
- Use a `set` to store sorted triplets to ensure uniqueness.
- **Complexity:** $O(N^3 \log(\text{triplets}))$ time | $O(N)$ space.

### Better
- Use a HashMap to store frequencies.
- Fix two numbers and check if the third `-(a+b)` exists in the map.
- Still requires a set to handle unique triplets.
- **Complexity:** $O(N^2)$ time | $O(N)$ space.

### Optimal
1. **Sort** the input array.
2. Iterate through the array with pointer `i`.
3. If `nums[i] == nums[i-1]`, **skip** (prevents duplicate triplets).
4. Set `left = i + 1` and `right = len(nums) - 1`.
5. While `left < right`:
   - Calculate `total = nums[i] + nums[left] + nums[right]`.
   - If `total == 0`: Add to result, then move `left`/`right` while skipping duplicates.
   - If `total < 0`: Increment `left`.
   - If `total > 0`: Decrement `right`.

---

## Code (Python)

```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        res = []
        nums.sort()  # O(N log N)
        
        for i in range(len(nums)):
            # Optimization: If first element > 0, sum can never be 0
            if nums[i] > 0:
                break
            # Skip duplicate pivot elements
            if i > 0 and nums[i] == nums[i-1]:
                continue
            
            l, r = i + 1, len(nums) - 1
            while l < r:
                s = nums[i] + nums[l] + nums[r]
                if s < 0:
                    l += 1
                elif s > 0:
                    r -= 1
                else:
                    res.append([nums[i], nums[l], nums[r]])
                    # Move pointers and skip duplicates
                    while l < r and nums[l] == nums[l+1]:
                        l += 1
                    while l < r and nums[r] == nums[r-1]:
                        r -= 1
                    l += 1
                    r -= 1
        return res
```

---

## Dry Run (Smart Example)

Input: `[-1, 0, 1, 2, -1, -4]` | Sorted: `[-4, -1, -1, 0, 1, 2]`

| Step | `i` (Val) | `l`, `r` (Vals) | Sum | Action |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 0 (-4) | 1 (-1), 5 (2) | -3 | Sum < 0 → `l++` |
| 2 | 1 (-1) | 2 (-1), 5 (2) | 0 | **Found [-1,-1,2]**; `l++, r--` |
| 3 | 1 (-1) | 3 (0), 4 (1) | 0 | **Found [-1,0,1]**; `l++, r--` |
| 4 | 2 (-1) | N/A | - | `nums[2]==nums[1]` → Skip |

---

## Edge Cases

- **Length < 3:** Return `[]`.
- **All Zeros:** `[0, 0, 0]` should return `[[0, 0, 0]]`.
- **No triplets:** Return `[]`.
- **All Positives/Negatives:** No solution possible (optimization: `nums[i] > 0` break).

---

## Mistakes

- Forgetting to **sort** the array first.
- Not skipping duplicates for the **pivot** `i`.
- Not skipping duplicates for `left` and `right` **after** finding a valid triplet.
- **User Mistake:** No specific note provided (ensure logic is visualized clearly next time).

---

## Complexity

Time: $O(N^2)$ → Sorting takes $O(N \log N)$, outer loop $N$ times with a $O(N)$ two-pointer scan.  
Space: $O(1)$ or $O(N)$ → Depending on the sorting implementation's space complexity.

---

## Similar Problems

- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Easy
- [3Sum Closest](https://leetcode.com/problems/3sum-closest/) - Medium
- [4Sum](https://leetcode.com/problems/4sum/) - Medium
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #arrays #sorting
- [[Two Pointers]] [[Sorting]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode 3Sum](https://leetcode.com/problems/3sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
