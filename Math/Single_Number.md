---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Find The Number That Appears Once, And Other Numbers Twice

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #bitmanipulation [[Bit Manipulation]]
  - #array [[Array]]
  - #hashmap [[HashMap]]

---
## Pattern

Bit Manipulation (XOR Properties)  

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The **XOR operator (`^`)** is the key. It has two critical properties:
1.  **Identity:** `x ^ 0 = x`
2.  **Self-Cancellation:** `x ^ x = 0`
Since XOR is commutative and associative, XORing all numbers together cancels out every pair, leaving only the unique number.

---

## ⚡ Quick Recall (VERY IMPORTANT)

XOR all elements in a single pass. The result is the "last man standing."

---

## Approach

### Brute Force
- Iterate through the array; for each element, count its occurrences using another loop.
- **Time:** O(N²)
- **Space:** O(1)

### Better
- Use a HashMap to store frequencies of each number. Iterate again to find the key with value 1.
- **Time:** O(N)
- **Space:** O(N)

### Optimal
- Initialize `res = 0`.
- Iterate through the array and update `res ^= num`.
- Return `res`.
- **Time:** O(N)
- **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def singleNumber(self, nums: list[int]) -> int:
        """
        Optimal solution using XOR Bit Manipulation.
        XORing a number with itself results in 0.
        XORing a number with 0 results in the number itself.
        """
        unique_num = 0
        
        for num in nums:
            # XOR every number in the array
            unique_num ^= num
            
        return unique_num
```

---

## Dry Run (Smart Example)

Input: `nums = [4, 1, 2, 1, 2]`

| Step | Current Num | XOR Operation | Result (`res`) | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| Init | - | - | 0 | Start with 0 |
| 1 | 4 | `0 ^ 4` | 4 (100₂) | First element stored |
| 2 | 1 | `4 ^ 1` | 5 (101₂) | Intermediate state |
| 3 | 2 | `5 ^ 2` | 7 (111₂) | Intermediate state |
| 4 | 1 | `7 ^ 1` | 6 (110₂) | 1 effectively cancels out |
| 5 | 2 | `6 ^ 2` | 4 (100₂) | 2 effectively cancels out |

---

## Edge Cases

- **Single Element:** `[5]` → XOR returns 5.
- **Negative Numbers:** `[-1, -1, -2]` → XOR works bitwise, correctly returns -2.
- **Large Arrays:** Works efficiently in O(N) regardless of size.
- **All Pairs + One:** Guaranteed by problem constraints.

---

## Mistakes

- **User Mistake:** No specific note provided.
- Attempting to use Sorting (O(N log N)) when O(N) is requested.
- Using extra space (HashMap) when O(1) space is the interview expectation.
- Forgetting that XOR is order-independent (commutative).

---

## Complexity

Time: O(N) → Single linear scan through the array.  
Space: O(1) → Only one integer variable used for tracking XOR result.

---

## Similar Problems

- [Single Number II](https://leetcode.com/problems/single-number-ii/) - Medium
- [Single Number III](https://leetcode.com/problems/single-number-iii/) - Medium
- [Missing Number](https://leetcode.com/problems/missing-number/) - Easy
- [Find the Difference](https://leetcode.com/problems/find-the-difference/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #bitmanipulation #interview-classic
  - [[Bit Manipulation]] [[Arrays]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Single Number](https://leetcode.com/problems/single-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
