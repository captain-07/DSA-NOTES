---
created: 2026-09-13
revisions:
  - 2026-09-15
  - 2026-09-20
  - 2026-09-28
  - 2026-10-13
---

# Largest Subarray With Sum 0

---

## Metadata & Placement Tags

- **Folder:** Arrays
- **Target Companies:** #Amazon #Microsoft #MakeMyTrip #Paytm
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #hashmap [[HashMap]], #prefixsum [[Prefix Sum]], #arrays [[Arrays]]

## Pattern

Prefix Sum + HashMap

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

If prefix sum up to index `i` is equal to prefix sum up to index `j` (`j > i`), then the sum of elements from index `i + 1` to `j` is 0. Storing the first occurrence of each prefix sum in a hash map allows us to find the maximum distance between identical prefix sums.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Track cumulative prefix sum. Store `sum -> first_index` in hash map. If sum repeats, subarray length is `current_index - first_index`.

---

## Approach

### Brute Force
- Check all possible subarrays, compute their sum, and track the maximum length where sum equals 0.
- **Time:** O(N²) | **Space:** O(1)

### Optimal
- Maintain a running prefix sum and a hash map storing `{prefix_sum: first_seen_index}`.
- Initialize `max_len = 0` and prefix sum `0` at index `-1`.
- Iterate through the array:
  1. Add current element to prefix sum.
  2. If prefix sum is 0, subarray from index 0 to `i` has sum 0 (`max_len = i + 1`).
  3. If prefix sum is already in hash map, update `max_len = max(max_len, i - hashmap[prefix_sum])`.
  4. If prefix sum is NOT in hash map, store `hashmap[prefix_sum] = i`.
- Return `max_len`.

---

## Code (Python)

```python
class Solution:
    def maxLen(self, arr: list[int], n: int) -> int:
        # Map to store first occurrence of prefix sum: {prefix_sum: index}
        prefix_sum_map = {}

        max_length = 0
        current_sum = 0

        for index in range(n):
            current_sum += arr[index]

            # Case 1: Subarray starting from index 0 has sum 0
            if current_sum == 0:
                max_length = index + 1

            # Case 2: Prefix sum seen before -> subarray between first occurrence and now sums to 0
            elif current_sum in prefix_sum_map:
                previous_index = prefix_sum_map[current_sum]
                max_length = max(max_length, index - previous_index)

            # Case 3: First time seeing this prefix sum -> store index
            else:
                prefix_sum_map[current_sum] = index

        return max_length
```

---

## Dry Run (Smart Example)

Input: `arr = [15, -2, 2, -8, 1, 7, 10, 23]`, `n = 8`

| Step | Index | Value | Current Sum | Map State `{sum: idx}` | Action / Explanation | `max_len` |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | 0 | 15 | 15 | `{15: 0}` | First seen 15, store index 0 | 0 |
| 2 | 1 | -2 | 13 | `{15: 0, 13: 1}` | First seen 13, store index 1 | 0 |
| 3 | 2 | 2 | 15 | `{15: 0, 13: 1}` | 15 seen at index 0 -> len = 2 - 0 = 2 | 2 |
| 4 | 3 | -8 | 7 | `{15: 0, 13: 1, 7: 3}` | First seen 7, store index 3 | 2 |
| 5 | 4 | 1 | 8 | `{..., 8: 4}` | First seen 8, store index 4 | 2 |
| 6 | 5 | 7 | 15 | `{...}` | 15 seen at index 0 -> len = 5 - 0 = 5 | 5 |

---

## Edge Cases

- **All zero array `[0, 0, 0]`:** Output should be length of array (3).
- **No subarray with sum 0 `[1, 2, 3]`:** Output should be 0.
- **Entire array sums to 0 `[1, -1, 2, -2]`:** Handled when `current_sum == 0`.
- **Single element array `[0]` vs `[5]`:** Returns 1 for `[0]` and 0 for `[5]`.

---

## Mistakes

- Updating the hash map index when a prefix sum is seen again (must ONLY store the *first* occurrence to maximize length).
- Forgetting to handle the case where prefix sum itself becomes `0`.
- User mistake: No specific note provided.

---

## Complexity

Time: O(N) → Single pass traversal over array with O(1) hash map operations.
Space: O(N) → Extra space used by hash map to store up to N prefix sums.

---

## Similar Problems

- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium
- [Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum/) - Medium
- [Contiguous Array](https://leetcode.com/problems/contiguous-array/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #prefixsum [[Prefix Sum]]
- #hashmap [[HashMap]]
- **Revision Date:** 2026-09-13
- **Problem Link:** [GeeksforGeeks - Largest Subarray With 0 Sum](https://www.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-15)
- [ ] Day 7 Revision (2026-09-20)
- [ ] Day 15 Revision (2026-09-28)
- [ ] Day 30 Revision (2026-10-13)
