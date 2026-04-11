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

Two Pointers (Converging)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

A palindrome reads the same forwards and backwards. The most efficient way to verify this is to compare symmetric characters from both ends moving toward the center. If any pair mismatch, it is not a palindrome.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use two pointers (`left` at index 0, `right` at `n-1`). Move inward while `left < right`. If `s[left] != s[right]`, return `False`.

---

## Approach

### Brute Force
- Create a reversed copy of the string and compare it with the original using `s == s[::-1]`.
- **Time Complexity:** O(N)
- **Space Complexity:** O(N) (due to the reversed string storage)

### Optimal (Two Pointers)
- Initialize two pointers at the start and end of the string.
- Compare characters at both pointers. If they match, increment the left pointer and decrement the right pointer.
- Continue until pointers meet or cross.
- **Time Complexity:** O(N)
- **Space Complexity:** O(1)

---

## Code (Python)

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        """
        Determines if a string is a palindrome using two pointers.
        Assumes case-sensitivity and includes all characters.
        """
        # Initialize pointers at both ends
        left, right = 0, len(s) - 1
        
        while left < right:
            # Check for character mismatch
            if s[left] != s[right]:
                return False
            
            # Move pointers toward the center
            left += 1
            right -= 1
            
        return True
```

---

## Dry Run (Smart Example)

**Input:** `"racecar"`

| Step | Pointers (L, R) | Comparison (`s[L] == s[R]`) | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | L=0 ('r'), R=6 ('r') | 'r' == 'r' (True) | Characters match, move pointers inward. |
| 2 | L=1 ('a'), R=5 ('a') | 'a' == 'a' (True) | Characters match, move pointers inward. |
| 3 | L=2 ('c'), R=4 ('c') | 'c' == 'c' (True) | Characters match, move pointers inward. |
| 4 | L=3 ('e'), R=3 ('e') | Loop Ends (L is not < R) | Pointers met at the center. Palindrome confirmed. |

---

## Edge Cases

- **Empty String:** Usually considered a palindrome.
- **Single Character:** Always a palindrome (`"a"`).
- **Case Sensitivity:** `"Abba"` is NOT a palindrome unless normalized to lowercase.
- **Spaces/Special Characters:** If the problem includes them, `"a b a"` is a palindrome, but `"a b"` is not.

---

## Mistakes

- **Case Sensitivity:** Forgetting to ask if the check is case-insensitive (use `.lower()` if needed).
- **Alphanumeric Only:** Not clarifying if spaces and symbols should be ignored (requires `isalnum()` check).
- **Pointer Bounds:** Using `left <= right` is valid but `left < right` is slightly more efficient as the middle character doesn't need to be compared with itself.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → We traverse the string at most once (N/2 comparisons).  
Space: O(1) → No extra data structures are used, only two integer pointers.

---

## Similar Problems

- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy
- [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) - Easy
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) - Medium
- [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #strings #palindromes
- [[Strings]] [[Two Pointers]]
- **Revision Date:** 2026-04-11
- **Problem Link:** [LeetCode - Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Facebook #Adobe #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #strings [[Strings]], #twopointers [[Two Pointers]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
