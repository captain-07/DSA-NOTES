---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Largest Element

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #TCS #Infosys #Accenture #Microsoft #Google

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #array [[Array]]
  - #linearsearch [[Linear Search]]

## Pattern

Single Pass (Linear Scan)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

- Maintain a tracker variable (`max_val`) initialized to the first element.
- Iterate through the array once: if the current element is greater than `max_val`, update the tracker.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Scan once, compare all, keep the global winner.

---

## Approach

### Brute Force
- Sort the array in ascending order and return the last element.
- Time: $O(N \log N)$ | Space: $O(1)$

### Optimal
- Use a single loop to compare each element with the current maximum.
- Time: $O(N)$ | Space: $O(1)$

---

## Code (Python)

```python
class Solution:
    def findLargest(self, arr: list[int]) -> int:
        # Initialize max_val with the first element
        max_val = arr[0]
        
        # Iterate through the array starting from the second element
        for i in range(1, len(arr)):
            if arr[i] > max_val:
                max_val = arr[i]
                
        return max_val
```

---

## Dry Run (Smart Example)

**Input:** `arr = [3, 10, -2, 10, 5]`

| Step | Current Element | Comparison (`arr[i] > max_val`) | `max_val` State | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| Init | - | - | 3 | Initialized with `arr[0]` |
| 1 | 10 | 10 > 3 (True) | 10 | Found larger value |
| 2 | -2 | -2 > 10 (False) | 10 | Ignore smaller value |
| 3 | 10 | 10 > 10 (False) | 10 | Ignore duplicate |
| 4 | 5 | 5 > 10 (False) | 10 | Final iteration |

---

## Edge Cases

- **Single Element:** `[5]` -> Returns 5 correctly.
- **All Identical:** `[2, 2, 2]` -> Returns 2.
- **Strictly Decreasing:** `[5, 4, 3]` -> Returns first element (5).
- **All Negatives:** `[-10, -20, -5]` -> Returns -5 (Properly handled by initializing with `arr[0]`).

---

## Mistakes

- **Initializing to 0:** This fails if all elements in the array are negative. Always initialize with `arr[0]` or `-float('inf')`.
- **Using Built-ins in Interviews:** While `max(arr)` works in Python, interviewers want to see the iterative logic first.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Must visit every element at least once to ensure it's not the largest.  
Space: O(1) → Only one variable used for tracking regardless of input size.

---

## Similar Problems

- [Second Largest Element](https://www.geeksforgeeks.org/problems/second-largest3735/1) - Easy
- [Find Smallest Element](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium (Variation)
- [Find Peak Element](https://leetcode.com/problems/find-peak-element/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #arrays #searching #fundamentals
  - [[Array]] [[Linear Search]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [Largest Element in Array](https://www.geeksforgeeks.org/problems/largest-element-in-array1510/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
