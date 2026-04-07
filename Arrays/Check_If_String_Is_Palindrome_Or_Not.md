---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Check If String Is Palindrome Or Not

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Meta #Google #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [x] High  

- **Concepts:**
  - #string [[String]]
  - #twopointers [[Two Pointers]]

## Pattern

Two Pointers

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

A palindrome reads the same backwards as it does forwards. This "mirror" property allows us to verify the string by comparing characters from the outermost ends moving inward towards the center.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use two pointers (`left`, `right`) starting at the ends. If `s[left] != s[right]` at any point, it's not a palindrome.

---

## Approach

### Brute Force
- Reverse the entire string and compare it with the original.
- **Complexity:** O(N) Time, O(N) Space.

### Optimal (Two Pointers)
1. Initialize `left` pointer at index `0` and `right` pointer at `len(s) - 1`.
2. Convert characters to lowercase (if case-insensitive) and skip non-alphanumeric characters if required.
3. Compare characters at `left` and `right`.
4. If they mismatch, return `False`.
5. Increment `left` and decrement `right` until they meet in the middle.

---

## Code (Python)

```python
def is_palindrome(s: str) -> bool:
    # 1. Clean the string: remove non-alphanumeric and lowercase
    # This covers the standard "Valid Palindrome" interview variation
    cleaned = "".join(char.lower() for char in s if char.isalnum())
    
    # 2. Two Pointer comparison
    left, right = 0, len(cleaned) - 1
    
    while left < right:
        if cleaned[left] != cleaned[right]:
            return False
        left += 1
        right -= 1
        
    return True

# Alternative Pythonic Way (High Performance)
def is_palindrome_pythonic(s: str) -> bool:
    cleaned = "".join(char.lower() for char in s if char.isalnum())
    return cleaned == cleaned[::-1]
```

---

## Dry Run (Smart Example)

**Input:** `"Aba"`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `cleaned = "aba"` | String is lowercased and filtered. |
| 2 | `left=0, right=2` | `s[0] ('a') == s[2] ('a')`. Continue. |
| 3 | `left=1, right=1` | `left` is no longer less than `right`. Loop ends. |
| 4 | `Result = True` | All checks passed. |

---

## Edge Cases

- **Empty String:** Usually considered a valid palindrome (True).
- **Single Character:** Always a palindrome (True).
- **Special Characters/Spaces:** Should be filtered out or handled per requirements.
- **Case Sensitivity:** `"Abba"` is a palindrome if case-insensitive, but not if case-sensitive.

---

## Mistakes

- **User mistake:** None
- **Logic error:** Forgetting to handle/skip non-alphanumeric characters.
- **Off-by-one:** Stopping the pointers too early or going out of bounds.
- **Case sensitivity:** Not normalizing characters before comparison.

---

## Complexity

Time: O(N) → We traverse the string at most twice (once for cleaning, once for comparison).  
Space: O(N) → Storing the cleaned version of the string (O(1) if modifying in-place with two pointers directly).

---

## Similar Problems

- [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) - Easy
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) - Medium
- [Palindrome Number](https://leetcode.com/problems/palindrome-number/) - Easy
- [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #palindrome #strings #coding-interview
  - [[String]] [[Two Pointers]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode - Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
