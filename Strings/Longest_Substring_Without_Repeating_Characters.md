---
created: 2026-09-13
revisions:
  - 2026-09-15
  - 2026-09-20
  - 2026-09-28
  - 2026-10-13
---

# Longest Substring Without Repeating Characters

---

## Metadata & Placement Tags

- **Folder:** Strings
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #slidingwindow [[Sliding Window]], #twopointers [[Two Pointers]], #hashmap [[HashMap]]

## Pattern

Sliding Window + Dynamic Window Sizing (HashMap / Array)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

Use two pointers to maintain a sliding window of unique characters. Expand the right pointer to include characters, and when a duplicate is found, shrink the window by updating the left pointer to `last_seen_index + 1`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

`left = max(left, char_map[char] + 1)` when duplicate seen; length is `right - left + 1`.

---

## Approach

### Brute Force
- Check all possible substrings for unique characters.
- Time: O(N³), Space: O(N)

### Better
- Use sliding window with a HashSet. Advance right pointer; if duplicate, advance left pointer one by one until duplicate is removed.
- Time: O(N) [each char visited twice], Space: O(min(M, N))

### Optimal
- Optimize sliding window using a HashMap/Array to store character indices. Skip left pointer directly past the last seen index of the repeating character.
- Time: O(N) [single pass], Space: O(min(M, N)) where M is alphabet size.

---

## Code (Python)

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        # Map to store the last seen index of each character
        last_seen = {}
        left = 0
        max_len = 0

        for right in range(len(s)):
            current_char = s[right]

            # If char was seen and is within current window, shrink window
            if current_char in last_seen and last_seen[current_char] >= left:
                left = last_seen[current_char] + 1

            # Update last seen position of character
            last_seen[current_char] = right

            # Update maximum length found so far
            current_window_len = right - left + 1
            if current_window_len > max_len:
                max_len = current_window_len

        return max_len
```

---

## Dry Run (Smart Example)

Input: `s = "pwwkew"`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `right=0 ('p')`, `left=0` | `last_seen={'p':0}`, `max_len=1` ("p") |
| 2 | `right=1 ('w')`, `left=0` | `last_seen={'p':0, 'w':1}`, `max_len=2` ("pw") |
| 3 | `right=2 ('w')`, `left=0` | Duplicate 'w'! `left = max(0, 1 + 1) = 2`. `last_seen['w']=2`, `max_len=2` |
| 4 | `right=3 ('k')`, `left=2` | `last_seen={'p':0, 'w':2, 'k':3}`, `max_len=2` ("wk") |
| 5 | `right=4 ('e')`, `left=2` | `last_seen={'p':0, 'w':2, 'k':3, 'e':4}`, `max_len=3` ("wke") |
| 6 | `right=5 ('w')`, `left=2` | Duplicate 'w'! `left = max(2, 2 + 1) = 3`. `last_seen['w']=5`, `max_len=3` |

---

## Edge Cases

- Empty string (`""`) → returns `0`.
- All identical characters (`"bbbbb"`) → returns `1`.
- All unique characters (`"abcdef"`) → returns length of string (`6`).
- Single space or symbol (`" "`) → returns `1`.

---

## Mistakes

- Forgetting to check `last_seen[char] >= left` before updating `left` pointer, causing `left` to jump backward.
- Not handling empty inputs cleanly.
- User mistake: No specific note provided.

---

## Complexity

Time: O(N) → Single pass over string of length N.
Space: O(min(N, M)) → Storage for HashMap, bounded by charset size M (e.g., 128 for ASCII).

---

## Similar Problems

- [Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/) - Medium
- [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) - Medium
- [Subarrays with K Distinct Integers](https://leetcode.com/problems/subarrays-with-k-distinct-integers/) - Hard
- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) - Hard

---

## Tags and Properties

- #dsa #important #revisit #slidingwindow #hashmap #strings
- **Concepts:** [[Sliding Window]], [[Two Pointers]], [[HashMap]]
- **Revision Date:** 2026-09-13
- **Problem Link:** [Longest Substring Without Repeating Characters - LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-15)
- [ ] Day 7 Revision (2026-09-20)
- [ ] Day 15 Revision (2026-09-28)
- [ ] Day 30 Revision (2026-10-13)
