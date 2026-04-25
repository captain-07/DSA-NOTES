---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Longest Subarray With Sum K

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #slidingwindow [[Sliding Window]], #prefixsum [[Prefix Sum]], #hashmap [[HashMap]], #twopointers [[Two Pointers]]

---
## Pattern

1. **Prefix Sum + HashMap** (Handles Positives, Negatives, and Zeros)
2. **Two Pointers / Sliding Window** (Optimal ONLY for Positives + Zeros)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

- **General (Prefix Sum):** If the current prefix sum is $S$, we search for a previous prefix sum $S - K$ in our HashMap. If found, the subarray between that index and current index sums to $K$.
- **Positives Only (Two Pointers):** Since adding elements strictly increases the sum, we can use a dynamic window. Expand `right` to increase sum; shrink `left` if `sum > K`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **Map Approach:** Store `first_occurrence` of each prefix sum to maximize length. 
- **Two Pointers:** Only works if the array is non-negative (monotonicity).

---

## Approach

### Brute Force
- Iterate through all possible subarrays using two nested loops, calculate sum, and track max length.
- **Time Complexity:** $O(N^2)$
- **Space Complexity:** $O(1)$

### Optimal (For Positives + Negatives)
- Use a **HashMap** to store `prefix_sum : index`.
- For each index `i`, check if `prefix_sum - K` exists in the Map.
- If it does, `length = i - Map[prefix_sum - K]`.
- **Note:** Only add `prefix_sum` to the map if it doesn't already exist (to keep the index as small as possible for max length).

### Optimal (For Positives Only)
- Initialize `left = 0`, `right = 0`, `current_sum = 0`.
- Move `right` and add to `current_sum`.
- If `current_sum > K`, subtract `arr[left]` and increment `left` until `current_sum <= K`.
- If `current_sum == K`, update `max_len`.

---

## Code (Python)

```python
class Solution:
    def longestSubarrayWithSumK_General(self, nums: list[int], k: int) -> int:
        """Handles positives, negatives, and zeros using Prefix Sum."""
        prefix_map = {0: -1} # sum : index
        current_sum = 0
        max_len = 0
        
        for i, val in enumerate(nums):
            current_sum += val
            
            # Check if (current_sum - k) exists
            if (current_sum - k) in prefix_map:
                max_len = max(max_len, i - prefix_map[current_sum - k])
            
            # Only store if sum is seen for the first time (to maximize length)
            if current_sum not in prefix_map:
                prefix_map[current_sum] = i
                
        return max_len

    def longestSubarrayWithSumK_Positives(self, nums: list[int], k: int) -> int:
        """Optimized Two Pointers approach for non-negative numbers."""
        left = 0
        current_sum = 0
        max_len = 0
        
        for right in range(len(nums)):
            current_sum += nums[right]
            
            while left <= right and current_sum > k:
                current_sum -= nums[left]
                left += 1
                
            if current_sum == k:
                max_len = max(max_len, right - left + 1)
                
        return max_len
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 2, 3, 1, 1, 1], k = 3` (Two Pointers)

| Step | Right | Val | Sum | Action | Left | Max Len |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 1 | 1 | sum < k, expand | 0 | 0 |
| 2 | 1 | 2 | 3 | sum == k | 0 | 2 (sub: [1,2]) |
| 3 | 2 | 3 | 6 | sum > k, shrink left | 3 | 2 |
| 4 | 3 | 1 | 1 | sum < k | 3 | 2 |
| 5 | 4 | 1 | 2 | sum < k | 3 | 2 |
| 6 | 5 | 1 | 3 | sum == k | 3 | 3 (sub: [1,1,1]) |

---

## Edge Cases

- **K = 0:** If negatives exist, prefix sum handles it; otherwise, only counts zeros.
- **All Negatives:** Subarray sum might never reach a positive K.
- **Array with Zeros:** Zeros increase length but don't change sum (Prefix sum handles this by not updating map).
- **No solution:** Should return 0.

---

## Mistakes

- **User mistake:** No specific note provided.
- Updating the HashMap with the latest index of a prefix sum (this minimizes the length; you must only store the *first* index).
- Using Two Pointers when the array contains negative numbers.
- Forgetting to initialize the HashMap with `{0: -1}`.

---

## Complexity

- **Prefix Sum:**
  - Time: $O(N)$ → Single pass through the array.
  - Space: $O(N)$ → To store prefix sums in HashMap.
- **Two Pointers:**
  - Time: $O(N)$ → Each pointer moves at most $N$ times.
  - Space: $O(1)$ → Only a few variables used.

---

## Similar Problems

- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium
- [Binary Subarrays With Sum](https://leetcode.com/problems/binary-subarrays-with-sum/) - Medium
- [Maximum Size Subarray Sum Equals k](https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/) - Medium
- [Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #slidingwindow #prefixsum
- [[Sliding Window]] [[Prefix Sum]] [[HashMap]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [GeeksforGeeks - Longest Subarray with Sum K](https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
