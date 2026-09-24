---
created: 2026-09-24
revisions:
  - 2026-09-26
  - 2026-10-01
  - 2026-10-09
  - 2026-10-24
---

# Merge Intervals

---

## Metadata & Placement Tags

- **Folder:** Sorting
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Apple #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #sorting [[Sorting]], #intervals [[Intervals]], #greedy [[Greedy]]

## Pattern

Sorting + Greedy Sweep

---

## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

- Sorting intervals by their start time aligns potential overlaps sequentially.
- If `current_interval.start <= previous_interval.end`, they overlap and can be merged by updating the previous interval's end to `max(previous.end, current.end)`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Sort by start time. Iterate through intervals and compare current start with last merged end; merge if overlapping, else append.

---

## Approach

### Brute Force
- Compare every interval with every other interval to check for overlaps and merge recursively/repeatedly until no overlaps remain.
- Time Complexity: $O(N^2)$ or $O(N^3)$

### Optimal
1. Sort the intervals list based on the starting value of each interval.
2. Initialize an empty list `merged_intervals` to hold the result.
3. Iterate through each interval:
   - If `merged_intervals` is empty or the current interval does not overlap with the last interval in `merged_intervals`, append it.
   - If it overlaps, update the end time of the last interval in `merged_intervals` to `max(last_interval.end, current_interval.end)`.

---

## Code (Python)

```python
class Solution:
    def merge(self, intervals: list[list[int]]) -> list[list[int]]:
        # Handle edge case for empty or single element input
        if len(intervals) <= 1:
            return intervals

        # Step 1: Sort intervals by their starting times
        intervals.sort(key=lambda interval: interval[0])

        merged_intervals = []

        # Step 2: Iterate through intervals and merge overlapping ones
        for current_interval in intervals:
            # If merged_intervals is empty or no overlap exists
            if not merged_intervals or merged_intervals[-1][1] < current_interval[0]:
                merged_intervals.append(current_interval)
            else:
                # Overlap detected: merge by expanding the end boundary
                merged_intervals[-1][1] = max(merged_intervals[-1][1], current_interval[1])

        return merged_intervals
```

---

## Dry Run (Smart Example)

Input: `intervals = [[1, 3], [2, 6], [8, 10], [15, 18], [9, 11]]`
After Sorting: `[[1, 3], [2, 6], [8, 10], [9, 11], [15, 18]]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `current = [1, 3]`, `merged = []` | `merged` is empty $\rightarrow$ Append `[1, 3]`. `merged = [[1, 3]]` |
| 2 | `current = [2, 6]`, `last = [1, 3]` | Overlap ($2 \le 3$) $\rightarrow$ Update end: $\max(3, 6) = 6$. `merged = [[1, 6]]` |
| 3 | `current = [8, 10]`, `last = [1, 6]` | No overlap ($8 > 6$) $\rightarrow$ Append `[8, 10]`. `merged = [[1, 6], [8, 10]]` |
| 4 | `current = [9, 11]`, `last = [8, 10]` | Overlap ($9 \le 10$) $\rightarrow$ Update end: $\max(10, 11) = 11$. `merged = [[1, 6], [8, 11]]` |
| 5 | `current = [15, 18]`, `last = [8, 11]` | No overlap ($15 > 11$) $\rightarrow$ Append `[15, 18]`. `merged = [[1, 6], [8, 11], [15, 18]]` |

---

## Edge Cases

- **Single interval:** Input like `[[1, 4]]` returns `[[1, 4]]`.
- **Already non-overlapping:** Input like `[[1, 2], [3, 4]]` remains unchanged.
- **Fully covered intervals:** Input like `[[1, 10], [2, 3]]` merges into `[[1, 10]]`.
- **Same endpoints:** Input like `[[1, 4], [4, 5]]` merges into `[[1, 5]]`.

---

## Mistakes

- User mistake: No specific note provided.
- Forgetting to sort intervals prior to the single-pass sweep.
- Comparing start times instead of checking if `current_start <= last_end`.
- Updating the end time to `current.end` directly without taking `max(last_end, current.end)`.

---

## Complexity

Time: $O(N \log N)$ → Dominated by the sorting step where $N$ is the number of intervals.
Space: $O(N)$ → Required for output storage or sorting algorithms implementation details.

---

## Similar Problems

- [Insert Interval](https://leetcode.com/problems/insert-interval/) - Medium
- [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) - Medium
- [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) - Medium
- [Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #intervals #sorting #greedy
- Concepts: [[Sorting]], [[Intervals]], [[Greedy]]
- Revision Date: 2026-09-24
- **Problem Link:** [Merge Intervals - LeetCode](https://leetcode.com/problems/merge-intervals/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-26)
- [ ] Day 7 Revision (2026-10-01)
- [ ] Day 15 Revision (2026-10-09)
- [ ] Day 30 Revision (2026-10-24)
