---
created: 2026-05-01
revisions:
  - 2026-05-03
  - 2026-05-08
  - 2026-05-16
  - 2026-05-31
---

# Maximum Nesting Depth Of The Parentheses

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Facebook #Google #Microsoft #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #stack [[Stack]]
  - #string [[String]]
  - #simulation [[Simulation]]

## Pattern

Parentheses Balance Counter (Stack Simulation)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The nesting depth of a character in a Valid Parentheses String (VPS) is simply the number of open parentheses `(` that have not yet been closed by a `)`. Tracking the maximum value of this "balance" during a single pass yields the result.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Increment a counter for `(`, update `max_depth`, and decrement for `)`. Ignore all other characters.

---

## Approach

### Brute Force
- Use an actual **Stack** to store `(`. Iterate through the string; if `(`, push to stack and check `stack.size()`. If `)`, pop.
- **Time Complexity:** O(N)
- **Space Complexity:** O(N) (to store the stack)

### Optimal
- Replace the physical stack with an integer variable `current_depth` since we only need to know the *count* of open brackets, not their positions.
- **Time Complexity:** O(N)
- **Space Complexity:** O(1)

---

## Code (Python)

```python
class Solution:
    def maxDepth(self, s: str) -> int:
        max_depth = 0
        current_depth = 0
        
        for char in s:
            if char == '(':
                current_depth += 1
                # Update max_depth whenever depth increases
                if current_depth > max_depth:
                    max_depth = current_depth
            elif char == ')':
                # Close the most recent nested group
                current_depth -= 1
                
        return max_depth
```

---

## Dry Run (Smart Example)

**Input:** `s = "(1+(2*3)+((8)/4))+1"`

| Step | Character | `current_depth` | `max_depth` | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `(` | 1 | 1 | First nesting level started. |
| 2 | `+` | 1 | 1 | Non-parenthesis; ignore. |
| 3 | `(` | 2 | 2 | Second nesting level started. |
| 4 | `)` | 1 | 2 | Second level closed. |
| 5 | `(` | 2 | 2 | New second level started. |
| 6 | `(` | 3 | 3 | **Third level started (Max reached).** |
| 7 | `)` | 2 | 3 | Inner level closed. |

---

## Edge Cases

- **Empty String or No Parentheses:** Returns 0 (correct, depth is 0).
- **Single Level `(1)`:** Returns 1.
- **Side-by-side Parentheses `()()`:** Returns 1 (depth resets between pairs).
- **Maximum Nesting at End `1+(2+(3))`:** Correctly tracks as depth increases.

---

## Mistakes

- **User mistake:** No specific note provided.
- **Confusing Depth with Total Count:** Counting all `(` instead of tracking the simultaneous open ones.
- **Updating Max at the Wrong Time:** Forgetting to update `max_depth` inside the `(` condition.
- **Unnecessary Space:** Using a Stack when a simple counter suffices.

---

## Complexity

Time: O(N) → Single pass through the string of length N.  
Space: O(1) → Only two integer variables used regardless of input size.

---

## Similar Problems

- [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) - Easy
- [Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/) - Medium
- [Remove Outermost Parentheses](https://leetcode.com/problems/remove-outermost-parentheses/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #parentheses #easy-wins
  - [[Stack]] [[Simulation]]
  - **Revision Date:** 2026-05-01
  - **Problem Link:** [LeetCode - Maximum Nesting Depth of the Parentheses](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-03)
- [ ] Day 7 Revision (2026-05-08)
- [ ] Day 15 Revision (2026-05-16)
- [ ] Day 30 Revision (2026-05-31)
