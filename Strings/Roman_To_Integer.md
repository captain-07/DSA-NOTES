---
created: 2026-05-01
revisions:
  - 2026-05-03
  - 2026-05-08
  - 2026-05-16
  - 2026-05-31
---

# Roman To Integer

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Apple #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]]
  - #string [[String]]
  - #math [[Math]]

## Pattern
Hash Map + Look-ahead Comparison  
Right-to-Left Accumulation

---
## Difficulty
Easy  
#easy

---

## ⚡ Key Idea (Core Insight)
Roman numerals are generally additive. The "subtractive rule" triggers **only** when a numeral of smaller value precedes a numeral of larger value (e.g., IV where I < V). To solve, compare the current character's value with the next one.

---

## ⚡ Quick Recall (VERY IMPORTANT)
Iterate through the string: if `val(i) < val(i+1)`, subtract `val(i)`; otherwise, add it.

---

## Approach

### Brute Force
- Manually check every possible subtractive pair (IV, IX, XL, XC, CD, CM) using string replacement or nested `if-else` blocks.
- Time: O(N) | Space: O(N) due to string copies.

### Optimal
1. Store Roman-to-Integer mappings in a Hash Map.
2. Iterate through the string from left to right.
3. If the current value is less than the next value, it's a subtractive case: subtract current from total.
4. Otherwise, add the current value to total.
5. Handle the last character separately or by checking bounds.
- Time: O(N) | Space: O(1) (Hash Map size is constant).

---

## Code (Python)

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        # Fixed mapping of Roman symbols to values
        roman_map = {
            'I': 1, 'V': 5, 'X': 10, 'L': 50,
            'C': 100, 'D': 500, 'M': 1000
        }
        
        total = 0
        n = len(s)
        
        for i in range(n):
            # If current value < next value, subtract it
            if i + 1 < n and roman_map[s[i]] < roman_map[s[i+1]]:
                total -= roman_map[s[i]]
            else:
                total += roman_map[s[i]]
                
        return total
```

---

## Dry Run (Smart Example)
**Input:** `s = "MCMXCIV"` (1994)

| Step | Index | Char | Comparison | Action | Total |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | M | 1000 > 100 (C) | +1000 | 1000 |
| 2 | 1 | C | 100 < 1000 (M) | -100 | 900 |
| 3 | 2 | M | 1000 > 10 (X) | +1000 | 1900 |
| 4 | 3 | X | 10 < 100 (C) | -10 | 1890 |
| 5 | 4 | C | 100 > 1 (I) | +100 | 1990 |
| 6 | 5 | I | 1 < 5 (V) | -1 | 1989 |
| 7 | 6 | V | Last Char | +5 | 1994 |

---

## Edge Cases
- **Single Character:** `s = "I"` → Returns 1 immediately.
- **Identical Characters:** `s = "III"` → Always adds (1+1+1).
- **Max Value:** `s = "MMMCMXCIX"` → Correctly handles multiple subtractive pairs.
- **Smallest Subtractive:** `s = "IV"` → Returns 4.

---

## Mistakes
- **Index Out of Bounds:** Forgetting to check `i + 1 < n` before looking ahead.
- **Wrong Logic:** Adding when you should subtract (e.g., treating IV as 6).
- **User Mistake:** No specific note provided.

---

## Complexity
Time: O(N) → We traverse the string exactly once.  
Space: O(1) → The Hash Map size is fixed (7 symbols), and we only use a few integer variables.

---

## Similar Problems
- [Integer to Roman](https://leetcode.com/problems/integer-to-roman/) - Medium
- [Roman to Integer II (Validation)](https://leetcode.com/problems/roman-to-integer/) - Medium
- [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) - Easy

---

## Tags and Properties
- #dsa #important #revisit
- #string [[String]]
- #hashmap [[HashMap]]
- **Revision Date:** 2026-05-01
- **Problem Link:** [LeetCode: Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-03)
- [ ] Day 7 Revision (2026-05-08)
- [ ] Day 15 Revision (2026-05-16)
- [ ] Day 30 Revision (2026-05-31)
