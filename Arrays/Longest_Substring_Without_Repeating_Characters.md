---
created: 2026-08-11
revisions:
  - 2026-08-13
  - 2026-08-18
  - 2026-08-26
  - 2026-09-10
---

# Longest Substring Without Repeating Characters

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Meta #Bloomberg #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #slidingwindow [[Sliding Window]], #hashmap [[HashMap]], #string [[String]]

## Pattern

Sliding Window (Dynamic Width) + HashMap

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

Use two pointers (`left` and `right`) to represent a window of unique characters. When a duplicate character is encountered at the `right` pointer, shrink the window instantly by jumping the `left` pointer to `max(left, last_seen_index + 1)`.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Slide `right` pointer and store character indices in a map. If `s[right]` is already in the map, jump `left` to `map[s[right]] + 1` (guarded by `max` to prevent moving backward). Track the maximum length at each step.

---
## Approach

### Brute Force
- Check every possible substring for duplicate characters using a set.
- Time Complexity: O(N³)

### Better
- Sliding window with a Set. Move `right` pointer, and if a duplicate is found, increment `left` pointer one by one while removing elements from the set until the duplicate is removed.
- Time Complexity: O(N) (each character is visited at most twice)

### Optimal
- Sliding window with a HashMap storing `{character: index}`. When a duplicate is seen, jump the `left` pointer directly to `max(left, map[char] + 1)` to skip redundant inner increments.
- Time Complexity: O(N) (each character is visited exactly once)

---
## Code (Python)

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        char_map = {}  # maps character -> its last seen index
        left = 0
        max_len = 0

        for right in range(len(s)):
            char = s[right]
            # If char is within the current active window, slide left pointer
            if char in char_map:
                left = max(left, char_map[char] + 1)

            # Record current character's index and calculate length
            char_map[char] = right
            max_len = max(max_len, right - left + 1)

        return max_len
```

---
## Dry Run (Smart Example)

Input: `s = "abba"`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `right=0`, `char='a'`, `left=0`, `char_map={'a': 0}`, `max_len=1` | First character added. |
| 2 | `right=1`, `char='b'`, `left=0`, `char_map={'a': 0, 'b': 1}`, `max_len=2` | New character, window expands. |
| 3 | `right=2`, `char='b'`, `left=2`, `char_map={'a': 0, 'b': 2}`, `max_len=2` | Duplicate 'b' seen inside window. `left` jumps to `max(0, 1 + 1) = 2`. |
| 4 | `right=3`, `char='a'`, `left=2`, `char_map={'a': 3, 'b': 2}`, `max_len=2` | Duplicate 'a' seen, but index `0` is outside window. `left` remains `2`. |

---
## Edge Cases

- **Empty string (`s = ""`)**: Loop does not execute; returns `0` correctly.
- **Single character (`s = "a"`)**: Loop runs once; returns `1`.
- **All identical characters (`s = "bbbbb"`)**: `left` updates to `right` at each step; returns `1`.
- **No duplicates (`s = "abcdef"`)**: `left` remains `0` throughout; returns string length.

---
## Mistakes

- **Moving left backward**: Forgetting to use `max(left, char_map[char] + 1)` when jumping the left pointer. This causes correctness issues when encountering old duplicates outside the active window.
- **Off-by-one errors**: Calculating length as `right - left` instead of `right - left + 1`.
- **User Mistake**: No specific note provided.

---
## Complexity

Time: O(N) → Single pass over the string of length N.
Space: O(min(M, N)) → Size of the map is bound by size of the string N and the size of the charset M (constant O(1) for standard ASCII).

---
## Similar Problems

- [Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/) - Medium
- [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) - Medium
- [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #slidingwindow #hashmap
- [[Sliding Window]] [[HashMap]]
- **Revision Date:** 2026-08-11
- **Problem Link:** [Longest Substring Without Repeating Characters - LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-13)
- [ ] Day 7 Revision (2026-08-18)
- [ ] Day 15 Revision (2026-08-26)
- [ ] Day 30 Revision (2026-09-10)
