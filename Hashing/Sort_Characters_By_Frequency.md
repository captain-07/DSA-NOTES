---
created: 2026-05-01
revisions:
  - 2026-05-03
  - 2026-05-08
  - 2026-05-16
  - 2026-05-31
---

# Sort Characters By Frequency

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Bloomberg #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]]
  - #sorting [[Sorting]]
  - #heap [[Heap]]
  - #bucketsort [[Bucket Sort]]

## Pattern
Frequency Map + Bucket Sort

---
## Difficulty
Medium #medium

---

## ⚡ Key Idea (Core Insight)
The frequency of any character is bounded by the string length $N$. By using frequencies as indices in a "bucket" array, we can group characters with the same count and reconstruct the string in linear time, bypassing $O(N \log N)$ sorting.

---

## ⚡ Quick Recall (VERY IMPORTANT)
Count frequencies → Create buckets where `index = frequency` → Iterate buckets from right to left to build the result.

---

## Approach

### Brute Force
- Generate all permutations of the string, check if sorted by frequency, and pick the valid one.
- Time: $O(N!)$

### Better
- Use a HashMap to count frequencies, then sort unique characters by their counts.
- Time: $O(N + K \log K)$, where $K$ is the number of unique characters.

### Optimal (Bucket Sort)
1. Count frequencies using a HashMap.
2. Create an array of lists (buckets) where the index represents the frequency.
3. Populate buckets: `buckets[freq].append(char)`.
4. Iterate the buckets from $N$ down to $1$ and append `char * freq` to the result list.
5. Join and return.

---

## Code (Python)

```python
from collections import Counter

class Solution:
    def frequencySort(self, s: str) -> str:
        if not s:
            return ""
        
        # 1. Count frequencies
        counts = Counter(s)
        max_freq = max(counts.values())
        
        # 2. Create buckets: index represents frequency
        buckets = [[] for _ in range(max_freq + 1)]
        for char, freq in counts.items():
            buckets[freq].append(char)
            
        # 3. Build result from highest frequency to lowest
        res = []
        for freq in range(max_freq, 0, -1):
            for char in buckets[freq]:
                res.append(char * freq)
                
        return "".join(res)
```

---

## Dry Run (Smart Example)
**Input:** `s = "tree"`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `counts = {'t':1, 'r':1, 'e':2}` | Frequency mapping. |
| 2 | `buckets = [[], ['t', 'r'], ['e'], []]` | `e` at index 2; `t, r` at index 1. |
| 3 | `freq=2, char='e'` | Append `e * 2` -> `res = ["ee"]`. |
| 4 | `freq=1, char='t', 'r'` | Append `t*1`, `r*1` -> `res = ["ee", "t", "r"]`. |
| 5 | `"".join(res)` | Output: `"eetr"` (or `"eert"`). |

---

## Edge Cases
- **Empty String:** Handled by early return or empty loop.
- **Single Character:** Frequency 1, works naturally.
- **All Same Characters:** `max_freq = N`, one bucket entry.
- **Case Sensitivity:** `'A'` and `'a'` are different (HashMap handles this).
- **Numbers/Symbols:** Handled correctly by Unicode mapping in HashMap.

---

## Mistakes
- **User Mistake:** No specific note provided (Initial lack of structured revision material).
- **Case Sensitivity:** Treating 'A' and 'a' as the same character.
- **Inefficient Sorting:** Using $O(N \log N)$ when $O(N)$ is possible via Bucket Sort.
- **String Concatenation:** Using `s += char` in a loop (O(N²)) instead of `"".join(list)` (O(N)).

---

## Complexity
- **Time:** $O(N)$ → One pass to count, one pass to fill buckets, one pass to build result.
- **Space:** $O(N)$ → To store the frequency map, buckets, and the final output string.

---

## Similar Problems
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) - Medium
- [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/) - Easy
- [Sort Characters By Frequency II](https://leetcode.com/problems/sort-array-by-increasing-frequency/) - Easy

---

## Tags and Properties
- #dsa #important #revisit
- #hashmap [[HashMap]] #bucketsort [[Bucket Sort]] #string [[String]]
- **Revision Date:** 2026-05-01
- **Problem Link:** [LeetCode - Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-03)
- [ ] Day 7 Revision (2026-05-08)
- [ ] Day 15 Revision (2026-05-16)
- [ ] Day 30 Revision (2026-05-31)
