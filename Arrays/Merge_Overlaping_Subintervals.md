---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Merge Overlapping Subintervals

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Facebook #Uber #Salesforce

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #intervals [[Intervals]]
  - #sorting [[Sorting]]
  - #greedy [[Greedy Algorithms]]

---
## Pattern

Sorting + Greedy (Interval Linear Scan)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The bottleneck is the unsorted order. Once intervals are **sorted by their start times**, overlapping intervals become contiguous. You only need to compare the `start` of the current interval with the `end` of the last merged interval.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort by start. If `current_start <= last_merged_end`, update `last_merged_end` to `max(last_merged_end, current_end)`. Otherwise, push a new interval.

---

## Approach

### Brute Force
- Compare every interval with every other interval to check for overlaps. If they overlap, merge and restart or track visited.
- **Time:** $O(N^2)$

### Optimal
1. **Sort** all intervals based on the start time: $O(N \log N)$.
2. **Initialize** an empty `merged` list.
3. **Iterate** through sorted intervals:
   - If `merged` is empty OR `current.start > merged[-1].end`: No overlap, append current.
   - Else: Overlap exists, update `merged[-1].end = max(merged[-1].end, current.end)`.
- **Time:** $O(N \log N)$

---

## Code (Python)

```python
class Solution:
    def merge(self, intervals: list[list[int]]) -> list[list[int]]:
        # 1. Sort by start time
        intervals.sort(key=lambda x: x[0])
        
        merged = []
        for interval in intervals:
            # 2. If list is empty or no overlap, append
            if not merged or interval[0] > merged[-1][1]:
                merged.append(interval)
            else:
                # 3. Overlap exists: Merge by updating the end to max
                merged[-1][1] = max(merged[-1][1], interval[1])
                
        return merged
```

---

## Dry Run (Smart Example)

**Input:** `[[1,3], [8,10], [2,6], [15,18]]`  
**Sorted:** `[[1,3], [2,6], [8,10], [15,18]]`

| Step | Current | `merged` (State) | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `[1,3]` | `[[1,3]]` | List empty, push first interval. |
| 2 | `[2,6]` | `[[1,6]]` | `2 <= 3`. Overlap. Update `max(3, 6)`. |
| 3 | `[8,10]`| `[[1,6], [8,10]]` | `8 > 6`. No overlap. Push `[8,10]`. |
| 4 | `[15,18]`| `[[1,6], [8,10], [15,18]]` | `15 > 10`. No overlap. Push. |

---

## Edge Cases

- **Empty Input:** Handled by empty loop/check.
- **Single Interval:** Loop runs once, returns input.
- **Identical Intervals:** `[[1,2], [1,2]]` → `[1,2]`.
- **Fully Nested:** `[[1,10], [2,5]]` → `[1,10]`.
- **Touching Ends:** `[[1,2], [2,3]]` → `[1,3]` (Overlapping).

---

## Mistakes

- **Forgetting to Sort:** The logic fails entirely if intervals aren't ordered by start time.
- **Max vs. Current End:** Using `merged[-1][1] = interval[1]` instead of `max(..., interval[1])` fails for nested intervals.
- **Off-by-one:** Checking `>` instead of `>=` for overlap boundaries.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(N \log N)$ → Dominated by the sorting step.
- **Space:** $O(N)$ or $O(\log N)$ → Depending on the sort implementation's space and the output list.

---

## Similar Problems

- [Insert Interval](https://leetcode.com/problems/insert-interval/) - Medium
- [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) - Medium
- [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) - Medium
- [Employee Free Time](https://leetcode.com/problems/employee-free-time/) - Hard

---

## Tags and Properties
- #dsa #important #revisit #arrays #intervals
- [[Intervals]] [[Sorting]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode - Merge Intervals](https://leetcode.com/problems/merge-intervals/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
