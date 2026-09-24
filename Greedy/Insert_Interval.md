---
created: 2026-09-24
revisions:
  - 2026-09-26
  - 2026-10-01
  - 2026-10-09
  - 2026-10-24
---

# Insert Interval

---

## Metadata & Placement Tags

- **Folder:** Arrays
- **Target Companies:** #Google #Amazon #Microsoft #Meta #Apple #LinkedIn
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #arrays [[Arrays]], #intervals [[Intervals]], #sorting [[Sorting]]

## Pattern

Intervals + Iterative Merging

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The existing intervals are already sorted and non-overlapping. Process intervals sequentially into three phases: add non-overlapping intervals before the new interval, merge all overlapping intervals into one combined new interval, and append remaining non-overlapping intervals after it.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Three linear loops/phases: Left (ends before `newInterval` starts), Merge (overlaps with `newInterval`), Right (starts after `newInterval` ends).

---

## Approach

### Brute Force
- Append `newInterval` to `intervals`, sort the array by start times, then perform standard Interval Merge.
- Time: O(N log N) | Space: O(N)

### Optimal
- Process intervals in a single linear scan:
  1. Add intervals ending before `newInterval.start` directly to result.
  2. While intervals start before/at `newInterval.end`, expand `newInterval` boundaries (`min(start)`, `max(end)`).
  3. Add expanded `newInterval`, then append all remaining intervals.
- Time: O(N) | Space: O(N) for output array.

---

## Code (Python)

```python
class Solution:
    def insert(self, intervals: list[list[int]], newInterval: list[int]) -> list[list[int]]:
        result = []
        index = 0
        total_intervals = len(intervals)

        # Phase 1: Add all intervals that end before newInterval starts
        while index < total_intervals and intervals[index][1] < newInterval[0]:
            result.append(intervals[index])
            index += 1

        # Phase 2: Merge all overlapping intervals with newInterval
        while index < total_intervals and intervals[index][0] <= newInterval[1]:
            newInterval[0] = min(newInterval[0], intervals[index][0])
            newInterval[1] = max(newInterval[1], intervals[index][1])
            index += 1

        # Add the merged newInterval
        result.append(newInterval)

        # Phase 3: Add all remaining intervals after newInterval
        while index < total_intervals:
            result.append(intervals[index])
            index += 1

        return result
```

---

## Dry Run (Smart Example)

Input: `intervals = [[1, 2], [3, 5], [6, 7], [8, 10], [12, 16]]`, `newInterval = [4, 8]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `index = 0`, `[1, 2]` | `2 < 4` (ends before `newInterval`), add `[1, 2]`. `result = [[1, 2]]`. |
| 2 | `index = 1`, `[3, 5]` | `3 <= 8` (overlaps), merge: `newInterval` becomes `[min(4,3), max(8,5)] = [3, 8]`. |
| 3 | `index = 2`, `[6, 7]` | `6 <= 8` (overlaps), merge: `newInterval` becomes `[min(3,6), max(8,7)] = [3, 8]`. |
| 4 | `index = 3`, `[8, 10]` | `8 <= 8` (overlaps), merge: `newInterval` becomes `[min(3,8), max(8,10)] = [3, 10]`. |
| 5 | `index = 4`, `[12, 16]` | `12 > 10` (no overlap), loop ends. Add `[3, 10]`. Append remaining `[12, 16]`. |

Output: `[[1, 2], [3, 10], [12, 16]]`

---

## Edge Cases

- **Empty intervals array:** Returns `[newInterval]`.
- **New interval inserted at start/end without overlapping:** Inserted cleanly without modifying existing bounds.
- **New interval completely spans across all existing intervals:** Merges everything into single range `[min_start, max_end]`.
- **New interval fully contained inside an existing interval:** Existing interval absorbs `newInterval`.

---

## Mistakes

- No specific note provided.
- Forgetting that overlap check is `intervals[i][0] <= newInterval[1]` (using `<` instead of `<=`).
- Mutating original array in-place inefficiently via array slicing instead of building result linearly.

---

## Complexity

Time: O(N) → Single pass through the list of `N` intervals.
Space: O(N) → Result list stores `N + 1` intervals in the worst case.

---

## Similar Problems

- [Merge Intervals](https://leetcode.com/problems/merge-intervals/) - Medium
- [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) - Medium
- [Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #intervals #arrays
- Obsidian Links: [[Intervals]], [[Arrays]], [[Sorting]]
- **Last Revised:** 2026-09-24
- **Problem Link:** [Insert Interval - LeetCode](https://leetcode.com/problems/insert-interval/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-26)
- [ ] Day 7 Revision (2026-10-01)
- [ ] Day 15 Revision (2026-10-09)
- [ ] Day 30 Revision (2026-10-24)
