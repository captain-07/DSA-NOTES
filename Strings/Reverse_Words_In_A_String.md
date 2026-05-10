---
created: 2026-04-27
revisions:
  - 2026-04-29
  - 2026-05-04
  - 2026-05-12
  - 2026-05-27
---

# Reverse Words In A String

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Meta #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #string [[String Manipulation]]
  - #array [[Array]]

## Pattern

String Splitting and Reversing

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The most efficient way to reverse words in Python while handling arbitrary whitespace is to use the `split()` method without arguments. It automatically splits by whitespace and removes empty strings. Reversing the resulting list and joining it with a single space solves all formatting requirements.

---

## ⚡ Quick Recall (VERY IMPORTANT)

`return " ".join(s.split()[::-1])`

---

## Approach

### Brute Force
- Iterate through the string, manually extract words by looking for spaces.
- Store words in a list, then build the result string by iterating backward.
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

### Optimal (Pythonic)
1. Use `s.split()` to obtain a list of non-empty words.
2. Reverse the list using `[::-1]` or `list.reverse()`.
3. Join the words back into a single string using `" ".join()`.
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

---

## Code (Python)

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        # split() without arguments handles multiple spaces automatically
        words = s.split()
        
        # Reverse the list using slicing
        reversed_words = words[::-1]
        
        # Join with a single space
        return " ".join(reversed_words)
```

---

## Dry Run (Smart Example)

**Input:** `s = "  the sky  is blue "`

| Step | Operation | Result | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `s.split()` | `['the', 'sky', 'is', 'blue']` | Leading, trailing, and double spaces removed. |
| 2 | `[::-1]` | `['blue', 'is', 'sky', 'the']` | Words order reversed. |
| 3 | `" ".join()` | `"blue is sky the"` | Reassembled with single spaces. |

---

## Edge Cases

- **Multiple Spaces:** `s.split()` treats consecutive spaces as a single delimiter.
- **Leading/Trailing Spaces:** Automatically handled by `split()`.
- **Empty String or Only Spaces:** `split()` returns an empty list; `join()` returns an empty string.
- **Single Word:** List has one element; join returns the same word.

---

## Mistakes

- **Using `s.split(' ')`:** This leaves empty strings in the list if there are multiple spaces.
- **String Concatenation in a Loop:** $O(N^2)$ due to string immutability in Python.
- **Manual Space Management:** Overcomplicating the logic with manual pointer tracking for spaces.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(N)$ → `split`, `reverse`, and `join` each take linear time.
- **Space:** $O(N)$ → To store the list of words.

---

## Similar Problems

- [Reverse String](https://leetcode.com/problems/reverse-string/) - Easy
- [Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/) - Easy
- [String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #strings #interview-prep
- [[Strings]] [[String Manipulation]]
- **Revision Date:** 2026-04-27
- **Problem Link:** [LeetCode - Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-29)
- [ ] Day 7 Revision (2026-05-04)
- [ ] Day 15 Revision (2026-05-12)
- [ ] Day 30 Revision (2026-05-27)
