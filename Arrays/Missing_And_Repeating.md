---
created: 2026-03-24
revisions:
  - 2026-03-26
  - 2026-03-31
  - 2026-04-08
  - 2026-04-23
---

# Missing And Repeating

---

## Pattern

- Math (Summation & Squares)
- Bit Manipulation (XOR)
- Array Indexing (Sign Marking)

---

## ⚡ Key Idea (Core Insight)

Use the mathematical relationship between the sum of first $N$ natural numbers and the sum of their squares. By calculating the difference between the actual sums and expected sums, you create a system of two equations: $(A - B)$ and $(A^2 - B^2)$, where $A$ is the repeating and $B$ is the missing number.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Solve $X - Y = \text{diff\_sum}$ and $X^2 - Y^2 = \text{diff\_sq\_sum}$. Use $(X^2 - Y^2) / (X - Y) = X + Y$ to find the second linear equation.

---

## Approach

### Brute Force
- Use a frequency array or hash map to count occurrences.
- **Time:** $O(N)$ | **Space:** $O(N)$

### Better (Sorting)
- Sort the array and check adjacent elements for duplicates and gaps.
- **Time:** $O(N \log N)$ | **Space:** $O(1)$ (ignoring sort stack)

### Optimal (Math)
1. Calculate $S = \sum \text{arr}$ and $S_n = \sum_{i=1}^N i$. Let $D_1 = S - S_n = R - M$.
2. Calculate $S^2 = \sum \text{arr}^2$ and $S_n^2 = \sum_{i=1}^N i^2$. Let $D_2 = S^2 - S_n^2 = R^2 - M^2$.
3. Since $R^2 - M^2 = (R-M)(R+M)$, then $R+M = D_2 / D_1$.
4. Solve for $R$ (Repeating) and $M$ (Missing) using $D_1$ and the result from step 3.

---

## Code (Python)

```python
def findTwoElement(arr, n):
    # Sum of first N numbers and squares
    sn = (n * (n + 1)) // 2
    s2n = (n * (n + 1) * (2 * n + 1)) // 6
    
    s, s2 = 0, 0
    for x in arr:
        s += x
        s2 += x * x
        
    # val1 = R - M
    val1 = s - sn
    # val2 = R^2 - M^2
    val2 = s2 - s2n
    
    # val2 = (R - M)(R + M) => R + M = val2 / val1
    val2 = val2 // val1
    
    # R = ((R-M) + (R+M)) / 2
    repeating = (val1 + val2) // 2
    missing = val2 - repeating
    
    return [repeating, missing]
```

---

## Dry Run (Smart Example)

**Input:** `arr = [3, 1, 2, 5, 3]`, `N = 5`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `sn=15`, `s2n=55` | Expected sum (1..5) and sum of squares. |
| 2 | `s=14`, `s2=48` | Actual sum is 14, Actual sum of squares is $9+1+4+25+9=48$. |
| 3 | `val1 = -1` | $R - M = 14 - 15 = -1$. |
| 4 | `val2 = -7` | $R^2 - M^2 = 48 - 55 = -7$. |
| 5 | `R+M = 7` | $(-7) / (-1) = 7$. |
| 6 | `R=3, M=4` | Solve $R-M=-1$ and $R+M=7$. |

---

## Edge Cases

- **Repeating is 1, Missing is N:** Formula handles boundaries naturally.
- **Array already sorted:** No impact on math logic.
- **Large N:** Use large integer types to prevent overflow (Python handles this).
- **Repeating and Missing are adjacent:** e.g., `[1, 2, 2, 4]`.

---

## Mistakes

- **Integer Overflow:** In languages like C++/Java, use `long long` for sum of squares.
- **Division by Zero:** If using XOR approach, ensure the rightmost set bit is calculated correctly.
- **Incorrect Order:** Returning [Missing, Repeating] instead of [Repeating, Missing].
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Single pass to calculate sum and sum of squares.  
Space: O(1) → Only a few variables used for calculations.

---

## Difficulty

Medium  
#medium

---

- **Target Companies:**
  - #Amazon #GoldmanSachs #Microsoft #Google

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Mathematics]]
  - #arrays [[Arrays]]
  - #bitmanipulation [[Bit Manipulation]]

- **Tags:**
  - #dsa #important #revisit  
  - #equations [[System of Equations]]
  - #problemsolving [[Problem Solving]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-03-26)
- [ ] Day 7 Revision (2026-03-31)
- [ ] Day 15 Revision (2026-04-08)
- [ ] Day 30 Revision (2026-04-23)
