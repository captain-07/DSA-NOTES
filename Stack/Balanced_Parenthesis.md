---
created: 2026-07-29
revisions:
  - 2026-07-31
  - 2026-08-05
  - 2026-08-13
  - 2026-08-28
---

# Balanced Parenthesis

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #stack [[Stack]], #string [[String]]

## Pattern
Stack-based Matching / LIFO Validation

---
## Difficulty
Easy
#easy

---
## ⚡ Key Idea (Core Insight)
Use a stack to track open brackets. A closing bracket is valid if and only if it matches the bracket type at the top of the stack.

---
## ⚡ Quick Recall (VERY IMPORTANT)
Push open brackets; pop and match close brackets; return `len(stack) == 0` at the end.

---
## Approach

### Brute Force
- Repeatedly replace adjacent valid pairs `()`, `[]`, `{}` with empty strings until no modifications can be made.
- Time Complexity: O(N^2)

### Optimal
- Maintain a stack and a dictionary mapping closing brackets to opening brackets.
- For each character:
  1. If it's a closing bracket, pop the top of the stack (default to a dummy value if empty) and check if it matches the mapping. If not, return False.
  2. If it's an opening bracket, push it onto the stack.
- Return True if stack is empty at the end, else False.
- Time Complexity: O(N)

---
## Code (Python)

```python
class Solution:
    def isValid(self, s: str) -> bool:
        # Map each closing bracket to its corresponding opening bracket
        mapping = {")": "(", "}": "{", "]": "["}
        stack = []

        for char in s:
            # If the character is a closing bracket
            if char in mapping:
                # Pop top element from stack if it exists, otherwise use dummy value
                top_element = stack.pop() if stack else '#'
                if mapping[char] != top_element:
                    return False
            else:
                # Opening bracket: push onto stack
                stack.append(char)

        # Valid only if stack is empty
        return not stack
```

---
## Dry Run (Smart Example)

Input: `s = "([)]"`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `char = '('`, `stack = ['(']` | Opening bracket, push to stack. |
| 2 | `char = '['`, `stack = ['(', '[']` | Opening bracket, push to stack. |
| 3 | `char = ')'`, `stack = ['(']`, `top_element = '['` | Closing bracket. Top element `[` does not match mapping value `(`. Return False. |

---
## Edge Cases

- `s = ""` (empty string): Returns True since stack remains empty.
- `s = "((("` (only open brackets): Returns False because stack is not empty at the end.
- `s = "}}}"` (only close brackets): Returns False immediately because pop from empty stack fails match.
- `s = "([]"` (unmatched open bracket): Returns False because stack contains `[` at the end.

---
## Mistakes

- Forgetting to check if stack is empty before popping (causes IndexError).
- Returning True immediately after matching a pair without verifying that the stack is completely empty at the end.
- User mistake: No specific note provided.

---
## Complexity

Time: O(N) → Single pass traversal of the string of length N.
Space: O(N) → In the worst case (e.g., `((((`), we push all characters onto the stack.

---
## Similar Problems

- [Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/) - Medium
- [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/) - Medium
- [Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/) - Medium
- [Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/) - Hard

---
## Tags and Properties
  - #dsa #important #revisit
  - #stack #string
  - [[Stack]] [[String]]
  - Revision Date: 2026-07-29
  - **Problem Link:** [LeetCode - Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-31)
- [ ] Day 7 Revision (2026-08-05)
- [ ] Day 15 Revision (2026-08-13)
- [ ] Day 30 Revision (2026-08-28)
