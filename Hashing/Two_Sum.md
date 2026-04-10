---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Two Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe #Apple #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]], #array [[Array]], #searching [[Searching]]

## Pattern

HashMap (Complement Lookup)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Instead of searching for a pair, iterate once and store the **complement** (`target - current_val`) in a HashMap. If the current value already exists in the map as a complement, the pair is found.

---

## ⚡ Quick Recall (VERY IMPORTANT)

One-pass HashMap: `seen[value] = index`. Check `target - num` in `seen` before adding `num`.

---

## Approach

### Brute Force
- Nested loops checking every possible pair $(i, j)$.
- Time: $O(n^2)$, Space: $O(1)$.

### Better
- Sort the array and use Two Pointers.
- Mention: Requires $O(n \log n)$ time and loses original indices unless tracked.

### Optimal
- **One-pass HashMap**: Traverse the array once. For each element, check if its complement exists in the map.
- If yes, return indices. If no, store current value and index.
- Time: $O(n)$, Space: $O(n)$.

---

## Code (Python)

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        # Hash map to store: value -> index
        prev_map = {} 
        
        for i, n in enumerate(nums):
            diff = target - n
            # If complement exists, we found the pair
            if diff in prev_map:
                return [prev_map[diff], i]
            
            # Store current number and its index
            prev_map[n] = i
        return []
```

---

## Dry Run (Smart Example)

**Input:** `nums = [3, 4, 3, 6]`, `target = 6`

| Step | Current (n, i) | Diff (6 - n) | `prev_map` State | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | (3, 0) | 3 | `{3: 0}` | 3 not in map. Add 3. |
| 2 | (4, 1) | 2 | `{3: 0, 4: 1}` | 2 not in map. Add 4. |
| 3 | (3, 2) | 3 | **Found!** | 3 exists in map at index 0. Return [0, 2]. |

---

## Edge Cases

- **Duplicates:** Handled by HashMap (as seen in dry run).
- **Negative Numbers:** `nums = [-3, 4, 1], target = 1` → returns `[0, 1]`.
- **Target is double an element:** `[3, 2, 4], target = 6` → Must not use `3` twice.
- **Minimum Array Size:** Array always has at least 2 elements per constraints.

---

## Mistakes

- **Same Element Twice:** Using the same index twice (e.g., if `target = 6` and `nums[i] = 3`, returning `[i, i]`). Avoided by checking map *before* adding the current element.
- **Sorting First:** Sorting loses original indices unless storing `(value, index)` pairs, adding unnecessary $O(n \log n)$ overhead.
- **Two-Pass HashMap:** Building the full map first, then iterating. This risks using the same element twice unless specifically checked (`if map[diff] != i`).

---

## Complexity

Time: $O(n)$ → Single traversal of the array; HashMap lookups are $O(1)$ on average.  
Space: $O(n)$ → In the worst case, we store $n-1$ elements in the HashMap.

---

## Similar Problems

- [3Sum](https://leetcode.com/problems/3sum/) - Medium
- [4Sum](https://leetcode.com/problems/4sum/) - Medium
- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Medium
- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #blind75 #leetcode1
- #hashmap [[HashMap]] #arrays [[Arrays]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [Two Sum - LeetCode](https://leetcode.com/problems/two-sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
