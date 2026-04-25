---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Count All Digits Of A Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #TCS #Zoho #Accenture

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]]
  - #basics [[Basic Algorithms]]

## Pattern

Repeated Division (Iterative)
Logarithmic Calculation (Constant Time)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The number of digits in $N$ is equivalent to how many times $N$ can be divided by 10 before reaching zero. Mathematically, this is $\lfloor \log_{10}(N) \rfloor + 1$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Iterate `n //= 10` until 0 OR use `int(math.log10(n) + 1)` for $N > 0$.

---

## Approach

### Brute Force
- Convert the number to a string and return its length.
- Time: $O(D)$ where $D$ is the number of digits.
- Space: $O(D)$ to store the string representation.

### Better (Iterative)
- Use a `while` loop to divide the number by 10 repeatedly.
- Increment a counter in each iteration.
- Handle $N=0$ as a special case (1 digit).

### Optimal (Mathematical)
- Use `math.log10(n)` to find the power of 10.
- Result is `floor(log10(n)) + 1`.
- Note: Only works for $N > 0$.

---

## Code (Python)

```python
import math

class Solution:
    def countDigitsIterative(self, n: int) -> int:
        # Handle 0 explicitly
        if n == 0: return 1
        # Handle negative numbers
        n = abs(n)
        
        count = 0
        while n > 0:
            n //= 10
            count += 1
        return count

    def countDigitsOptimal(self, n: int) -> int:
        if n == 0: return 1
        n = abs(n)
        # log10(n) + 1 gives the exact count
        return int(math.log10(n) + 1)
```

---

## Dry Run (Smart Example)

**Input:** `n = 156`

| Step | n (Value) | count | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 156 | 0 | Initial state |
| 2 | 15 | 1 | 156 // 10 = 15, count incremented |
| 3 | 1 | 2 | 15 // 10 = 1, count incremented |
| 4 | 0 | 3 | 1 // 10 = 0, count incremented. Loop ends. |

---

## Edge Cases

- **n = 0**: The loop might not execute; must return 1.
- **n = Negative**: Convert to absolute value before processing.
- **Large Integers**: Ensure the language handles large integers (Python does automatically).
- **Single Digit**: `n = 5` should return 1.

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Off-by-one:** Forgetting to handle `n=0` separately in iterative or log approaches.
- **Precision:** Relying on float-based `log10` for extremely large numbers without checking precision limits.
- **Negative Numbers:** Forgetting that `-123` still has 3 digits.

---

## Complexity

Time: O(log₁₀N) → The number of divisions is proportional to the number of digits.  
Space: O(1) → Only a single counter variable is used.

---

## Similar Problems

- [Palindrome Number](https://leetcode.com/problems/palindrome-number/) - Easy
- [Reverse Integer](https://leetcode.com/problems/reverse-integer/) - Medium
- [Number of Steps to Reduce a Number to Zero](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #math #digits #logic
  - [[Math]] [[Basic Programming]]
  - **Problem Link:** [GeeksforGeeks: Count Digits](https://www.geeksforgeeks.org/problems/count-digits5716/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
