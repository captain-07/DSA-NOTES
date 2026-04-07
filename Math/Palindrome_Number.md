---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Palindrome Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Facebook #Adobe #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]], #twopointers [[Two Pointers]]

## Pattern

Math (Digit Manipulation)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

- **Negative numbers** are never palindromes (e.g., `-121` reversed is `121-`).
- To avoid **integer overflow** when reversing, reverse only the **second half** of the number and compare it to the first half.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Negative? `False`. Ends in 0 (but not 0)? `False`.
- Compare `x` with `reversed_half` until `x <= reversed_half`.

---

## Approach

### Brute Force (String Conversion)
- Convert the integer to a string and check if it reads the same forwards and backwards.
- **Time:** O(log₁₀N) | **Space:** O(log₁₀N) (to store the string).

### Optimal (Reversing Half the Number)
1. Handle base cases: negatives and multiples of 10 (except 0) are not palindromes.
2. Extract the last digit of `x` using `% 10` and add it to `revertedNumber`.
3. Truncate `x` using `// 10`.
4. Stop when `x <= revertedNumber`.
5. For even length: `x == revertedNumber`. For odd length: `x == revertedNumber // 10`.

---

## Code (Python)

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        # Base cases: 
        # 1. Negative numbers are not palindromes
        # 2. If the last digit is 0, the first must be 0 (only 0 itself qualifies)
        if x < 0 or (x % 10 == 0 and x != 0):
            return False
        
        reverted_num = 0
        while x > reverted_num:
            # Pop last digit and push to reverted_num
            reverted_num = (reverted_num * 10) + (x % 10)
            x //= 10
            
        # For even length: x == reverted_num
        # For odd length: x == reverted_num // 10 (middle digit doesn't matter)
        return x == reverted_num or x == reverted_num // 10
```

---

## Dry Run (Input: 1221)

| Step | x | reverted_num | Explanation |
| :--- | :--- | :--- | :--- |
| Start | 1221 | 0 | Initial state. |
| 1 | 122 | 1 | Pop 1, x becomes 122, reverted_num becomes 1. |
| 2 | 12 | 12 | Pop 2, x becomes 12, reverted_num becomes 12. |
| End | 12 | 12 | `x` is no longer `> reverted_num`. Loop breaks. |
| Result | True | - | `x == reverted_num` (12 == 12) is True. |

---

## Edge Cases

- **Negative Numbers (-121):** Instantly return `False`.
- **Single Digits (0-9):** Always `True`.
- **Multiples of 10 (10, 100):** Return `False` (ends in 0, but doesn't start with 0).
- **Large Palindrome (2147447412):** Half-reversal prevents overflow issues in languages with fixed integer sizes.

---

## Mistakes

- **User mistake:** No specific note provided.
- Forgetting that negative numbers cannot be palindromes due to the minus sign.
- Reversing the entire number without checking for overflow (though Python handles large ints, this is bad practice in C++/Java).
- Not handling the middle digit in odd-length numbers correctly (e.g., `121` becomes `x=1`, `reverted=12`).

---

## Complexity

- **Time:** O(log₁₀N) → We divide the input by 10 in every iteration.
- **Space:** O(1) → We only store a few integer variables.

---

## Similar Problems

- [Reverse Integer](https://leetcode.com/problems/reverse-integer/) - Medium
- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) - Easy
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #math #logic
- [[Math]] [[Two Pointers]]
- **Revision Date:** 2026-04-07
- **Problem Link:** [LeetCode - Palindrome Number](https://leetcode.com/problems/palindrome-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
