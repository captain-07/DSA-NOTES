---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Check If The Number Is Armstrong

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Infosys #TCS #Wipro

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]]
  - #digit-manipulation [[Digit Manipulation]]

---
## Pattern

Digit Extraction + Power Summation

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

An Armstrong number of $n$ digits is equal to the sum of its digits each raised to the power $n$. The process involves two passes or using `log10` to find the digit count first, then summing the powers.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Count digits ($k$), extract digits using `% 10`, and accumulate `digit ** k`. Compare result to the original input.

---

## Approach

### Brute Force
- Convert number to string to find length and iterate through characters.
- Time: $O(\text{digits})$, Space: $O(\text{digits})$ for string storage.

### Optimal (Math-based)
- **Step 1:** Count digits using `floor(log10(n) + 1)` or a simple loop.
- **Step 2:** Extract each digit using `% 10`, raise to the power, and add to sum.
- **Step 3:** Use integer division `// 10` to move to the next digit.
- **Step 4:** Return `sum == original_number`.

---

## Code (Python)

```python
import math

class Solution:
    def isArmstrong(self, n: int) -> bool:
        # Step 1: Handle non-positive edge cases
        if n < 0: return False
        
        # Step 2: Calculate number of digits
        temp = n
        num_digits = len(str(n)) # Simple way, or use math.log10(n) + 1
        
        # Step 3: Calculate Armstrong sum
        total_sum = 0
        while temp > 0:
            digit = temp % 10
            total_sum += pow(digit, num_digits)
            temp //= 10
            
        return total_sum == n
```

---

## Dry Run (Smart Example)

**Input:** `n = 153`
**Digits ($k$):** 3

| Step | Current `temp` | Digit (`temp % 10`) | Calculation | `total_sum` |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 153 | 3 | $3^3 = 27$ | 27 |
| 2 | 15 | 5 | $5^3 = 125$ | 152 |
| 3 | 1 | 1 | $1^3 = 1$ | 153 |
| 4 | 0 | - | Loop Ends | **153 == 153 (True)** |

---

## Edge Cases

- **Single Digits (0-9):** Always Armstrong ($n^1 = n$).
- **Large Numbers:** Ensure power calculation doesn't cause overflow (not an issue in Python).
- **Negative Numbers:** Typically not Armstrong by definition.
- **10, 100, etc.:** Powers of 10 are rarely Armstrong (except 1).

---

## Mistakes

- **Hardcoding Power:** Using power of 3 for all numbers (only works for 3-digit numbers).
- **Modifying Input:** Forgetting to store the original `n` in a `temp` variable before the loop.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(\log_{10} N)$ → We process each digit of the number once.  
Space: $O(1)$ → Only a few integer variables used regardless of input size.

---

## Similar Problems

- [Palindrome Number](https://leetcode.com/problems/palindrome-number/) - Easy
- [Reverse Integer](https://leetcode.com/problems/reverse-integer/) - Medium
- [Sum of Digits in Base K](https://leetcode.com/problems/sum-of-digits-in-base-k/) - Easy

---

## Tags and Properties
- #dsa #important #revisit  
- #math #digits  
- [[Math]] [[Digit Manipulation]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [Armstrong Numbers - GFG](https://www.geeksforgeeks.org/problems/armstrong-numbers2727/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
