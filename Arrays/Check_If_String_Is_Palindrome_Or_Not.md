---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Check If String Is Palindrome Or Not

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #twopointers [[Two Pointers]]
  - #strings [[Strings]]

## Pattern

Two Pointers (Meeting in the middle)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

A palindrome is a symmetric sequence. By placing one pointer at the start and another at the end, we can verify symmetry by comparing characters while moving both pointers toward the center.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `left` and `right` pointers; if any pair mismatches, it is not a palindrome. Stop when `left >= right`.

---

## Approach

### Brute Force
- Create a reversed copy of the string and compare it with the original.
- **Time:** O(N) | **Space:** O(N) due to the new string.

### Optimal (Two Pointers)
- Use two pointers, `i = 0` and `j = n-1`.
- While `i < j`, compare `s[i]` and `s[j]`.
- If the problem requires ignoring case and non-alphanumeric characters, skip invalid characters and normalize case before/during comparison.
- **Time:** O(N) | **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Standard implementation (handles alphanumeric + case sensitivity)
        left, right = 0, len(s) - 1
        
        while left < right:
            # Skip non-alphanumeric from left
            while left < right and not s[left].isalnum():
                left += 1
            # Skip non-alphanumeric from right
            while left < right and not s[right].isalnum():
                right -= 1
            
            # Compare normalized characters
            if s[left].lower() != s[right].lower():
                return False
            
            left += 1
            right -= 1
            
        return True

    def isPalindromeSimple(self, s: str) -> bool:
        # Pythonic approach (Optimal for clean strings)
        # Space O(N) due to slicing
        return s == s[::-1]
```

---

## Dry Run (Smart Example)

**Input:** `"A man, a plan, a canal: Panama"`

| Step | Left | Right | s[left] | s[right] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 29 | 'A' | 'a' | Match (ignore case), move both. |
| 2 | 2 | 28 | 'm' | 'm' | Skip space at index 1. Match 'm'. |
| 3 | 5 | 23 | 'n' | 'n' | Skip comma/space. Match 'n'. |
| 4 | 10 | 18 | 'p' | 'p' | Skip spaces/colons. Match 'p'. |
| 5 | ... | ... | ... | ... | Continues until pointers meet at 'a'. |

---

## Edge Cases

- **Empty String:** Usually considered a valid palindrome.
- **Single Character:** Always a palindrome.
- **Only Special Characters:** Becomes an empty string after filtering; valid palindrome.
- **Case Sensitivity:** "Racecar" should be True (requires `.lower()`).
- **Numeric Characters:** "12321" is a palindrome.

---

## Mistakes

- **Case Sensitivity:** Forgetting to convert characters to lowercase before comparison.
- **Non-Alphanumeric:** Failing to skip spaces, commas, or colons.
- **Pointer Bounds:** Not checking `left < right` inside the nested while loops, leading to `IndexError`.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → We traverse the string at most once with two pointers.  
Space: O(1) → We use only a few pointers regardless of input size (in-place comparison).

---

## Similar Problems

- [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) - Easy
- [Palindrome Number](https://leetcode.com/problems/palindrome-number/) - Easy
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) - Medium
- [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #strings #twopointers
  - [[Two Pointers]] [[String Manipulation]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
