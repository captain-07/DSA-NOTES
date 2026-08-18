---
created: 2026-04-27
revisions:
  - 2026-04-29
  - 2026-05-04
  - 2026-05-12
  - 2026-05-27
---

# Remove Outermost Parentheses

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #strings [[Strings]]
  - #stack [[Stack]]
  - #greedy [[Greedy]]

---
## Pattern

Balance Counter (Parenthesis Tracking)

---
## Difficulty

Easy 
#easy

---

## ⚡ Key Idea (Core Insight)

The outermost parentheses of a primitive string are those that start at balance level 0 and end at balance level 0. By tracking the nesting level (count), we only append characters to the result if they exist at a depth greater than 0.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Skip appending `(` if it starts at depth 0; skip appending `)` if it ends at depth 0.

---

## Approach

### Brute Force
- Identify every "Primitive" substring by finding indices where open and close counts equalize. Extract substrings and slice `[1:-1]`.
- **Time Complexity:** O(N)
- **Space Complexity:** O(N) for substring storage.

### Optimal (Single Pass Counter)
- Use a variable `opened` to track the nesting level.
- For `(`: If `opened > 0`, it's not outermost → Append. Then increment `opened`.
- For `)`: Decrement `opened` first. If `opened > 0`, it's not outermost → Append.
- **Time Complexity:** O(N)
- **Space Complexity:** O(1) (excluding result string).

---

## Code (Python)

```python
class Solution:
    def removeOuterParentheses(self, s: str) -> str:
        res = []
        opened = 0
        
        for char in s:
            if char == '(':
                # If opened > 0, this '(' is inside another pair
                if opened > 0:
                    res.append(char)
                opened += 1
            else:
                # Decrement first to check if it was an inner ')'
                opened -= 1
                if opened > 0:
                    res.append(char)
                    
        return "".join(res)
```

---

## Dry Run (Smart Example)

**Input:** `s = "(()())(())"`

| Step | Char | `opened` (Before) | `opened` (After) | Action | Result |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `(` | 0 | 1 | Skip (Outer) | `""` |
| 2 | `(` | 1 | 2 | Append | `"("` |
| 3 | `)` | 2 | 1 | Append | `"()"` |
| 4 | `(` | 1 | 2 | Append | `"()("` |
| 5 | `)` | 2 | 1 | Append | `"()()"` |
| 6 | `)` | 1 | 0 | Skip (Outer) | `"()()"` |
| 7 | `(` | 0 | 1 | Skip (Outer) | `"()()"` |
| 8 | `(` | 1 | 2 | Append | `"()()("` |
| 9 | `)` | 2 | 1 | Append | `"()()()"` |
| 10 | `)` | 1 | 0 | Skip (Outer) | `"()()()"` |

---

## Edge Cases

- **Empty String:** Should return `""` (though constraints usually forbid).
- **Single Primitive:** `"(())"` → returns `"()"` correctly.
- **Multiple Primitives:** `"()()()"` → returns `""` correctly.
- **Deeply Nested:** `"(((())))"` → returns `"((()))"`.

---

## Mistakes

- **Incorrect Order:** Incrementing `opened` before checking the condition for `(` or decrementing after checking for `)`.
- **Off-by-one:** Confusion between checking `opened > 0` vs `opened > 1`.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → We iterate through the string exactly once.  
Space: O(N) → In the worst case, the result string stores nearly all characters of the input.

---

## Similar Problems

- [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) - Easy
- [Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/) - Medium
- [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #parenthesis #string-manipulation
  - [[Stack]] [[Strings]]
  - **Revision Date:** 2026-04-27
  - **Problem Link:** [LeetCode - Remove Outermost Parentheses](https://leetcode.com/problems/remove-outermost-parentheses/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-29)
- [ ] Day 7 Revision (2026-05-04)
- [ ] Day 15 Revision (2026-05-12)
- [ ] Day 30 Revision (2026-05-27)
