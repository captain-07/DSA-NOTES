---
created: 2026-04-27
revisions:
  - 2026-04-29
  - 2026-05-04
  - 2026-05-12
  - 2026-05-27
---

# Valid Palindrome

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Meta #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #twopointers [[Two Pointers]]
  - #string [[String Manipulation]]

## Pattern

Two Pointers (Converging with Filtering)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

To determine if a phrase is a palindrome while ignoring non-alphanumeric characters and case, use two pointers (`left`, `right`). Increment/decrement pointers until they point to alphanumeric characters, then compare. This avoids the $O(N)$ extra space required to create a filtered version of the string.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Use `isalnum()` to skip non-alphanumeric characters.
- Use `.lower()` for case-insensitive comparison.
- `while left < right: if s[l].lower() != s[r].lower(): return False`

---

## Approach

### Brute Force
- Create a new string containing only alphanumeric characters in lowercase.
- Check if the new string is equal to its reverse: `s == s[::-1]`.
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

### Optimal (Two Pointers)
1. Initialize `left = 0`, `right = len(s) - 1`.
2. Move pointers inward, skipping non-alphanumeric characters using `while` loops and `isalnum()`.
3. Compare the characters at `left` and `right` (case-insensitive).
4. If they don't match, return `False`.
5. If they match, move both pointers closer to the center.
6. Return `True` if the pointers meet or cross.
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

## Code (Python)

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1
        
        while l < r:
            # Skip non-alphanumeric characters from the left
            while l < r and not s[l].isalnum():
                l += 1
            # Skip non-alphanumeric characters from the right
            while l < r and not s[r].isalnum():
                r -= 1
                
            # Case-insensitive comparison
            if s[l].lower() != s[r].lower():
                return False
            
            l += 1
            r -= 1
            
        return True
```

---

## Dry Run (Smart Example)

**Input:** `s = "A man, a plan, a canal: Panama"`

| Step | Left Pointer | Right Pointer | Comparison | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `s[0]` ('A') | `s[29]` ('a') | 'a' == 'a' | Match. Move both pointers. |
| 2 | `s[1]` (' ') | `s[28]` ('m') | - | Skip space at index 1. |
| 3 | `s[2]` ('m') | `s[28]` ('m') | 'm' == 'm' | Match. Move both pointers. |
| ... | ... | ... | ... | ... |
| End | - | - | - | Pointers cross. Return **True**. |

---

## Edge Cases

- **Empty String or Whitespace Only:** Handled by `l < r` condition; returns `True`.
- **Single Character (Alphanumeric):** Loop doesn't run; returns `True`.
- **Single Character (Non-Alphanumeric):** Pointers meet while skipping; returns `True`.
- **String with no alphanumeric characters:** Returns `True`.

---

## Mistakes

- **Not normalizing case:** Comparing 'A' with 'a' and returning `False`.
- **Not skipping non-alphanumeric:** Trying to compare commas or spaces.
- **Incorrect pointer logic:** Moving pointers out of bounds when skipping.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(N)$ → Single pass through the string of length N.
- **Space:** $O(1)$ → Only two integer pointers used.

---

## Similar Problems

- [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) - Easy
- [Palindrome Number](https://leetcode.com/problems/palindrome-number/) - Easy
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #strings #palindromes #twopointers
- [[Strings]] [[Two Pointers]]
- **Revision Date:** 2026-04-27
- **Problem Link:** [LeetCode - Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-29)
- [ ] Day 7 Revision (2026-05-04)
- [ ] Day 15 Revision (2026-05-12)
- [ ] Day 30 Revision (2026-05-27)
