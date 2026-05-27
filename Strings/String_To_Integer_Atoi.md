---
created: 2026-05-01
revisions:
  - 2026-05-03
  - 2026-05-08
  - 2026-05-16
  - 2026-05-31
---

# String To Integer(Atoi)

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Facebook #LinkedIn #Bloomberg #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #strings [[Strings]]
  - #simulation [[Simulation]]
  - #overflow [[Integer Overflow]]

---
## Pattern

Sequential Character Processing + Boundary Simulation

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The problem is a **linear simulation** of string parsing rules. The "unlock" is the specific order of operations: 1. Discard Whitespace → 2. Determine Sign → 3. Read Digits → 4. Clamp to 32-bit range. You must stop immediately upon encountering a non-digit character after the sequence has started.

---

## ⚡ Quick Recall (VERY IMPORTANT)

**Trim → Sign → Digit-Loop → Clamp.** Use `res = res * 10 + digit` and check boundaries at every step or before final return.

---

## Approach

### Brute Force
- Using `int()` in a try-except block after manually slicing.
- Time: O(N) | Space: O(N) for slicing.

### Optimal
- **Single Pass Simulation:** Initialize an index pointer, skip spaces, identify the sign, and iterate through the string once to build the integer. Handle overflow using the constant limits $-2^{31}$ and $2^{31}-1$.
- Time: O(N) | Space: O(1)

---

## Code (Python)

```python
class Solution:
    def myAtoi(self, s: str) -> int:
        # Constants for 32-bit signed integer limits
        MAX_INT = 2**31 - 1
        MIN_INT = -2**31
        
        i, n = 0, len(s)
        res = 0
        sign = 1
        
        # 1. Skip leading whitespaces
        while i < n and s[i] == ' ':
            i += 1
            
        # 2. Check for sign
        if i < n and (s[i] == '+' or s[i] == '-'):
            sign = -1 if s[i] == '-' else 1
            i += 1
            
        # 3. Process digits
        while i < n and s[i].isdigit():
            digit = int(s[i])
            
            # Check for overflow before updating res
            if res > (MAX_INT - digit) // 10:
                return MAX_INT if sign == 1 else MIN_INT
                
            res = res * 10 + digit
            i += 1
            
        return max(MIN_INT, min(sign * res, MAX_INT))
```

---

## Dry Run (Smart Example)

**Input:** `s = " -042words"`

| Step | Index/Char | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `i=0, ' '` | `res=0, sign=1` | Skip leading whitespace. |
| 2 | `i=1, '-'` | `res=0, sign=-1` | Detect negative sign, increment `i`. |
| 3 | `i=2, '0'` | `res=0` | `0*10 + 0 = 0`. |
| 4 | `i=3, '4'` | `res=4` | `0*10 + 4 = 4`. |
| 5 | `i=4, '2'` | `res=42` | `4*10 + 2 = 42`. |
| 6 | `i=5, 'w'` | `res=42` | Non-digit found; break loop. |
| 7 | Result | `-42` | `sign * res` applied and clamped. |

---

## Edge Cases

- **Empty/Whitespace only:** Should return `0`.
- **Overflow/Underflow:** `"9223372036854775808"` should return `2147483647`.
- **Sign with no digits:** `"+"` or `"- "` should return `0`.
- **Leading Zeros:** `"0000123"` should return `123`.
- **Middle Non-digits:** `"4193 with words"` returns `4193`; `"words and 987"` returns `0`.

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Missing whitespace check:** Forgetting that only *leading* spaces are ignored.
- **Ordering:** Checking for sign *before* skipping spaces.
- **Late Break:** Continuing to read digits after a non-digit char (e.g., `"123a45"` should be `123`, not `12345`).
- **Python's `int` range:** Forgetting that Python handles arbitrarily large integers, so explicit clamping to 32-bit is required.

---

## Complexity

Time: O(N) → Single pass through the string of length N.  
Space: O(1) → Constant extra space used regardless of input size.

---

## Similar Problems

- [Reverse Integer](https://leetcode.com/problems/reverse-integer/) - Medium
- [Valid Number](https://leetcode.com/problems/valid-number/) - Hard
- [Multiply Strings](https://leetcode.com/problems/multiply-strings/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #simulation 
  - [[Strings]] [[Simulation]] [[Integer Overflow]]
  - **Revision Date:** 2026-05-01
  - **Problem Link:** [LeetCode - String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-03)
- [ ] Day 7 Revision (2026-05-08)
- [ ] Day 15 Revision (2026-05-16)
- [ ] Day 30 Revision (2026-05-31)
