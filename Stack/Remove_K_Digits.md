---
created: 2026-08-08
revisions:
  - 2026-08-10
  - 2026-08-15
  - 2026-08-23
  - 2026-09-07
---

# Remove K Digits

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google
  - #Amazon
  - #Microsoft
  - #TikTok

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #monotonicstack [[Monotonic Stack]]
  - #greedy [[Greedy Algorithms]]
  - #string [[String]]

## Pattern

Monotonic Stack + Greedy

---
## Difficulty

Medium #medium

---
## ⚡ Key Idea (Core Insight)

To minimize the number, make the leftmost digits as small as possible. Use a monotonic increasing stack to iteratively remove peak digits (where `digit > next_digit`) from left to right.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Maintain a monotonic increasing stack. Pop elements from the stack while the current digit is smaller than the stack's top and removals are remaining ($k > 0$).

---
## Approach

### Brute Force
Generate all possible subsequences of length $n - k$ and find the lexicographically smallest one.
- **Time Complexity:** $O(\binom{n}{k} \cdot n)$

### Optimal (Monotonic Stack)
1. Iterate through each digit.
2. While stack is not empty, $k > 0$, and the top of stack is greater than the current digit, pop from the stack and decrement $k$.
3. Push current digit.
4. If $k > 0$ after the loop, slice off the remaining $k$ elements from the end of the stack (handles strictly increasing sequences like `"1234"`).
5. Convert stack to string, strip leading zeros, and return `"0"` if empty.

---
## Code (Python)

```python
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        stack = []

        # Maintain monotonic increasing order
        for digit in num:
            while k > 0 and stack and stack[-1] > digit:
                stack.pop()
                k -= 1
            stack.append(digit)

        # Truncate remaining k digits from the tail
        if k > 0:
            stack = stack[:-k]

        # Remove leading zeros and handle empty case
        result = "".join(stack).lstrip("0")
        return result if result else "0"
```

---
## Dry Run (Smart Example)

Input: `num = "10200"`, `k = 1`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Init | `stack = []`, `k = 1` | Initialize stack and count. |
| 1 | `digit = '1'`, `stack = ['1']` | Push `'1'`. |
| 2 | `digit = '0'`, `stack = ['0']`, `k = 0` | `'1' > '0'` and `k > 0`. Pop `'1'`, decrement `k` to `0`, push `'0'`. |
| 3 | `digit = '2'`, `stack = ['0', '2']` | `k = 0`, no removals left. Push `'2'`. |
| 4 | `digit = '0'`, `stack = ['0', '2', '0']` | Push `'0'`. |
| 5 | `digit = '0'`, `stack = ['0', '2', '0', '0']` | Push `'0'`. |
| End | `result = "200"` | Join stack -> `"0200"`. `lstrip("0")` yields `"200"`. |

---
## Edge Cases

- **Strictly Increasing (`num = "1234", k = 2`)**: Stack never pops inside loop. Slices last $k$ digits -> `"12"`.
- **All Identical (`num = "111", k = 1`)**: Truncates from the end -> `"11"`.
- **All Zeros (`num = "0000", k = 2`)**: Returns `"0"`.
- **Single/All Removed (`num = "9", k = 1`)**: Returns `"0"`.

---
## Mistakes

- **Tricky Edge Cases**: Edge cases are very tricky—always verify leading zeros, remaining $k$ at stack tail, and empty result fallbacks.
- **Unprocessed Removals**: Forgetting to slice `stack[:-k]` when the loop finishes but $k > 0$.
- **Incorrect Greedy Focus**: Pop logic must prioritize the leftmost peaks rather than global maximums.

---
## Complexity

Time: O(n) → Each digit is pushed and popped at most once.
Space: O(n) → Stack stores at most $n$ digits.

---
## Similar Problems

- [Create Maximum Number](https://leetcode.com/problems/create-maximum-number/) - Hard
- [Find the Most Competitive Subsequence](https://leetcode.com/problems/find-the-most-competitive-subsequence/) - Medium
- [Smallest Subsequence of Distinct Characters](https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #greedy #monotonicstack
- Concepts: [[Monotonic Stack]], [[Greedy Algorithms]], [[Strings]]
- **Revision Date:** 2026-08-08
- **Problem Link:** [LeetCode - Remove K Digits](https://leetcode.com/problems/remove-k-digits/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-10)
- [ ] Day 7 Revision (2026-08-15)
- [ ] Day 15 Revision (2026-08-23)
- [ ] Day 30 Revision (2026-09-07)
