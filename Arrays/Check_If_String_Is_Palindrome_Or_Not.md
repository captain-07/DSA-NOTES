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
  - #Amazon #Microsoft #Facebook #Apple #Google #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #twopointers [[Two Pointers]]
  - #string [[String]]

## Pattern

Two Pointers (Meeting in the middle)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

A palindrome reads the same forwards and backwards. The most efficient way to verify this is by comparing characters from both ends simultaneously using two pointers, moving towards the center.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Initialize `left` at 0 and `right` at `len - 1`. Compare `s[left]` and `s[right]`. If they differ at any point, it is not a palindrome.

---

## Approach

### Brute Force
- Reverse the entire string and compare it with the original.
- **Time:** O(N) | **Space:** O(N) to store the reversed string.

### Optimal (Two Pointers)
1. Initialize two pointers: `left = 0`, `right = n - 1`.
2. While `left < right`:
   - Compare characters at `left` and `right`.
   - If they are not equal, return `False`.
   - Increment `left` and decrement `right`.
3. If the loop completes, return `True`.
- **Time:** O(N) | **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        """
        Checks if a string is a palindrome using two pointers.
        Note: Standard version usually ignores case and non-alphanumeric.
        """
        # Clean the string: remove non-alphanumeric and lowercase
        # (Common interview requirement for LeetCode 125)
        filtered_chars = [char.lower() for char in s if char.isalnum()]
        
        left, right = 0, len(filtered_chars) - 1
        
        while left < right:
            if filtered_chars[left] != filtered_chars[right]:
                return False
            left += 1
            right -= 1
            
        return True
```

---

## Dry Run (Smart Example)

**Input:** `s = "A man, a plan, a canal: Panama"`  
**Processed:** `amanaplanacanalpanama`

| Step | Pointers (L, R) | Chars (s[L], s[R]) | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 0, 20 | 'a', 'a' | Match. Move pointers. |
| 2 | 1, 19 | 'm', 'm' | Match. Move pointers. |
| 3 | 2, 18 | 'a', 'a' | Match. Move pointers. |
| 4 | 10, 10 | 'c', 'c' | L == R. Loop terminates. |

---

## Edge Cases

- **Empty String:** Usually considered a valid palindrome.
- **Single Character:** Always a palindrome.
- **Case Sensitivity:** "AbA" is a palindrome, but "Ab a" requires normalization.
- **Special Characters:** Spaces and punctuation should often be ignored.
- **Numeric Characters:** Should be treated as part of the string.

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Extra Space:** Creating a reversed copy of the string instead of using pointers.
- **Incorrect Bounds:** Using `left <= right` (unnecessary check for the middle character).
- **Not Handling Case:** Forgetting to convert to lowercase before comparison.

---

## Complexity

- **Time: O(N)** → We traverse the string at most once.
- **Space: O(1)** → Constant extra space used for pointers (if input modification is allowed or if we skip cleaning). O(N) if we create a filtered list.

---

## Similar Problems

- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy
- [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) - Easy
- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) - Easy
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) - Medium

---

## Tags and Properties
- #dsa #important #revisit  
- #string #twopointers #palindrome
- [[Two Pointers]] [[String]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [LeetCode - Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
