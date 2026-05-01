---
created: 2026-05-01
revisions:
  - 2026-05-03
  - 2026-05-08
  - 2026-05-16
  - 2026-05-31
---

# Count Number Of Substrings

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Samsung #Walmart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #slidingwindow [[Sliding Window]]
  - #hashmap [[Hash Map]]
  - #strings [[Strings]]

---
## Pattern

Sliding Window (At Most K trick)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Calculating substrings with **exactly** $k$ distinct characters directly is difficult because the window doesn't shrink monotonically.  
**Insight:** `Exactly(K) = AtMost(K) - AtMost(K-1)`.  
By calculating the number of substrings with *at most* $k$ characters, we can use a standard sliding window where every valid window `[left, right]` contributes `right - left + 1` substrings.

---

## ⚡ Quick Recall (VERY IMPORTANT)

`solve(k) - solve(k-1)` where `solve(x)` counts substrings with $\le x$ distinct characters using sliding window.

---

## Approach

### Brute Force
- Generate all possible substrings using nested loops and count distinct characters using a set.
- **Time Complexity:** $O(N^2)$
- **Space Complexity:** $O(K)$

### Optimal
1. Define a helper function `atMost(s, k)` to count substrings with $\le k$ distinct characters.
2. Use two pointers (`left`, `right`) and a frequency map (array of size 26).
3. Expand `right`. If the number of distinct characters exceeds $k$, shrink `left` until distinct count $\le k$.
4. At each step, the number of substrings ending at `right` is `right - left + 1`.
5. Return `atMost(s, k) - atMost(s, k-1)`.

---

## Code (Python)

```python
class Solution:
    def countSubstrings(self, s: str, k: int) -> int:
        def atMost(s, k):
            if k < 0: return 0
            
            left = 0
            count = 0
            distinct_cnt = 0
            freq = {}
            
            for right in range(len(s)):
                # Add current character
                char_r = s[right]
                freq[char_r] = freq.get(char_r, 0) + 1
                if freq[char_r] == 1:
                    distinct_cnt += 1
                
                # Shrink window if distinct characters > k
                while distinct_cnt > k:
                    char_l = s[left]
                    freq[char_l] -= 1
                    if freq[char_l] == 0:
                        distinct_cnt -= 1
                    left += 1
                
                # Number of substrings ending at 'right' with at most k distinct
                count += (right - left + 1)
                
            return count

        return atMost(s, k) - atMost(s, k - 1)
```

---

## Dry Run (Smart Example)

**Input:** `s = "aba"`, `k = 2`  
**Goal:** `atMost(2) - atMost(1)`

| Step | right | char | Window | atMost(2) count | atMost(1) count | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 'a' | "a" | +1 (1) | +1 (1) | Both $\le 2$ and $\le 1$ |
| 2 | 1 | 'b' | "ab" | +2 (3) | +1 (2) | `atMost(1)` shrinks to "b" |
| 3 | 2 | 'a' | "ba" | +3 (6) | +1 (3) | `atMost(1)` shrinks to "a" |

**Result:** $6 - 3 = 3$ (Substrings: "ab", "ba", "aba")

---

## Edge Cases

- **$k=1$:** Correctly calculates `atMost(1) - atMost(0)`.
- **$k >$ distinct characters in $s$:** `atMost(k-1)` will count all valid substrings, `atMost(k)` will be the same, result 0.
- **Empty String:** Loop won't execute, returns 0.
- **All identical characters:** e.g., "aaaa", $k=1$. Result will be $N(N+1)/2$.

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Direct Calculation:** Trying to shrink the window as soon as you hit $k$ distinct characters (incorrect, because more characters might still keep it at $k$).
- **Off-by-one:** Forgetting that `right - left + 1` represents the number of substrings *ending* at the current index.
- **k=0 Case:** If the helper function doesn't handle `k=0` or `k < 0`, it might crash or return incorrect counts.

---

## Complexity

- **Time:** $O(N)$ → Each pointer (`left`, `right`) travels the string at most once.
- **Space:** $O(1)$ → Frequency map size is capped at 26 (alphabet size).

---

## Similar Problems

- [Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/) - Hard
- [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/) - Medium
- [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) - Medium
- [Number of Substrings Containing All Three Characters](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #slidingwindow #strings
- [[Sliding Window]] [[Hash Map]]
- **Revision Date:** 2026-05-01
- **Problem Link:** [GeeksforGeeks - Count number of substrings](https://www.geeksforgeeks.org/problems/count-number-of-substrings4522/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-03)
- [ ] Day 7 Revision (2026-05-08)
- [ ] Day 15 Revision (2026-05-16)
- [ ] Day 30 Revision (2026-05-31)
