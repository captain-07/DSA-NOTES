---
created: 2026-07-17
revisions:
  - 2026-07-19
  - 2026-07-24
  - 2026-08-01
  - 2026-08-16
---

# Letter Combinations Of A Phone Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Uber

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #backtracking [[Backtracking]], #recursion [[Recursion]], #string [[String]]

---
## Pattern

Backtracking / DFS on Decision Tree

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

Map each digit to its corresponding letters. Construct combinations by traversing a decision tree where each level represents a digit in the input string, and each branch represents choosing one of the letters corresponding to that digit.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Backtracking DFS: Base case is `index == len(digits)`. Branch on each letter associated with `digits[index]`, building the string as you descend.

---
## Approach

### Brute Force
Generate all possible combinations of lowercase English letters of length `len(digits)` and filter out the ones that don't match the keypad mapping.
Time Complexity: O(26^N) where N is the length of digits.

### Optimal
#### Solution 1: Recursive Backtracking (DFS)
Use a helper method to traverse each digit choice. Append path to results when path length equals digit length.

#### Solution 2: Iterative BFS
Use a queue starting with an empty string. For each digit, pop the current combination queue and append each mapping character, pushing them back to form the next level's state.

---
## Code (Python)

```python
# Optimal 1: Recursive Backtracking
class Solution:
    def letterCombinations(self, digits: str) -> list[str]:
        if not digits:
            return []

        digit_to_char = {
            "2": "abc", "3": "def", "4": "ghi", "5": "jkl",
            "6": "mno", "7": "pqrs", "8": "tuv", "9": "wxyz"
        }

        res = []
        self._backtrack(0, "", digits, digit_to_char, res)
        return res

    def _backtrack(self, index: int, path: str, digits: str, digit_to_char: dict, res: list):
        if len(path) == len(digits):
            res.append(path)
            return

        for char in digit_to_char[digits[index]]:
            self._backtrack(index + 1, path + char, digits, digit_to_char, res)

# Optimal 2: Iterative BFS
class SolutionBFS:
    def letterCombinations(self, digits: str) -> list[str]:
        if not digits:
            return []

        digit_to_char = {
            "2": "abc", "3": "def", "4": "ghi", "5": "jkl",
            "6": "mno", "7": "pqrs", "8": "tuv", "9": "wxyz"
        }

        queue = [""]
        for digit in digits:
            next_queue = []
            for combo in queue:
                for char in digit_to_char[digit]:
                    next_queue.append(combo + char)
            queue = next_queue

        return queue
```

---
## Dry Run (Smart Example)

Input: `digits = "23"` (mappings: `2 -> "abc"`, `3 -> "def"`)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `index=0, path=""` | Current digit is '2'. Branch on 'a', 'b', 'c'. |
| 2 | `index=1, path="a"` | Current digit is '3'. Branch on 'd', 'e', 'f'. |
| 3 | `index=2, path="ad"` | Base case reached. Add `"ad"` to result. Backtrack. |
| 4 | `index=2, path="ae"` | Base case reached. Add `"ae"` to result. Backtrack. |
| 5 | `index=2, path="af"` | Base case reached. Add `"af"` to result. Backtrack to index 0. |
| 6 | `index=1, path="b"` | Branch on 'd', 'e', 'f' to generate `"bd"`, `"be"`, `"bf"`. |

---
## Edge Cases

- **Empty string (`digits = ""`)**: Must return `[]` (not `[""]`).
- **Single digit (`digits = "2"`)**: Should correctly output `["a", "b", "c"]`.
- **Digits 7 and 9**: Map to 4 letters instead of 3; verify loop limits.

---
## Mistakes

- Returning `[""]` instead of `[]` when the input is empty.
- User Mistake: No specific note provided.

---
## Complexity

Time: O(3^N * 4^M) → where N is the count of 3-letter digits and M is the count of 4-letter digits.
Space: O(N + M) → Recursion depth is bounded by the length of input digits.

---
## Similar Problems

- [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/) - Medium
- [Combinations](https://leetcode.com/problems/combinations/) - Medium
- [Subsets](https://leetcode.com/problems/subsets/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #backtracking #recursion
- [[Backtracking]] [[Recursion]] [[String]]
- **Revision Date:** 2026-07-17
- **Problem Link:** [LeetCode - Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-19)
- [ ] Day 7 Revision (2026-07-24)
- [ ] Day 15 Revision (2026-08-01)
- [ ] Day 30 Revision (2026-08-16)
