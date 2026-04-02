---
created: 2026-04-02
revisions:
  - 2026-04-04
  - 2026-04-09
  - 2026-04-17
  - 2026-05-02
---

# Palindrome Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Adobe #Facebook #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]]
  - #string [[String Manipulation]]

## Pattern

Reversing Half the Number / Digit Extraction

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

A number is a palindrome if it reads the same forward and backward. To optimize, reverse only the **last half** of the digits and compare it to the first half. This avoids potential integer overflow and extra space.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Negatives are NEVER palindromes. If $x > 0$ and ends in 0, it's not a palindrome. Stop reversing when `original_x <= reversed_half`.

---

## Approach

### Brute Force
- Convert the integer to a string and check if `s == s[::-1]`.
- **Time:** $O(\log_{10} n)$ (number of digits)
- **Space:** $O(\log_{10} n)$ (to store the string)

### Better
- Reverse the entire integer using `% 10` and `* 10` logic. Compare `reversed_num == original_num`.
- **Time:** $O(\log_{10} n)$
- **Space:** $O(1)$

### Optimal (Reverse Half)
1. Handle base cases: negatives and numbers ending in 0 (except 0 itself) return `False`.
2. Extract digits from the end: `reversed_num = reversed_num * 10 + x % 10`.
3. Stop when `x <= reversed_num`.
4. For even digits, `x == reversed_num`. For odd digits, `x == reversed_num // 10`.

---

## Code (Python)

```python
def isPalindrome(x: int) -> bool:
    # Negatives and numbers ending in 0 (except 0) aren't palindromes
    if x < 0 or (x % 10 == 0 and x != 0):
        return False
    
    reverted_number = 0
    while x > reverted_number:
        # Extract last digit and build the reversed half
        reverted_number = reverted_number * 10 + x % 10
        x //= 10
        
    # x == reverted_number (even digits) 
    # x == reverted_number // 10 (odd digits, middle digit is ignored)
    return x == reverted_number or x == reverted_number // 10
```

---

## Dry Run (Smart Example)

Input: `x = 1221`

| Step | x | reverted_number | Explanation |
| :--- | :--- | :--- | :--- |
| Init | 1221 | 0 | Start. `x > reverted_number` (1221 > 0). |
| 1 | 122 | 1 | `1221 % 10 = 1`. `x` becomes 122. |
| 2 | 12 | 12 | `122 % 10 = 2`. `reverted` = 1*10 + 2 = 12. |
| End | 12 | 12 | `x` is no longer `> reverted`. Return `12 == 12` (True). |

---

## Edge Cases

- **Negative Numbers:** `-121` $\to$ `121-` (False).
- **Single Digits:** `5` is always a palindrome (True).
- **Trailing Zeros:** `10`, `100` $\to$ Start with 0, not a palindrome (False).
- **Zero itself:** `0` is a palindrome (True).
- **Large Integers:** Reversing half prevents overflow in languages with fixed `int` sizes.

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Missing Negatives:** Forgetting that `-121` is not a palindrome.
- **String Conversion:** Using `str(x)` when the interviewer asks for a mathematical solution.
- **Odd/Even Length:** Forgetting to handle the middle digit by `reverted_number // 10`.

---

## Complexity

Time: $O(\log_{10} n)$ → We iterate through half the digits of the number.  
Space: $O(1)$ → No extra data structures used; only a few variables.

---

## Tags and Properties
  - #dsa #important #revisit  
  - #math #palindrome #integers
  - [[Math]] [[Palindrome]]
  - Revision Date: 2026-04-02

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-04)
- [ ] Day 7 Revision (2026-04-09)
- [ ] Day 15 Revision (2026-04-17)
- [ ] Day 30 Revision (2026-05-02)
