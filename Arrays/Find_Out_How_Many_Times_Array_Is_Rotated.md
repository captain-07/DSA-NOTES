---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Find Out How Many Times Array Is Rotated

---

## Pattern

Binary Search (Pivot Finding)

---
## Difficulty

Easy/Medium  
#easy #medium

---

## ⚡ Key Idea (Core Insight)

The number of times a sorted array is rotated is exactly equal to the **index of the minimum element** in the array. In a rotated sorted array, the minimum element is the only element that "breaks" the increasing order (the pivot).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the index of the minimum element using Binary Search. If `arr[mid] > arr[high]`, the pivot/min is in the right half; otherwise, it is in the left half (including `mid`).

---

## Approach

### Brute Force
- Perform a linear search to find the minimum element in the array.
- Return the index of that minimum element.
- **Time Complexity:** O(N)

### Optimal
- Use Binary Search to locate the minimum element.
- Maintain `low` and `high` pointers. 
- While `low < high`:
    1. Calculate `mid`.
    2. If `arr[mid] > arr[high]`, it means the rotation point is to the right (set `low = mid + 1`).
    3. Otherwise, the rotation point is at `mid` or to the left (set `high = mid`).
- The index `low` (or `high`) will be the number of rotations.
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
class Solution:
    def findKRotation(self, arr: list[int]) -> int:
        low, high = 0, len(arr) - 1
        
        # Binary Search to find the index of the minimum element
        while low < high:
            # Standard optimization to avoid overflow
            mid = low + (high - low) // 2
            
            # If mid element is greater than the last element, 
            # the minimum must be in the right half
            if arr[mid] > arr[high]:
                low = mid + 1
            # Otherwise, the minimum is in the left half (including mid)
            else:
                high = mid
                
        # The index of the minimum element is the rotation count
        return low
```

---

## Dry Run (Smart Example)

Input: `arr = [4, 5, 6, 7, 0, 1, 2]`

| Step | low | high | mid | arr[mid] | arr[high] | Comparison | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 7 | 2 | 7 > 2 | `low = 4` |
| 2 | 4 | 6 | 5 | 1 | 2 | 1 < 2 | `high = 5` |
| 3 | 4 | 5 | 4 | 0 | 1 | 0 < 1 | `high = 4` |
| End | 4 | 4 | - | - | - | `low == high` | **Return 4** |

---

## Edge Cases

- **Already Sorted:** `[1, 2, 3, 4, 5]` → Index 0 (0 rotations).
- **Single Element:** `[1]` → Index 0.
- **Max Rotations (N-1):** `[2, 3, 4, 5, 1]` → Index 4.
- **Duplicates:** Standard binary search might fail; requires O(N) in worst case (e.g., `[1, 1, 0, 1, 1]`).

---

## Mistakes

- Returning the minimum **value** instead of the **index**.
- Not handling the condition `low < high` vs `low <= high` correctly, leading to infinite loops.
- **User Mistake:** No specific note provided. Ensure to track the "why" behind the rotation count logic.

---

## Complexity

Time: O(log N) → Reducing the search space by half in each step of the binary search.  
Space: O(1) → Only using a few pointers regardless of input size.

---

## Similar Problems

- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II (with duplicates)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard

---

## Tags and Properties
- #dsa #important #revisit #binarysearch #arrays
- [[Binary Search]] [[Pivot Element]] [[Rotated Sorted Array]]
- **Revision Date:** 2026-04-11
- **Problem Link:** [GeeksforGeeks - Rotation Count](https://www.geeksforgeeks.org/problems/rotation4523/1)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Flipkart #Adobe #Samsung #Google

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #searching [[Searching]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
