---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Count Subarrays With Given Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]]
  - #prefixsum [[Prefix Sum]]
  - #arrays [[Arrays]]

## Pattern
Prefix Sum + HashMap Frequency Tracking

---
## Difficulty
Medium #medium

---

## ⚡ Key Idea (Core Insight)
For any index $i$ with prefix sum $S_i$, we need to find how many previous indices $j$ had a prefix sum $S_j$ such that $S_i - S_j = k$. This rearranges to $S_j = S_i - k$. A HashMap stores the frequency of all seen prefix sums to provide $O(1)$ lookups for $S_j$.

---

## ⚡ Quick Recall (VERY IMPORTANT)
Use a map to store `{prefix_sum: frequency}`. At each step, `count += map[current_sum - k]`. Initialize map with `{0: 1}` to handle subarrays starting from index 0.

---

## Approach

### Brute Force
- Check every possible subarray $(i, j)$ and calculate its sum.
- **Time:** $O(N^2)$ (or $O(N^3)$ without prefix sum optimization).

### Better
- Precompute prefix sums in an array. Subarray sum $(i, j) = P[j] - P[i-1]$.
- **Time:** $O(N^2)$ to iterate all pairs $(i, j)$.
- **Space:** $O(N)$.

### Optimal
- Use a running `current_sum`. 
- Check if `(current_sum - k)` exists in the HashMap.
- Update the count with the frequency of `(current_sum - k)`.
- Store/update `current_sum` frequency in the map.
- **Time:** $O(N)$.
- **Space:** $O(N)$.

---

## Code (Python)

```python
class Solution:
    def subarraySum(self, nums: list[int], k: int) -> int:
        # count: stores total subarrays found
        # curr_sum: running prefix sum
        # prefix_map: {sum: frequency}
        count = 0
        curr_sum = 0
        prefix_map = {0: 1} # Base case: sum 0 seen once
        
        for num in nums:
            curr_sum += num
            
            # If (curr_sum - k) was seen before, it means a 
            # subarray with sum k exists between that point and now
            diff = curr_sum - k
            if diff in prefix_map:
                count += prefix_map[diff]
                
            # Update frequency of current prefix sum
            prefix_map[curr_sum] = prefix_map.get(curr_sum, 0) + 1
            
        return count
```

---

## Dry Run (Smart Example)
**Input:** `nums = [1, -1, 1, 1], k = 0`

| Step | Num | `curr_sum` | `diff` (sum-k) | `prefix_map` | `count` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | - | 0 | - | `{0:1}` | 0 | Initial state |
| 1 | 1 | 1 | 1 | `{0:1, 1:1}` | 0 | `1` not in map |
| 2 | -1 | 0 | 0 | `{0:2, 1:1}` | 1 | `0` in map, `count += 1` |
| 3 | 1 | 1 | 1 | `{0:2, 1:2}` | 2 | `1` in map, `count += 1` |
| 4 | 1 | 2 | 2 | `{0:2, 1:2, 2:1}` | 2 | `2` not in map |

---

## Edge Cases
- **k = 0:** Requires prefix sum to repeat to count (handled by map).
- **Negative Numbers:** Prefix sum is not monotonic; HashMap is mandatory (Two Pointers fails).
- **Empty Array:** Should return 0.
- **Single Element:** Check if `nums[0] == k`.

---

## Mistakes
- Forgetting to initialize the map with `{0: 1}`.
- Using Two Pointers (only works for non-negative numbers).
- Updating the map *before* checking the difference (can count the current element incorrectly if $k=0$).
- **User Mistake:** No specific note provided.

---

## Complexity
- **Time:** $O(N)$ → Single pass through the array with $O(1)$ average map operations.
- **Space:** $O(N)$ → In the worst case (all unique prefix sums), the map stores $N$ entries.

---

## Similar Problems
- [Subarray Sums Divisible by K](https://leetcode.com/problems/subarray-sums-divisible-by-k/) - Medium
- [Path Sum III](https://leetcode.com/problems/path-sum-iii/) - Medium
- [Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum/) - Medium
- [Two Sum](https://leetcode.com/problems/two-sum/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #interview-favorite
- [[Prefix Sum]] [[HashMap]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode - Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
