---
created: 2026-04-28
revisions:
  - 2026-04-30
  - 2026-05-05
  - 2026-05-13
  - 2026-05-28
---

# Check If Two Strings Are Anagram Of Each Other

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]], #strings [[Strings]], #sorting [[Sorting]], #counting [[Counting]]

## Pattern

Frequency Counting (Hash Map or Fixed-size Array)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

Two strings are anagrams if and only if they have the **exact same characters** with the **exact same frequencies**. A frequency map (or a fixed-size array for ASCII) is the most efficient way to verify this.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Check lengths first; if they differ, return `False`. Use one frequency array/map: increment for string `s`, decrement for string `t`. All counts must be zero.

---

## Approach

### Brute Force
- Sort both strings and compare them character by character.
- **Time Complexity:** $O(N \log N)$
- **Space Complexity:** $O(1)$ or $O(N)$ depending on sorting implementation.

### Optimal
- Use a hash map or an array of size 26 (for lowercase English).
- Iterate through `s` to increment counts and `t` to decrement.
- Verify if all counts in the map/array are zero.
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ (constant space for fixed character set).

---

## Code (Python)

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # Step 1: Length check (O(1))
        if len(s) != len(t):
            return False
        
        # Step 2: Frequency map (using array for efficiency)
        # Assuming lowercase English letters
        count = [0] * 26
        
        for i in range(len(s)):
            count[ord(s[i]) - ord('a')] += 1
            count[ord(t[i]) - ord('a')] -= 1
            
        # Step 3: Verify all counts are zero
        for c in count:
            if c != 0:
                return False
                
        return True
```

---

## Dry Run (Smart Example)

Input: `s = "anagram"`, `t = "nagaram"`

| Step | Index | `s[i]` / `t[i]` | Variable State (Partial `count` array) | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | - | - | All 0s | `len(s) == len(t)` check passes. |
| 2 | 0 | 'a' / 'n' | `count[a]=1, count[n]=-1` | Increment for 'a', decrement for 'n'. |
| 3 | 1 | 'n' / 'a' | `count[a]=0, count[n]=0` | Counts reset for these two chars. |
| 4 | 2 | 'a' / 'g' | `count[a]=1, count[g]=-1` | Tracking current diff. |
| 5 | ... | ... | ... | After all indices, all indices in `count` are 0. |

---

## Edge Cases

- **Different Lengths:** Return `False` immediately.
- **Empty Strings:** Technically anagrams (True).
- **Unicode/Special Characters:** Use a Hash Map instead of a size-26 array.
- **Case Sensitivity:** "Anagram" vs "anagram" (clarify with interviewer if 'A' == 'a').

---

## Mistakes

- **Forgetting Length Check:** Wasteful $O(N)$ processing for strings that can't be anagrams.
- **Character Set Assumption:** Hardcoding size 26 when the input might contain Unicode or symbols.
- **Using Two HashMaps:** One is sufficient (increment then decrement).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(N)$ → Single pass through strings of length $N$.  
Space: $O(1)$ → Constant space for the 26-character frequency array (or $O(K)$ where $K$ is the character set size).

---

## Similar Problems

- [Group Anagrams](https://leetcode.com/problems/group-anagrams/) - Medium
- [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/) - Medium
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy
- [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/) - Medium

---

## Tags and Properties
- #dsa #important #revisit
- #strings [[Strings]] #hashmap [[HashMap]]
- **Revision Date:** 2026-04-28
- **Problem Link:** [LeetCode - Valid Anagram](https://leetcode.com/problems/valid-anagram/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-30)
- [ ] Day 7 Revision (2026-05-05)
- [ ] Day 15 Revision (2026-05-13)
- [ ] Day 30 Revision (2026-05-28)
