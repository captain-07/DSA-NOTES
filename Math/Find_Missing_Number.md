---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Find Missing Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]]
  - #bit-manipulation [[Bit Manipulation]]
  - #arrays [[Arrays]]

## Pattern
Mathematical (Summation) or Bit Manipulation (XOR)

---
## Difficulty
Easy
#easy

---

## ⚡ Key Idea (Core Insight)
The array contains $n$ distinct numbers from a range of size $n+1$ (0 to $n$). The missing number is the difference between the **expected** sum of the range and the **actual** sum of the array, or the result of XORing all numbers and indices.

---

## ⚡ Quick Recall (VERY IMPORTANT)
`Expected_Sum - Actual_Sum` OR `XOR(all indices) ^ XOR(all values)`.

---

## Approach

### Brute Force
Sort the array and iterate to find the first index $i$ where `nums[i] != i`. 
Time: $O(N \log N)$ | Space: $O(1)$ or $O(N)$ depending on sort.

### Better
Use a HashSet to store all numbers in `nums`. Iterate from $0$ to $n$ and return the first number not in the set.
Time: $O(N)$ | Space: $O(N)$

### Optimal
1. **Sum Method:** Calculate `total = n*(n+1)//2`. Subtract every element in `nums` from `total`. The remainder is the answer.
2. **XOR Method:** XOR all numbers from $0$ to $n$ and all numbers in the array. Since $x \oplus x = 0$, only the missing number remains.
Time: $O(N)$ | Space: $O(1)$

---

## Code (Python)

```python
class Solution:
    def missingNumber(self, nums: list[int]) -> int:
        # Optimal Approach 1: Summation (Gauss Formula)
        n = len(nums)
        expected_sum = n * (n + 1) // 2
        actual_sum = sum(nums)
        return expected_sum - actual_sum

    def missingNumberXOR(self, nums: list[int]) -> int:
        # Optimal Approach 2: XOR logic
        res = len(nums)
        for i, val in enumerate(nums):
            res ^= i ^ val
        return res
```

---

## Dry Run (Smart Example)

**Input:** `nums = [3, 0, 1]` ($n=3$)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `n = 3` | Array length is 3, range is [0, 1, 2, 3]. |
| 2 | `expected = 3*(4)//2 = 6` | Sum of numbers from 0 to 3. |
| 3 | `actual = 3 + 0 + 1 = 4` | Sum of elements present in the array. |
| 4 | `6 - 4 = 2` | The difference is the missing number. |

---

## Edge Cases
- **Missing 0:** Array is `[1, 2, 3]`, expected sum is 6, actual is 6? No, $n=3$, sum(0..3) is 6. Actual sum is 6. Wait, if $n=3$ and array is `[1,2,3]`, sum is 6, diff is 0. Correct.
- **Missing $n$:** Array is `[0, 1, 2]`, expected sum is 6, actual is 3, diff is 3. Correct.
- **Single Element:** `nums = [0]`, $n=1$, expected $1*(2)//2 = 1$, actual 0, diff 1. Correct.

---

## Mistakes
- Integer overflow in languages like C++/Java (use XOR or subtract as you go if $n$ is massive).
- Off-by-one errors with $n$ vs $n+1$.
- **User Mistake:** No specific note provided.

---

## Complexity
Time: O(N) → Single pass through the array.  
Space: O(1) → Only constant extra space for variables.

---

## Similar Problems
- [Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/) - Easy
- [Single Number](https://leetcode.com/problems/single-number/) - Easy
- [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #arrays #math 
- [[Bit Manipulation]] [[Gauss Sum]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode - Missing Number](https://leetcode.com/problems/missing-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
