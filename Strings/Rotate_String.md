---
created: 2026-04-28
revisions:
  - 2026-04-30
  - 2026-05-05
  - 2026-05-13
  - 2026-05-28
---

# Rotate String

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #LinkedIn #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #strings [[Strings]], #string-matching [[String Matching]]

## Pattern

String Concatenation + Substring Search

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The most elegant insight is that any rotation of a string `s` is a substring of `s + s`. If `s = "abcde"`, then `s + s = "abcdeabcde"`. Notice that "bcdea", "cdeab", "deabc", and "eabcd" are all contained within it.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If `len(s) == len(goal)`, check if `goal` exists inside the concatenated string `(s + s)`.

---

## Approach

### Brute Force
- Manually generate all $N$ possible rotations by slicing and shifting, then compare each with the goal.
- Time Complexity: $O(N^2)$ due to $N$ rotations and $O(N)$ string comparisons.

### Optimal
1. Check if `len(s)` is equal to `len(goal)`. If not, return `False`.
2. Concatenate `s` with itself: `double_s = s + s`.
3. Check if `goal` is a substring of `double_s`.
4. Return the boolean result.

---

## Code (Python)

```python
class Solution:
    def rotateString(self, s: str, goal: str) -> bool:
        # Step 1: Length check is mandatory
        if len(s) != len(goal):
            return False
        
        # Step 2: Concatenation trick
        # Any rotation of s MUST be a substring of s + s
        return goal in (s + s)
```

---

## Dry Run (Smart Example)

**Input:** `s = "abcde"`, `goal = "cdeab"`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `len(s)=5, len(goal)=5` | Lengths match, proceed. |
| 2 | `combined = "abcdeabcde"` | `s + s` created to hold all possible rotations. |
| 3 | `"cdeab" in "abcdeabcde"` | Search finds "cdeab" at index 2. |
| 4 | `Return True` | Match found, rotation confirmed. |

---

## Edge Cases

- **Different Lengths:** `s = "abc"`, `goal = "abcd"` -> Immediate `False`.
- **Empty Strings:** Usually handled by constraints, but `""` in `""` is `True`.
- **Single Character:** `s = "a"`, `goal = "a"` -> `True`.
- **Identical Strings:** `s = "abc"`, `goal = "abc"` -> `True` (0 rotations).

---

## Mistakes

- **Length Omission:** Forgetting to check `len(s) == len(goal)` (results in false positives if `goal` is a smaller substring).
- **Manual Shifting:** Overcomplicating with deque or manual slicing which increases code complexity.
- **User Mistake:** No specific note provided. (Ensure you remember the concatenation trick for $O(1)$ lines of logic).

---

## Complexity

Time: O(N) → Python's `in` operator uses a mix of Boyer-Moore and Horspool (average $O(N+M)$).  
Space: O(N) → Creating the concatenated string `s + s` requires linear space.

---

## Similar Problems

- [Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern/) - Easy
- [String Matching in an Array](https://leetcode.com/problems/string-matching-in-an-array/) - Easy
- [Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit
  - #strings #linear-search [[Strings]]
  - Revision Date: 2026-04-28
  - **Problem Link:** [LeetCode - Rotate String](https://leetcode.com/problems/rotate-string/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-30)
- [ ] Day 7 Revision (2026-05-05)
- [ ] Day 15 Revision (2026-05-13)
- [ ] Day 30 Revision (2026-05-28)
