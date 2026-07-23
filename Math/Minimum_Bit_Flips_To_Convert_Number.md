---
created: 2026-07-23
revisions:
  - 2026-07-25
  - 2026-07-30
  - 2026-08-07
  - 2026-08-22
---

# Minimum Bit Flips To Convert Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Bloomberg

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #bitmanipulation [[Bit Manipulation]]
  - #bitwise [[Bitwise Operations]]

## Pattern
Bit Manipulation (XOR Difference + Bit Counting)

---
## Difficulty
Easy #easy

---
## ⚡ Key Idea (Core Insight)
The minimum bit flips to convert `start` to `goal` is equal to the number of positions where their bits differ. XORing `start ^ goal` outputs `1` only at these differing bit positions. Counting the set bits in the XOR result yields the answer.

---
## ⚡ Quick Recall (VERY IMPORTANT)
Calculate `start ^ goal` and count the set bits of the result using Brian Kernighan's algorithm (`n & (n - 1)`) or Python's `bit_count()`.

---
## Approach

### Brute Force
Convert both numbers to 32-character binary strings, pad with leading zeros, and compare them character by character.
- Time Complexity: O(1) (fixed 32 iterations)
- Space Complexity: O(1)

### Better
Iterate 32 times. In each iteration, extract the least significant bit of both numbers using `& 1`, compare them, and right-shift both numbers by 1.
- Time Complexity: O(1) (always 32 shifts)
- Space Complexity: O(1)

### Optimal

**Approach 1: XOR + Brian Kernighan’s Algorithm (Manual Counting)**
1. Compute `xor_result = start ^ goal`.
2. Clear the lowest set bit repeatedly using `xor_result = xor_result & (xor_result - 1)` until the value becomes `0`.
3. Count the number of operations.

**Approach 2: XOR + Built-in bit_count()**
1. Compute `xor_result = start ^ goal`.
2. Return `xor_result.bit_count()`.

---
## Code (Python)

```python
class Solution:
    def minBitFlips(self, start: int, goal: int) -> int:
        # Step 1: XOR to find differing bits
        xor_result = start ^ goal
        count = 0

        # Step 2: Clear the lowest set bit until xor_result becomes 0
        while xor_result > 0:
            xor_result &= (xor_result - 1)
            count += 1

        return count
```

---
## Dry Run (Smart Example)

Input: `start = 10` (binary `1010`), `goal = 7` (binary `0111`)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Init | `start = 10`, `goal = 7` | `10 ^ 7 = 13` (binary `1101`). |
| 1 | `xor_result = 13`, `count = 1` | `13 & 12 = 12` (binary `1100`). Rightmost set bit cleared. |
| 2 | `xor_result = 12`, `count = 2` | `12 & 11 = 8` (binary `1000`). Next set bit cleared. |
| 3 | `xor_result = 8`, `count = 3` | `8 & 7 = 0` (binary `0000`). Loop terminates. Return `3`. |

---
## Edge Cases
- `start == goal`: XOR is `0`, returns `0` instantly.
- `start = 0`: Flips needed equal the number of set bits in `goal`.
- Extreme values (`10^9`): Fits comfortably in standard 32-bit integer limits.

---
## Mistakes
- **Failing to explain Python's `bit_count()`:** Interviewers expect you to know that `int.bit_count()` (introduced in Python 3.10) is the optimal way to count set bits as it maps to the hardware-level `POPCNT` instruction. Do not use `bin(x).count('1')` without noting that it incurs memory overhead by allocating an intermediate string.
- **Operator Precedence:** Forgetting that bitwise operators like `^` and `&` have lower precedence than comparison operators (e.g., `start ^ goal == 0` evaluates as `start ^ (goal == 0)`). Use parentheses.

---
## Complexity
Time: O(1) → The numbers are bounded by 32 bits; the loop runs at most 30 times (since $10^9 < 2^{30}$).
Space: O(1) → Constant auxiliary space.

---
## Similar Problems
- [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/) - Easy
- [Hamming Distance](https://leetcode.com/problems/hamming-distance/) - Easy
- [Counting Bits](https://leetcode.com/problems/counting-bits/) - Easy

---
## Tags and Properties
  - #dsa #important #revisit
  - #bitmanipulation #bitwise #leetcode-easy
  - [[Bit Manipulation]] [[XOR]] [[Brian Kernighans Algorithm]]
  - Revision Date: 2026-07-23
  - **Problem Link:** [LeetCode - Minimum Bit Flips to Convert Number](https://leetcode.com/problems/minimum-bit-flips-to-convert-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-25)
- [ ] Day 7 Revision (2026-07-30)
- [ ] Day 15 Revision (2026-08-07)
- [ ] Day 30 Revision (2026-08-22)
