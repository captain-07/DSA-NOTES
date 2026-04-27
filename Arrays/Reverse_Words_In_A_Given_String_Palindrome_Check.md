---
created: 2026-04-27
revisions:
  - 2026-04-29
  - 2026-05-04
  - 2026-05-12
  - 2026-05-27
---

# Reverse Words In A Given String / Palindrome Check

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
  - #array [[Array]]

## Pattern

Two Pointers + String Splitting

---
## Difficulty

- Reverse Words: Medium #medium
- Palindrome Check: Easy #easy

---

## ⚡ Key Idea (Core Insight)

- **Reverse Words:** In Python, `split()` handles arbitrary whitespace automatically. Reversing the resulting list of words and `join()`ing them with a single space solves the spacing and ordering issues simultaneously.
- **Palindrome:** Use two pointers (`left`, `right`). Increment/decrement pointers until they point to alphanumeric characters, then compare. This avoids extra space from creating a new filtered string.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **Reverse Words:** `return " ".join(s.split()[::-1])`
- **Palindrome:** `while left < right: if s[l] != s[r]: return False`

---

## Approach

### Brute Force
- **Reverse Words:** Iterate through the string, manually extract words, prepend them to a new string. (Time: $O(N^2)$ due to string concatenation).
- **Palindrome:** Create a reversed copy of the string and compare. (Space: $O(N)$).

### Optimal (Reverse Words)
1. Use `split()` to get all non-empty words (removes leading/trailing/multiple spaces).
2. Reverse the list of words.
3. Join words with a single space.

### Optimal (Palindrome Check)
1. Initialize `left = 0`, `right = len(s) - 1`.
2. Move pointers inward, skipping non-alphanumeric characters.
3. Compare characters (case-insensitive). If mismatch, return `False`.

---

## Code (Python)

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        # split() without arguments handles multiple spaces automatically
        words = s.split()
        # Reverse the list in-place or via slicing
        words.reverse()
        return " ".join(words)

    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1
        
        while l < r:
            # Skip non-alphanumeric
            while l < r and not s[l].isalnum():
                l += 1
            while l < r and not s[r].isalnum():
                r -= 1
                
            if s[l].lower() != s[r].lower():
                return False
            
            l += 1
            r -= 1
            
        return True
```

---

## Dry Run (Smart Example)
**Input:** `s = "  the sky  is blue "` (Reverse Words)

| Step | Operation | Result/Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `s.split()` | `['the', 'sky', 'is', 'blue']` | Leading/trailing/extra spaces removed. |
| 2 | `[::-1]` | `['blue', 'is', 'sky', 'the']` | List order reversed. |
| 3 | `" ".join()` | `"blue is sky the"` | Words joined with single space. |

---

## Edge Cases

- **Multiple Spaces:** `s.split()` handles this; `s.split(' ')` does not.
- **Empty/Whitespace Only:** Returns empty string.
- **Single Word:** Reversing a single word returns the same word.
- **Non-Alphanumeric (Palindrome):** Ensure pointers don't go out of bounds when skipping.
- **Case Sensitivity (Palindrome):** Always use `.lower()` for comparisons.

---

## Mistakes

- Using `s.split(' ')` instead of `s.split()` (leaves empty strings in the list).
- Forgetting that strings are immutable in Python (cannot reverse in-place).
- Not handling non-alphanumeric characters in "Valid Palindrome" problems.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(N)$ → We traverse the string/list a constant number of times.
- **Space:** $O(N)$ → To store the list of words or the filtered characters.

---

## Similar Problems

- [Reverse String](https://leetcode.com/problems/reverse-string/) - Easy
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy
- [Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/) - Easy
- [Palindrome Number](https://leetcode.com/problems/palindrome-number/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #strings #interview-prep
- [[Two Pointers]] [[String Manipulation]]
- **Revision Date:** 2026-04-27
- **Problem Link:** [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/) | [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-29)
- [ ] Day 7 Revision (2026-05-04)
- [ ] Day 15 Revision (2026-05-12)
- [ ] Day 30 Revision (2026-05-27)
