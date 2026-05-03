---
created: 2026-05-03
revisions:
  - 2026-05-05
  - 2026-05-10
  - 2026-05-18
  - 2026-06-02
---

# Sum Of Beauty Of All Substring

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #GoldmanSachs #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #strings [[Strings]], #hashmap [[HashMap]], #frequency-array [[Frequency Array]]

## Pattern

Nested Loops + Dynamic Frequency Tracking  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The beauty of a substring is the difference between the maximum and minimum frequencies of characters present in it. Since $N$ is typically small ($\le 500$), an $O(N^2)$ approach is optimal. We iterate through all starting positions and expand the substring, updating a frequency array/map in real-time to avoid re-calculating from scratch.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Nested loops for all $i, j$; maintain a `count[26]` array; for each $j$, update count and compute `max(f) - min(f > 0)`.

---

## Approach

### Brute Force
- Generate all possible substrings $O(N^2)$, then for each substring, count character frequencies $O(N)$.
- **Time Complexity:** $O(N^3)$

### Optimal
- Use a nested loop where the outer loop marks the start of the substring.
- The inner loop expands the substring one character at a time.
- Maintain a frequency array of size 26.
- In each step of the inner loop, update the frequency of the current character and calculate `max_freq - min_freq`.
- **Note:** `min_freq` must only consider characters with frequency $> 0$.

---

## Code (Python)

```python
class Solution:
    def beautySum(self, s: str) -> int:
        total_beauty = 0
        n = len(s)
        
        for i in range(n):
            # Frequency array for substring starting at index i
            freq = [0] * 26
            for j in range(i, n):
                # Update frequency of character at index j
                freq[ord(s[j]) - ord('a')] += 1
                
                # Calculate max and min frequencies
                max_f = 0
                min_f = float('inf')
                
                for f in freq:
                    if f > 0:
                        max_f = max(max_f, f)
                        min_f = min(min_f, f)
                
                # Add beauty of current substring s[i:j+1]
                if max_f > 0:
                    total_beauty += (max_f - min_f)
                    
        return total_beauty
```

---

## Dry Run (Smart Example)

**Input:** `s = "aabcb"`

| Step | Substring | Frequencies | max_f | min_f | Beauty |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `a` | a:1 | 1 | 1 | 0 |
| 2 | `aa` | a:2 | 2 | 2 | 0 |
| 3 | `aab` | a:2, b:1 | 2 | 1 | 1 |
| 4 | `aabc` | a:2, b:1, c:1 | 2 | 1 | 1 |
| 5 | `aabcb` | a:2, b:2, c:1 | 2 | 1 | 1 |
| ... | ... | ... | ... | ... | ... |
| **Final** | **Sum** | | | | **5** (Total for all) |

---

## Edge Cases

- **Single Character:** Beauty is always 0.
- **All Same Characters:** `aaaaa` → Beauty is always 0.
- **All Unique Characters:** `abcde` → Beauty is always 0.
- **Maximum Constraints:** $N=500$ ensures $O(26 \cdot N^2)$ passes within time limits.

---

## Mistakes

- **Minimum Frequency Zero:** Including characters with 0 frequency in the `min_f` calculation (results in 0 beauty always).
- **Redundant Calculation:** Re-calculating frequencies for each substring from scratch ($O(N^3)$).
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(N^2 \times 26)$ → Nested loops for all substrings, inner loop checks 26 character frequencies.  
- **Space:** $O(26) \approx O(1)$ → Constant space for the frequency array.

---

## Similar Problems

- [Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/) - Hard
- [Number of Substrings Containing All Three Characters](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/) - Medium
- [Frequency of the Most Frequent Element](https://leetcode.com/problems/frequency-of-the-most-frequent-element/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #strings #slidingwindow
  - [[String]] [[HashMap]] [[Subarray_Pattern]]
  - **Revision Date:** 2026-05-03
  - **Problem Link:** [LeetCode 1781 - Sum of Beauty of All Substrings](https://leetcode.com/problems/sum-of-beauty-of-all-substrings/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-05)
- [ ] Day 7 Revision (2026-05-10)
- [ ] Day 15 Revision (2026-05-18)
- [ ] Day 30 Revision (2026-06-02)
