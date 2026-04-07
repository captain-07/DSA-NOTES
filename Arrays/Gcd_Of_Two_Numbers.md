---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Gcd Of Two Numbers

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #Google #TCS #Infosys

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]], #recursion [[Recursion]], #euclidean-algorithm [[Euclidean Algorithm]]

## Pattern

Euclidean Algorithm (Division-based)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

The GCD of two numbers does not change if the larger number is replaced by its remainder when divided by the smaller number.  
**Formula:** `gcd(a, b) = gcd(b, a % b)` until `b` becomes `0`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use **Euclidean Algorithm**: Continuously replace `(a, b)` with `(b, a % b)` until the remainder is `0`. The last non-zero divisor is the GCD.

---

## Approach

### Brute Force
- Iterate from `min(a, b)` down to `1`. The first number that divides both `a` and `b` is the GCD.
- **Time Complexity:** O(min(a, b))

### Better
- Iterate from `1` to `sqrt(min(a, b))` to find factors, but this is unnecessarily complex for GCD compared to the optimal approach.

### Optimal (Euclidean Algorithm)
1. If `b == 0`, return `a`.
2. Otherwise, recursively call `gcd(b, a % b)`.
3. Alternatively, use an iterative loop to update `a, b = b, a % b`.

---

## Code (Python)

```python
def gcd(a, b):
    # Iterative Euclidean Algorithm
    while b:
        # a becomes b, and b becomes the remainder of a / b
        a, b = b, a % b
    return a

# Example Usage:
# print(gcd(48, 18)) # Output: 6
```

---

## Dry Run (Smart Example)

**Input:** `a = 48, b = 18`

| Step | a | b | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 48 | 18 | Initial values. `48 % 18 = 12`. |
| 2 | 18 | 12 | `a` becomes 18, `b` becomes 12. `18 % 12 = 6`. |
| 3 | 12 | 6 | `a` becomes 12, `b` becomes 6. `12 % 6 = 0`. |
| 4 | 6 | 0 | `b` is now 0. Return `a = 6`. |

---

## Edge Cases

- **One number is 0:** `gcd(4, 0)` is `4`.
- **Both numbers are same:** `gcd(10, 10)` is `10`.
- **Prime numbers:** `gcd(13, 7)` is `1`.
- **One number is 1:** `gcd(100, 1)` is `1`.

---

## Mistakes

- **Bullet points only**
- Forgetting that `gcd(a, 0) = a`.
- Using subtraction-based Euclidean algorithm (`a-b`) which is slower than division-based (`a%b`).
- **User mistake:** None.

---

## Complexity

Time: O(log(min(a, b))) → The number of steps in the Euclidean algorithm grows logarithmically with the value of the numbers.  
Space: O(1) → Iterative approach uses constant extra space. (Recursive uses O(log(min(a, b))) stack space).

---

## Similar Problems

- [LCM And GCD](https://www.geeksforgeeks.org/problems/lcm-and-gcd4516/1) - Easy
- [Greatest Common Divisor of Strings](https://leetcode.com/problems/greatest-common-divisor-of-strings/) - Easy
- [Find Greatest Common Divisor of Array](https://leetcode.com/problems/find-greatest-common-divisor-of-array/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #math #fundamentals
  - [[Euclidean Algorithm]] [[Number Theory]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [Gcd Of Two Numbers - GeeksforGeeks](https://www.geeksforgeeks.org/problems/gcd-of-two-numbers3459/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
