---
created: 2026-09-25
revisions:
  - 2026-09-27
  - 2026-10-02
  - 2026-10-10
  - 2026-10-25
---

# Number Of Substrings Containing All Three Characters

---

## Metadata & Placement Tags

- **Folder:** Sliding Window
- **Target Companies:** #Amazon #Microsoft #Google #Adobe
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #slidingwindow [[Sliding Window]], #twopointers [[Two Pointers]], #hashmap [[HashMap]]

## Pattern

Sliding Window (At Most / Shrinking Window) or Last Seen Index Tracking

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

For any valid window `[left, right]` containing at least one `'a'`, `'b'`, and `'c'`, all substrings starting from `0` to `left` and ending at `right` are also valid. Thus, adding `left + 1` (or `min(last_a, last_b, last_c) + 1`) to the total count gives all valid substrings ending at `right`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Track the last seen index of characters `'a'`, `'b'`, and `'c'`. For each index `i`, valid substrings ending at `i` count is `min(last['a'], last['b'], last['c']) + 1`.

---

## Approach

### Brute Force
- Generate all possible substrings using nested loops and check if each contains `'a'`, `'b'`, and `'c'`.
- Time: $O(N^2)$ or $O(N^3)$ | Space: $O(1)$

### Better
- Use a sliding window to maintain character counts. Expand `right` until valid, then increment `count` by `len(s) - right` and shrink `left`.
- Time: $O(N)$ | Space: $O(1)$

### Optimal
- Iterate `right` pointer from `0` to `n - 1`. Update the last seen index of `s[right]`.
- At each step, add `min(last_seen['a'], last_seen['b'], last_seen['c']) + 1` to `total_count` (if all three have been seen).
- Time: $O(N)$ | Space: $O(1)$

---

## Code (Python)

```python
class Solution:
    def numberOfSubstrings(self, s: str) -> int:
        # Track the last seen 0-based index of 'a', 'b', and 'c'
        last_seen = {'a': -1, 'b': -1, 'c': -1}
        total_substrings = 0

        for current_index, char in enumerate(s):
            # Update the last seen position of the current character
            last_seen[char] = current_index

            # Find the leftmost start index among 'a', 'b', and 'c'
            min_last_index = min(last_seen['a'], last_seen['b'], last_seen['c'])

            # If all 3 characters have appeared at least once, min_last_index >= 0
            if min_last_index != -1:
                # All substrings starting from 0 up to min_last_index and ending at current_index are valid
                total_substrings += min_last_index + 1

        return total_substrings
```

---

## Dry Run (Smart Example)

Input: `s = "abcabc"`

| Step | `current_index` (`char`) | `last_seen` (`a, b, c`) | `min_last_index` | `total_substrings` Added | Total |
|---|---|---|---|---|---|
| 1 | 0 (`'a'`) | `{0, -1, -1}` | -1 | 0 (incomplete) | 0 |
| 2 | 1 (`'b'`) | `{0, 1, -1}` | -1 | 0 (incomplete) | 0 |
| 3 | 2 (`'c'`) | `{0, 1, 2}` | 0 | 0 + 1 = 1 | 1 |
| 4 | 3 (`'a'`) | `{3, 1, 2}` | 1 | 1 + 1 = 2 | 3 |
| 5 | 4 (`'b'`) | `{3, 4, 2}` | 2 | 2 + 1 = 3 | 6 |
| 6 | 5 (`'c'`) | `{3, 4, 5}` | 3 | 3 + 1 = 4 | 10 |

---

## Edge Cases

- **Minimum Length String (`"abc"`):** Returns `1` correctly.
- **Missing Character (`"aabb"`):** No character `'c'` seen, returns `0`.
- **Repeated Prefix (`"aaabc"`):** Works correctly as `min_last_index` picks the latest valid position of `'a'`.

---

## Mistakes

- Using nested loops leading to TLE ($O(N^2)$).
- Forgetting that all prefixes before `left` in a valid sliding window form valid substrings.
- User mistake: No specific note provided.

---

## Complexity

Time: $O(N)$ → Single pass through string of length $N$.
Space: $O(1)$ → Fixed auxiliary space for storing indices of 3 characters.

---

## Similar Problems

- [Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/) - Hard
- [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/) - Medium
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #slidingwindow #strings
- [[Sliding Window]] [[Two Pointers]]
- **Revision Date:** 2026-09-25
- **Problem Link:** [Number of Substrings Containing All Three Characters - LeetCode](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-27)
- [ ] Day 7 Revision (2026-10-02)
- [ ] Day 15 Revision (2026-10-10)
- [ ] Day 30 Revision (2026-10-25)
