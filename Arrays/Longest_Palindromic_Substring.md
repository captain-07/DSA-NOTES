---
created: 2026-05-01
revisions:
  - 2026-05-03
  - 2026-05-08
  - 2026-05-16
  - 2026-05-31
---

# Longest Palindromic Substring

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #string [[String]]
  - #dynamicprogramming [[Dynamic Programming]]
  - #twopointers [[Two Pointers]]

---
## Pattern

Expand Around Center  
Manacher's Algorithm (Linear Time)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

A palindrome reads the same forwards and backwards. Instead of checking every possible substring (O(N³)), treat each character and each gap between characters as a **center** and expand outwards as long as the characters match. There are $2n - 1$ such centers.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Expand from $2n-1$ centers (indices $i$ for odd, $(i, i+1)$ for even). Maximize `right - left + 1`.

---

## Approach

### Brute Force
- Generate all $O(N^2)$ substrings and check each for palindrome property $O(N)$.
- **Time:** $O(N^3)$ | **Space:** $O(1)$

### Better (Dynamic Programming)
- Use a 2D table `dp[i][j]` to store if `s[i...j]` is a palindrome.
- `dp[i][j] = (s[i] == s[j]) and dp[i+1][j-1]`.
- **Time:** $O(N^2)$ | **Space:** $O(N^2)$

### Optimal 1 (Expand Around Center)
- Iterate through the string. For each index $i$, expand assuming $s[i]$ is the center (odd length) and $s[i], s[i+1]$ is the center (even length).
- Update the global maximum length and start index whenever a longer palindrome is found.
- **Time:** $O(N^2)$ | **Space:** $O(1)$

### Optimal 2 (Manacher's Algorithm)
- Pre-process string with boundaries (e.g., `#a#b#a#`).
- Use previously computed palindrome radii and a "rightmost boundary" to skip redundant checks.
- **Time:** $O(N)$ | **Space:** $O(N)$

---

## Code (Python)

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if not s or len(s) < 1:
            return ""
        
        start, end = 0, 0
        
        def expand(left: int, right: int) -> int:
            # Expand as long as characters match and indices are in bounds
            while left >= 0 and right < len(s) and s[left] == s[right]:
                left -= 1
                right += 1
            # Return length of the palindrome found
            return right - left - 1

        for i in range(len(s)):
            # Case 1: Odd length (center is s[i])
            len1 = expand(i, i)
            # Case 2: Even length (center is between s[i] and s[i+1])
            len2 = expand(i, i + 1)
            
            max_len = max(len1, len2)
            
            if max_len > (end - start):
                # Update start/end based on center i and max_len
                start = i - (max_len - 1) // 2
                end = i + max_len // 2
                
        return s[start:end + 1]
```

---

## Dry Run (Smart Example)

**Input:** `s = "babad"`

| Step | Center(s) | Type | Max Len Found | Result Substring |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `i=0 ('b')` | Odd | 1 | "b" |
| 2 | `i=1 ('a')` | Odd | 3 ("bab") | "bab" |
| 3 | `i=2 ('b')` | Odd | 3 ("aba") | "bab" (no update) |
| 4 | `i=1,2 ('ab')`| Even | 0 | "bab" |
| 5 | `i=4 ('d')` | Odd | 1 | "bab" |

---

## Edge Cases

- **Single Character:** `s = "a"` -> Returns "a".
- **All Same Characters:** `s = "aaaa"` -> Returns "aaaa".
- **No Palindrome > 1:** `s = "abcde"` -> Returns "a" (first char).
- **Empty String:** `s = ""` -> Returns "".

---

## Mistakes

- **User mistake:** No specific note provided.
- **Forgetting Even Lengths:** Only expanding from `(i, i)` and missing cases like `abba`.
- **Inefficient Substring Slicing:** Slicing strings inside the loop increases time complexity; store `start` and `max_len` instead.
- **Off-by-one errors:** Incorrectly calculating `start` and `end` from `max_len`.

---

## Complexity

- **Time:** $O(N^2)$ → We expand from $2N-1$ centers, and each expansion takes $O(N)$.
- **Space:** $O(1)$ → Only storing pointers and lengths (excluding output string).

---

## Similar Problems

- [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/) - Medium
- [Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/) - Medium
- [Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/) - Hard
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #strings #palindromes
- [[String]] [[Two Pointers]] [[Dynamic Programming]]
- **Revision Date:** May 1, 2026
- **Problem Link:** [LeetCode - Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-03)
- [ ] Day 7 Revision (2026-05-08)
- [ ] Day 15 Revision (2026-05-16)
- [ ] Day 30 Revision (2026-05-31)
