---
created: 2026-08-15
revisions:
  - 2026-08-17
  - 2026-08-22
  - 2026-08-30
  - 2026-09-14
---

# Minimum Operations To Make A Rotated Palindrome I

---

## Metadata & Placement Tags

- **Target Companies:** #Google #Meta #Microsoft #Amazon
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #dynamic-programming [[Dynamic Programming]], #string [[String]], #palindrome [[Palindrome]]

---
## Pattern

Dynamic Programming + String Rotation (or Doubling)

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

A string $S$ can be rotated into a palindrome if and only if it contains a palindromic subsequence of length $N$ within the doubled string $S + S$ (specifically, restricted to substrings of length $\le N$). The minimum operations to make it a palindrome equals $N - \text{LPS}(T)$ for a valid rotation, where $\text{LPS}$ is the Longest Palindromic Subsequence.

---
## ⚡ Quick Recall

Double the string to $S + S$, find the Longest Palindromic Subsequence (LPS) of length $\le N$ for all window shifts, and return $N - \text{max\_LPS}$.

---
## Approach

### Brute Force
- Generate all $N$ rotations of $S$. For each rotation, find the Longest Palindromic Subsequence (LPS) using standard DP.
- Time Complexity: $O(N^3)$
- Space Complexity: $O(N^2)$

### Optimal
- Double the string to $T = S + S$. Compute DP table for LPS of $T$.
- Since we only care about sub-segments of length $\le N$, the answer is $N - \max_{0 \le i < N} (\text{LPS}(T[i \dots i+N-1]))$.
- Time Complexity: $O(N^2)$
- Space Complexity: $O(N^2)$

---
## Code (Python)

```python
class Solution:
    def minOpsRotatedPalindrome(self, s: str) -> int:
        n = len(s)
        if n <= 1:
            return 0

        # Double the string to handle rotations
        t = s + s
        m = 2 * n

        # dp[i][j] stores length of LPS in t[i...j]
        dp = [[0] * m for _ in range(m)]

        # Base cases: single characters
        for i in range(m):
            dp[i][i] = 1

        # Fill DP table
        for length in range(2, n + 1):  # Only need up to length n
            for i in range(m - length + 1):
                j = i + length - 1
                if t[i] == t[j]:
                    dp[i][j] = dp[i+1][j-1] + 2
                else:
                    dp[i][j] = max(dp[i+1][j], dp[i][j-1])

        # Find maximum LPS of length <= n across all rotations
        max_lps = 0
        for i in range(n):
            max_lps = max(max_lps, dp[i][i + n - 1])

        return n - max_lps
```

---
## Dry Run (Smart Example)

Input: `s = "aab"` (Length $N = 3$), Doubled $T = \text{"aabaab"}$

| Step | Substring Window | DP calculation / Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `T = "aabaab"` | Initialize `dp[i][i] = 1` | Base case for single characters. |
| 2 | Length 2 & 3 DP | `dp[0][2]` for `"aab"` $\to 2$ (`"aa"`) | Standard LPS DP values calculated for all windows. |
| 3 | Window 0: `T[0:3] = "aab"` | `dp[0][2] = 2` | LPS is `"aa"` (length 2). |
| 4 | Window 1: `T[1:4] = "aba"` | `dp[1][3] = 3` | LPS is `"aba"` (length 3). |
| 5 | Window 2: `T[2:5] = "baa"` | `dp[2][4] = 2` | LPS is `"aa"` (length 2). |
| 6 | Max & Result | `max_lps = 3`, Return $3 - 3 = 0$ | "aba" is a rotated palindrome requiring 0 operations. |

---
## Edge Cases

- **Already a Palindrome** (`"aba"`): LPS is $N$, returns $0$.
- **All Distinct Characters** (`"abc"`): LPS is $1$, returns $N - 1$.
- **String with duplicates** (`"aab"`): Handled correctly via doubled sliding window.
- **Single character** (`"a"`): Handled by base case, returns $0$.

---
## Mistakes

- **User Mistake:** No specific note provided.
- Failing to restrict the LPS window length to $N$, which can falsely match characters beyond the boundaries of a single rotation.
- Not doubling the string to simulate rotation efficiently, leading to repeated DP state calculations.

---
## Complexity

- **Time:** $O(N^2)$ $\to$ We populate a DP table of size $2N \times 2N$ up to step width $N$.
- **Space:** $O(N^2)$ $\to$ To store the DP transition table of size $2N \times 2N$.

---
## Similar Problems

- [Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/) - Medium
- [Minimum Insertion Steps to Make a String Palindrome](https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/) - Medium
- [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) - Easy

---
## Tags and Properties

- #dsa #important #revisit #dynamic-programming #string-rotation
- [[Dynamic Programming]]
- [[String Algorithms]]
- **Revision Date:** 2026-08-15
- **Problem Link:** [Leetcode - Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-17)
- [ ] Day 7 Revision (2026-08-22)
- [ ] Day 15 Revision (2026-08-30)
- [ ] Day 30 Revision (2026-09-14)
