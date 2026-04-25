---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Longest Consecutive Sequence In An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Salesforce #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashset [[HashSet]]
  - #array [[Array]]
  - #sorting [[Sorting]]

---
## Pattern

Hash Set + Start-of-Sequence Logic  
Sorting + Linear Scan  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The bottleneck is finding if a consecutive number exists. A **HashSet** provides $O(1)$ lookups. To ensure $O(n)$ time, only start counting a sequence if the current number is the **actual start** (i.e., `num - 1` does not exist in the set).

---

## ⚡ Quick Recall (VERY IMPORTANT)

"Is `x - 1` in the set? No? Then `x` is a start. Count `x + 1`, `x + 2`... from the set."

---

## Approach

### Brute Force
- For every number $x$, perform a linear search for $x+1, x+2...$ until the sequence breaks.
- Time: $O(N^3)$ (Two nested loops + linear search).

### Better
- Sort the array first. Iterate once and count consecutive elements, handling duplicates by skipping them.
- Time: $O(N \log N)$ | Space: $O(1)$ or $O(N)$ depending on sort.

### Optimal
1. Insert all elements into a **HashSet**.
2. Iterate through the array/set.
3. For each `num`, check if `num - 1` exists in the set.
4. If **no**, it is the start of a sequence. Start a loop to find `num + 1`, `num + 2`... incrementing count.
5. Update `max_length` accordingly.

---

## Code (Python)

```python
class Solution:
    def longestConsecutive(self, nums: list[int]) -> int:
        if not nums:
            return 0
        
        num_set = set(nums)
        longest_streak = 0
        
        for num in num_set:
            # Check if num is the start of a sequence
            if (num - 1) not in num_set:
                current_num = num
                current_streak = 1
                
                # Expand the sequence
                while (current_num + 1) in num_set:
                    current_num += 1
                    current_streak += 1
                
                longest_streak = max(longest_streak, current_streak)
                
        return longest_streak
```

---

## Dry Run (Smart Example)

**Input:** `[100, 4, 200, 1, 3, 2]`  
**Set:** `{1, 2, 3, 4, 100, 200}`

| Step | Num | `num - 1` in Set? | Action | Streak | Max Streak |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 100 | No | Start counting (100) | 1 | 1 |
| 2 | 4 | Yes | Skip (part of sequence) | - | 1 |
| 3 | 200 | No | Start counting (200) | 1 | 1 |
| 4 | 1 | No | Start counting (1,2,3,4) | 4 | 4 |
| 5 | 3 | Yes | Skip | - | 4 |
| 6 | 2 | Yes | Skip | - | 4 |

---

## Edge Cases

- **Empty Array:** `[]` → Return 0.
- **Single Element:** `[10]` → Return 1.
- **Identical Elements:** `[1, 1, 1]` → Set handles duplicates, Return 1.
- **Negative Numbers:** `[-2, -1, 0, 1]` → Logic remains identical, Return 4.
- **No Sequence:** `[1, 10, 100]` → Return 1.

---

## Mistakes

- **O(N²) Trap:** Forgetting to check `(num - 1)` before starting the `while` loop, leading to redundant checks.
- **Handling Duplicates:** Not using a set or not skipping duplicates in the sorting approach.
- **User Mistake:** No specific note provided.

---

## Complexity

**Time:** $O(N)$  
Each number is visited at most twice: once in the main loop and once inside the `while` loop across the entire execution.

**Space:** $O(N)$  
To store all unique elements in the HashSet.

---

## Similar Problems

- [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) - Hard
- [Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/) - Easy
- [Missing Number](https://leetcode.com/problems/missing-number/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #hashset #sequences
  - [[HashSet]] [[Array]] [[Interview_Favorite]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode 128 - Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
