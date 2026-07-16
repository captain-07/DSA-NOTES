---
created: 2026-07-10
revisions:
  - 2026-07-12
  - 2026-07-17
  - 2026-07-25
  - 2026-08-09
---

# Generate Binary Strings Without Consecutive 1s

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Uber

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #backtracking [[Backtracking]], #recursion [[Recursion]]

## Pattern

Backtracking + State-Space Reduction

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

- Build the binary string of length $N$ character-by-character from left to right.
- If the previous character placed was `'1'`, the current character can only be `'0'`.
- If the previous character placed was `'0'` (or string is empty), the current character can be either `'0'` or `'1'`.

---
## ⚡ Quick Recall (VERY IMPORTANT)

- Append `'0'` unconditionally. Only append `'1'` if the previous character was `'0'` (or empty).

---
## Approach

### Brute Force
- Generate all $2^N$ binary strings using recursion and filter out strings containing the substring `"11"`.
- Time Complexity: $O(N \cdot 2^N)$

### Optimal
- Use recursive backtracking to build only valid strings, pruning invalid state-space branches early.
- Track the current string and the last appended character.
- Append `'0'` to branch into the next state.
- If `last_char` is not `'1'`, branch again by appending `'1'`.
- Base Case: When string length reaches $N$, store the result.

---
## Code (Python)

```python
class Solution:
    def generateString(self, n: int) -> list[str]:
        self.res = []
        self.n = n
        # Start recursion with empty string and empty last_char state
        self.backtrack("", "")
        return self.res

    def backtrack(self, curr_str: str, last_char: str):
        # Base Case: valid string of length n generated
        if len(curr_str) == self.n:
            self.res.append(curr_str)
            return

        # '0' can always be appended regardless of the last character
        self.backtrack(curr_str + "0", "0")

        # '1' can only be appended if the last character was '0' or empty
        if not last_char or last_char == "0":
            self.backtrack(curr_str + "1", "1")
```

---
## Dry Run (Smart Example)

Input: `n = 3`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `curr_str = "", last_char = ""` | Start recursion. Branches to `"0"` and `"1"`. |
| 2 | `curr_str = "0", last_char = "0"` | Branches to `"00"` and `"01"`. |
| 3 | `curr_str = "00", last_char = "0"` | Branches to `"000"` and `"001"`. |
| 4 | `curr_str = "000", last_char = "0"` | Length = 3. Add `"000"`. Backtrack. |
| 5 | `curr_str = "001", last_char = "1"` | Length = 3. Add `"001"`. Backtrack. |
| 6 | `curr_str = "01", last_char = "1"` | Last char is `'1'`. Only branch to `"010"`. |
| 7 | `curr_str = "010", last_char = "0"` | Length = 3. Add `"010"`. Backtrack. |
| 8 | `curr_str = "1", last_char = "1"` | Last char is `'1'`. Only branch to `"10"`. |
| 9 | `curr_str = "10", last_char = "0"` | Branches to `"100"` and `"101"`. |
| 10 | `curr_str = "100", last_char = "0"` | Length = 3. Add `"100"`. Backtrack. |
| 11 | `curr_str = "101", last_char = "1"` | Length = 3. Add `"101"`. Backtrack. |

---
## Edge Cases

- `n = 1`: Standard single-digit binary strings; returns `["0", "1"]`.
- `n = 0`: Returns `[]` or `[""]`. Handle gracefully depending on constraints.
- Large `n`: standard stack limit for recursion depth $O(N)$ (typically up to $N = 1000$ is safe in Python).

---
## Mistakes

- **Generating All Strings**: Generating all $2^N$ combinations and filtering for `"11"` results in TLE.
- **Incorrect Backtrack Conditions**: Forgetting that `"00"` is a valid substring and only pruning `"11"`.
- **User Mistake**: Didn't understand how state constraints prune invalid branches early in the recursion tree.

---
## Complexity

Time: $O(1.618^N)$ → Valid string count follows the Fibonacci sequence, which scales asymptotically with the golden ratio.
Space: $O(N)$ → Maximum recursion stack depth is proportional to the target string length $N$.

---
## Similar Problems

- [Generate Binary Strings Without Adjacent Zeros](https://leetcode.com/problems/generate-binary-strings-without-adjacent-zeros/) - Medium
- [Non-negative Integers without Consecutive Ones](https://leetcode.com/problems/non-negative-integers-without-consecutive-ones/) - Hard
- [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/) - Medium
- [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) - Medium

---
## Tags and Properties

- #dsa #important #revisit
- #backtracking #recursion #binary-strings
- Obsidian links: [[Backtracking]] [[Recursion]]
- **Revision Date:** 2026-07-10
- **Problem Link:** [GeeksforGeeks - Generate all binary strings without consecutive 1s](https://www.geeksforgeeks.org/generate-binary-strings-without-consecutive-1s/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-12)
- [ ] Day 7 Revision (2026-07-17)
- [ ] Day 15 Revision (2026-07-25)
- [ ] Day 30 Revision (2026-08-09)
