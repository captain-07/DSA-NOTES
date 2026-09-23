---
created: 2026-09-22
revisions:
  - 2026-09-24
  - 2026-09-29
  - 2026-10-07
  - 2026-10-22
---

# Maximum Meetings In One Room

---

## Metadata & Placement Tags

- **Folder:** Greedy
- **Target Companies:** #Amazon #Microsoft #Flipkart #Atlassian
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #greedy [[Greedy]], #sorting [[Sorting]], #customcomparator [[Custom Comparator]]

## Pattern

Greedy (Interval Scheduling / Activity Selection) + Sorting

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

To maximize the total number of non-overlapping meetings, **always choose the meeting that ends earliest**. Finishing early leaves the maximum possible time remaining for subsequent meetings.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort meetings by **finish time** (and by original index as tie-breaker for lexicographical order), then greedily select non-overlapping ones.

---

## Approach

### Brute Force
- Generate all possible subsets of meetings, check if they overlap, and find the largest valid subset.
- Time Complexity: O(2^N * N)

### Optimal
1. Store meeting start time, end time, and original 1-based index as a tuple/structure.
2. Sort the list primarily by end time ascending. If end times are equal, sort by original index ascending.
3. Keep track of the end time of the last selected meeting.
4. Iterate through the sorted meetings; if a meeting's start time is strictly greater than the last selected meeting's end time, select it.
5. Sort the selected meeting indices to return them in increasing order.

---

## Code (Python)

```python
class Solution:
    def maxMeetings(self, number_of_meetings: int, start_times: list[int], end_times: list[int]) -> list[int]:
        # Step 1: Combine start time, end time, and 1-based index
        meetings = []
        for index in range(number_of_meetings):
            meetings.append((start_times[index], end_times[index], index + 1))

        # Step 2: Sort by finish time ascending; tie-break by original index
        meetings.sort(key=lambda meeting: (meeting[1], meeting[2]))

        selected_meeting_indices = []
        last_end_time = -1

        # Step 3: Greedily pick non-overlapping meetings
        for start, end, original_index in meetings:
            if start > last_end_time:
                selected_meeting_indices.append(original_index)
                last_end_time = end

        # Step 4: Sort indices to return them in increasing order as per problem requirement
        selected_meeting_indices.sort()
        return selected_meeting_indices
```

---

## Dry Run (Smart Example)

Input: `start_times = [1, 3, 0, 5, 8, 5]`, `end_times = [2, 4, 6, 7, 9, 9]`
Meetings after sorting by end time: `[(1,2,1), (3,4,2), (0,6,3), (5,7,4), (8,9,5), (5,9,6)]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `start=1, end=2, idx=1`, `last_end=-1` | `1 > -1` -> Select meeting 1. `last_end` becomes 2. Selected: `[1]` |
| 2 | `start=3, end=4, idx=2`, `last_end=2` | `3 > 2` -> Select meeting 2. `last_end` becomes 4. Selected: `[1, 2]` |
| 3 | `start=0, end=6, idx=3`, `last_end=4` | `0 <= 4` -> Skip meeting 3 (overlaps). |
| 4 | `start=5, end=7, idx=4`, `last_end=4` | `5 > 4` -> Select meeting 4. `last_end` becomes 7. Selected: `[1, 2, 4]` |
| 5 | `start=8, end=9, idx=5`, `last_end=7` | `8 > 7` -> Select meeting 5. `last_end` becomes 9. Selected: `[1, 2, 4, 5]` |

Result: `[1, 2, 4, 5]`

---

## Edge Cases

- **Meetings share end and start boundaries (e.g., [1, 2] and [2, 3]):** Problem specifies strictly `start > last_end` for non-overlapping, so ignore or pick accordingly based on problem constraints.
- **Single meeting:** Returns `[1]` directly.
- **Multiple meetings with identical start and end times:** Custom sort by index ensures consistent lexicographical order selection.
- **All meetings overlap:** Picks only 1 meeting (the one ending earliest).

---

## Mistakes

- Sorting by start time instead of end time (fails because a long meeting starting early blocks many short ones).
- Forgetting to track original 1-based indices before sorting.
- Failing to sort the final list of selected meeting indices.
- **`class Solution:`** Writing solution without maintaining `class Solution:` wrapper or nesting inner helper methods instead of using proper class methods.

---

## Complexity

Time: O(N log N) → Sorting N meetings takes O(N log N) time, iterating through takes O(N).
Space: O(N) → Storing meeting objects and result array requires O(N) space.

---

## Similar Problems

- [N Meetings In One Room](https://www.geeksforgeeks.org/problems/n-meetings-in-one-room-1587115620/1) - Easy
- [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) - Medium
- [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/) - Medium
- [Meeting Rooms](https://leetcode.com/problems/meeting-rooms/) - Easy

---

## Tags and Properties

- #dsa #important #revisit #greedy #interval-scheduling
- Concept Links: [[Greedy]], [[Sorting]], [[Intervals]]
- **Revision Date:** 2026-09-22
- **Problem Link:** [Maximum Meetings In One Room - GeeksforGeeks](https://www.geeksforgeeks.org/problems/maximum-meetings-in-one-room/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-24)
- [ ] Day 7 Revision (2026-09-29)
- [ ] Day 15 Revision (2026-10-07)
- [ ] Day 30 Revision (2026-10-22)
