---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Find Nth Root Of A Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Samsung #Adobe #Flipkart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #mathematics [[Mathematics]]

## Pattern

Binary Search on Answer Space  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The function $f(x) = x^n$ is **monotonically increasing** for $x \ge 1$. Since the range of possible answers $[1, m]$ is sorted, we can use Binary Search to find the value $x$ such that $x^n = m$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Search for the root in the range $[1, m]$. If $mid^n > m$, the root lies to the left; if $mid^n < m$, it lies to the right. Use a helper or direct power comparison to handle potential overflow in non-Python languages.

---

## Approach

### Brute Force
- Linearly check every integer $i$ from $1$ to $m$. Compute $i^n$ and stop if it equals or exceeds $m$.
- Time Complexity: $O(m \cdot \log n)$

### Better
- Use **Newton-Raphson Method** for approximation (more common in numerical analysis than standard DSA interviews).
- Time Complexity: $O(\log(\text{precision}))$

### Optimal
- **Binary Search on Answer**:
  1. Initialize `low = 1`, `high = m`.
  2. Calculate `mid = (low + high) // 2`.
  3. Compute `val = mid**n`.
  4. If `val == m`, return `mid`.
  5. If `val < m`, update `low = mid + 1`.
  6. If `val > m`, update `high = mid - 1`.
  7. If loop ends without finding `m`, return -1.

---

## Code (Python)

```python
def find_nth_root(n, m):
    # Search space for the root
    low = 1
    high = m
    
    while low <= high:
        mid = (low + high) // 2
        # Calculate mid^n
        val = mid ** n
        
        if val == m:
            return mid # Found exact integer root
        
        if val < m:
            low = mid + 1 # Target is higher
        else:
            high = mid - 1 # Target is lower
            
    return -1 # No integer root exists
```

---

## Dry Run (Smart Example)

**Input:** `n = 3, m = 27` (Finding Cube Root of 27)

| Step | low | high | mid | mid^n vs m | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 27 | 14 | 2744 > 27 | mid^3 is way too high, move high to 13. |
| 2 | 1 | 13 | 7 | 343 > 27 | 7^3 is still too high, move high to 6. |
| 3 | 1 | 6 | 3 | 27 == 27 | 3^3 matches m exactly. Return 3. |

---

## Edge Cases

- **m = 1**: Always returns 1 regardless of $n$.
- **n = 1**: The $n^{th}$ root of $m$ is $m$ itself.
- **No Perfect Root**: e.g., $n=2, m=5$ should return -1.
- **Large n**: $mid^n$ can grow extremely fast; Python handles this, but C++/Java needs overflow checks.

---

## Mistakes

- **Overflow Errors**: In languages like C++, `pow(mid, n)` will overflow `long long`. Use a custom comparison function that returns early if the product exceeds $m$.
- **Range limit**: Starting `high` at $m$ is safe, but for $n \ge 2$, the root is often much smaller than $m$.
- **User Mistake**: No specific note provided.

---

## Complexity

Time: $O(\log m \cdot \log n)$ → $\log m$ for binary search range, $\log n$ for the power calculation.  
Space: $O(1)$ → No extra data structures used.

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch [[Binary Search]] #math [[Mathematics]] #integers 
  - Revision Date: 2026-04-07
  - Related: [[Square Root of a Number]], [[Pow(x, n)]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
