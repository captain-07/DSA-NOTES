---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Check If String Is Palindrome Or Not

---

## Pattern

Two Pointers (Meeting in the middle)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

A palindrome is a mirror image of itself. The character at index `i` must match the character at index `n - 1 - i`. By using two pointers starting from the extremities and moving inward, we can validate this symmetry in a single pass.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Initialize `left = 0` and `right = len - 1`. While `left < right`, if `s[left] != s[right]`, return `False`.

---

## Approach

### Brute Force
- Reverse the entire string and compare it with the original.
- **Time:** O(N)  
- **Space:** O(N) (to store the reversed string)

### Optimal
- Use two pointers, `left` and `right`, at both ends.
- Move pointers toward the center, comparing characters at each step.
- Handle case sensitivity and non-alphanumeric characters by skipping or converting if the problem context requires it.
- **Time:** O(N)
- **Space:** O(1) (in-place comparison)

---

## Code (Python)

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Standard interview version: Handle alphanumeric + Case insensitive
        left, right = 0, len(s) - 1
        
        while left < right:
            # Skip non-alphanumeric from left
            while left < right and not s[left].isalnum():
                left += 1
            # Skip non-alphanumeric from right
            while left < right and not s[right].isalnum():
                right -= 1
            
            # Compare lowercase versions
            if s[left].lower() != s[right].lower():
                return False
            
            left += 1
            right -= 1
            
        return True
```

---

## Dry Run (Smart Example)

**Input:** `"A man, a plan, a canal: Panama"`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `L=0('A'), R=29('a')` | Both are 'a' after `lower()`. Move pointers. |
| 2 | `L=2('m'), R=27('m')` | Skipped space/comma. 'm' matches 'm'. |
| 3 | `L=5('n'), R=24('n')` | Skipped spaces. 'n' matches 'n'. |
| 4 | `L=15('c'), R=15('c')` | Pointers meet at 'c'. Loop terminates. |

---

## Edge Cases

- **Empty String:** Usually considered a valid palindrome (True).
- **Single Character:** Always a palindrome (True).
- **Case Sensitivity:** "Racecar" should be True (requires `.lower()`).
- **Special Characters:** " " or ".,!" should be handled (True if empty after filtering).
- **All Same Characters:** "aaaaa" (True).

---

## Mistakes

- Not converting characters to lowercase before comparison.
- Forgetting to increment/decrement pointers inside the `while` loop, leading to infinite loops.
- Not handling non-alphanumeric characters (if the problem follows LeetCode "Valid Palindrome" rules).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Each character is visited at most twice (once by each pointer).  
Space: O(1) → Constant extra space used for pointers.

---

## Similar Problems

- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy
- [Palindrome Number](https://leetcode.com/problems/palindrome-number/) - Easy
- [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) - Easy
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #string #twopointers
  - [[Strings]] [[Two Pointers]]
  - **Revision Date:** 2026-04-11
  - **Problem Link:** [LeetCode - Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #string [[Strings]], #twopointers [[Two Pointers]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
