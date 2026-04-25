---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Leaders In An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #GoldmanSachs #Google

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #array [[Array]]
  - #greedy [[Greedy]]
  - #suffix-max [[Suffix Maximum]]

## Pattern

Right-to-Left Scan (Suffix Maximum)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The rightmost element is always a leader. By scanning the array from **right to left**, we can maintain a "running maximum." Any element greater than this current maximum is a leader and becomes the new maximum.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Scan backwards, track `max_from_right`, and collect elements that break the record.

---

## Approach

### Brute Force
- Use nested loops: for each element, check every element to its right. If no element is greater, it's a leader.
- **Time:** O(N²)
- **Space:** O(1)

### Optimal
- Initialize `max_so_far` with the last element.
- Traverse from `n-2` down to `0`.
- If `arr[i] >= max_so_far`, add to results and update `max_so_far`.
- Reverse the result list at the end to maintain original relative order.
- **Time:** O(N)
- **Space:** O(1) (excluding output array)

---

## Code (Python)

```python
class Solution:
    def leaders(self, arr):
        """
        Finds all leaders in the array.
        An element is a leader if it is greater than or equal to 
        all elements to its right.
        """
        n = len(arr)
        if n == 0:
            return []
            
        leaders_list = []
        # Rightmost element is always a leader
        max_from_right = arr[n-1]
        leaders_list.append(max_from_right)
        
        # Scan from right to left
        for i in range(n-2, -1, -1):
            if arr[i] >= max_from_right:
                max_from_right = arr[i]
                leaders_list.append(max_from_right)
        
        # Reverse to restore original order (left to right)
        return leaders_list[::-1]
```

---

## Dry Run (Smart Example)

**Input:** `[16, 17, 4, 3, 5, 2]`

| Step | Index | Value | max_from_right | Action | Result List |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 5 | 2 | 2 | Init (Last element) | `[2]` |
| 2 | 4 | 5 | 5 | 5 > 2 (Update Max) | `[2, 5]` |
| 3 | 3 | 3 | 5 | 3 < 5 (Ignore) | `[2, 5]` |
| 4 | 2 | 4 | 5 | 4 < 5 (Ignore) | `[2, 5]` |
| 5 | 1 | 17 | 17 | 17 > 5 (Update Max) | `[2, 5, 17]` |
| 6 | 0 | 16 | 17 | 16 < 17 (Ignore) | `[2, 5, 17]` |

**Final Reverse:** `[17, 5, 2]`

---

## Edge Cases

- **Single Element:** `[10]` → Result `[10]` (always a leader).
- **Sorted Ascending:** `[1, 2, 3, 4]` → Only the last element `[4]` is a leader.
- **Sorted Descending:** `[4, 3, 2, 1]` → All elements are leaders `[4, 3, 2, 1]`.
- **All Elements Same:** `[5, 5, 5]` → All elements are leaders (since $arr[i] \ge$ right).

---

## Mistakes

- Scanning from left to right (results in O(N²) unless using a stack).
- Forgetting to reverse the final list (if left-to-right order is required).
- Not handling the "equal to" case correctly (check problem constraints on "strictly greater" vs "greater or equal").
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** O(N) → Single pass from right to left + O(N) reversal.
- **Space:** O(1) → No extra space used other than the list required to return the answer.

---

## Similar Problems

- [Replace Elements with Greatest Element on Right Side](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/) - Easy
- [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) - Hard (Uses suffix/prefix max concept)
- [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) - Medium (Monotonic Stack variation)

---

## Tags and Properties
- #dsa #important #revisit
- #array [[Array]] #suffix-max [[Suffix Maximum]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [GeeksforGeeks: Leaders in an array](https://www.geeksforgeeks.org/problems/leaders-in-an-array-1587115620/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
