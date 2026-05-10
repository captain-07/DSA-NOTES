---
created: 2026-04-27
revisions:
  - 2026-04-29
  - 2026-05-04
  - 2026-05-12
  - 2026-05-27
---

# Longest Common Prefix

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Apple #Adobe #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #strings [[Strings]]
  - #sorting [[Sorting]]
  - #verticalscanning [[Vertical Scanning]]

## Pattern

Vertical Scanning  
Sorting-based Comparison

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The longest common prefix (LCP) must be a prefix of **every** string. By sorting the array, the strings that are most "different" lexicographically move to the first and last positions. The LCP of the entire array is simply the LCP of the first and last strings.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort the list and compare only the **first** and **last** strings. The common part between them is the answer.

---

## Approach

### Brute Force
- Compare `strs[0]` with `strs[1]` to find a prefix, then compare that result with `strs[2]`, and so on.
- Time: O(S) where S is the sum of all characters in all strings.

### Better (Vertical Scanning)
- Iterate through characters of the first string index by index.
- For each index, check if that character exists at the same position in all other strings.
- Time: O(S), but better average case as it stops at the first mismatch.

### Optimal (Sorting)
1. Handle empty input edge case.
2. Sort the array lexicographically.
3. Compare the first string (`strs[0]`) and the last string (`strs[-1]`).
4. Incrementally build the prefix as long as characters match.

---

## Code (Python)

```python
class Solution:
    def longestCommonPrefix(self, strs: list[str]) -> str:
        if not strs:
            return ""
        
        # Sort lexicographically
        strs.sort()
        
        first = strs[0]
        last = strs[-1]
        res = []
        
        # Compare first and last strings only
        for i in range(min(len(first), len(last))):
            if first[i] != last[i]:
                break
            res.append(first[i])
            
        return "".join(res)
```

---

## Dry Run (Smart Example)

Input: `strs = ["flower", "flow", "flight"]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `strs = ["flight", "flow", "flower"]` | Sorted array lexicographically. |
| 2 | `first="flight"`, `last="flower"` | Select first and last for comparison. |
| 3 | `i=0`: 'f' == 'f' | Match found, add 'f' to result. |
| 4 | `i=1`: 'l' == 'l' | Match found, add 'l' to result. |
| 5 | `i=2`: 'i' != 'o' | Mismatch! Break loop. |
| 6 | Return `"fl"` | Final result. |

---

## Edge Cases

- **Empty List:** Handled by `if not strs`.
- **Single String:** Sorting works; first and last are the same, returns the whole string.
- **No Common Prefix:** Loop breaks at `i=0`, returns empty string.
- **One string is a prefix of another:** `min(len(first), len(last))` prevents out-of-bounds.

---

## Mistakes

- Not checking for an empty input array.
- Using a nested loop that doesn't break early (inefficient).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N * L log N) → N is the number of strings, L is the max length. Sorting dominates.  
Space: O(L) → To store the resulting prefix string.

---

## Similar Problems

- [Longest Common Substring](https://leetcode.com/problems/longest-common-subpath/) - Hard
- [Group Anagrams](https://leetcode.com/problems/group-anagrams/) - Medium
- [String Matching in an Array](https://leetcode.com/problems/string-matching-in-an-array/) - Easy

---

## Tags and Properties
- #dsa #important #revisit
- #strings [[Strings]] #sorting [[Sorting]]
- **Revision Date:** 2026-04-27
- **Problem Link:** [LeetCode - Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-29)
- [ ] Day 7 Revision (2026-05-04)
- [ ] Day 15 Revision (2026-05-12)
- [ ] Day 30 Revision (2026-05-27)
