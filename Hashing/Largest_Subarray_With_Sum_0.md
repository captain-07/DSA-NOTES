---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Largest Subarray With Sum 0

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Ola #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #prefixsum [[Prefix Sum]], #hashmap [[HashMap]]

## Pattern

Prefix Sum + HashMap (Difference Pattern)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

If the **Prefix Sum** at index `i` is $S$ and the Prefix Sum at index `j` is also $S$, the sum of the subarray between $i+1$ and $j$ must be **zero**. We use a HashMap to store the *first* occurrence of each prefix sum to maximize the distance.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Store `prefix_sum` in a map. If seen again, calculate `current_index - first_occurrence_index`. Handle `sum == 0` separately as length `i + 1`.

---

## Approach

### Brute Force
- Check all possible subarrays $(i, j)$ and calculate their sum.
- Time Complexity: $O(N^2)$

### Optimal
1. Maintain `curr_sum` while iterating through the array.
2. If `curr_sum == 0`, the largest subarray so far is `i + 1`.
3. If `curr_sum` exists in the HashMap, a zero-sum subarray exists. Update `max_len = max(max_len, i - map[curr_sum])`.
4. If `curr_sum` is NOT in the HashMap, store it with its current index: `map[curr_sum] = i`.
5. **Note:** We only store the *first* occurrence to ensure we get the *longest* subarray.

---

## Code (Python)

```python
class Solution:
    def maxLen(self, n, arr):
        # Map to store the first occurrence of prefix_sum
        hash_map = {}
        max_len = 0
        curr_sum = 0
        
        for i in range(n):
            curr_sum += arr[i]
            
            if curr_sum == 0:
                # Subarray starts from index 0
                max_len = i + 1
            
            if curr_sum in hash_map:
                # Calculate distance from first occurrence
                max_len = max(max_len, i - hash_map[curr_sum])
            else:
                # Only store the first time we see this sum
                hash_map[curr_sum] = i
                
        return max_len
```

---

## Dry Run (Smart Example)

Input: `arr = [1, 2, -2, 4, -4]`

| Step | Index | Val | `curr_sum` | HashMap `{Sum: Index}` | `max_len` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 1 | 1 | `{1: 0}` | 0 | First sum, add to map. |
| 2 | 1 | 2 | 3 | `{1: 0, 3: 1}` | 0 | New sum, add to map. |
| 3 | 2 | -2 | 1 | `{1: 0, 3: 1}` | $2-0 = 2$ | `1` seen at index 0. |
| 4 | 3 | 4 | 5 | `{1: 0, 3: 1, 5: 3}` | 2 | New sum, add to map. |
| 5 | 4 | -4 | 1 | `{1: 0, 3: 1, 5: 3}` | $4-0 = 4$ | `1` seen at index 0. |

Final Result: **4** (Subarray: `[2, -2, 4, -4]`)

---

## Edge Cases

- **All zeros:** Returns array length.
- **No zero sum:** Returns 0.
- **Single element 0:** Returns 1.
- **Sum becomes 0 at the end:** Handled by `curr_sum == 0` check.
- **Large negatives/positives:** Handled by `curr_sum` logic.

---

## Mistakes

- **Updating index in HashMap:** Never update the index if the sum is already present; you want the *earliest* index for maximum length.
- **Forgetting `curr_sum == 0`:** If the sum is zero, the subarray starts from the very beginning (index 0).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(N)$ → Single pass through the array.  
Space: $O(N)$ → HashMap stores at most $N$ prefix sums.

---

## Similar Problems

- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium
- [Longest Subarray with Sum K](https://www.geeksforgeeks.org/longest-sub-array-sum-k/) - Medium
- [Subarray Sums Divisible by K](https://leetcode.com/problems/subarray-sums-divisible-by-k/) - Medium
- [Contiguous Array (Binary Array 0s and 1s)](https://leetcode.com/problems/contiguous-array/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #prefixsum #hashmap
- [[Prefix Sum]] [[HashMap]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [Largest subarray with 0 sum - GFG](https://www.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
