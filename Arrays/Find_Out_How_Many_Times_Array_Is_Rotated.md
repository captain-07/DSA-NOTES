---
created: 2026-04-03
revisions:
  - 2026-04-05
  - 2026-04-10
  - 2026-04-18
  - 2026-05-03
---

# Find Out How Many Times Array Is Rotated

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #TCS #Walmart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #searching [[Searching]]

---
## Pattern

Modified Binary Search (Find Minimum in Rotated Sorted Array)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The number of rotations in a sorted array is exactly equal to the **index of the minimum element**. Since the array was originally sorted, finding the "pivot" (the point where the property $arr[i] > arr[i+1]$ first occurs) reveals how many positions the elements shifted.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the **index of the minimum element** using Binary Search. If `arr[mid] > arr[high]`, the minimum must be in the right half; otherwise, it is in the left half (including `mid`).

---

## Approach

### Brute Force
- Iterate through the array to find the minimum element's index.
- **Time Complexity:** $O(N)$

### Optimal
- Use **Binary Search**.
- Compare `arr[mid]` with `arr[high]`.
- If `arr[mid] > arr[high]`, the right part is unsorted, so the minimum (pivot) lies in the range `[mid + 1, high]`.
- If `arr[mid] <= arr[high]`, the right part is sorted, so the minimum lies in the range `[low, mid]`.
- **Time Complexity:** $O(\log N)$

---

## Code (Python)

```python
def find_rotations(nums):
    low = 0
    high = len(nums) - 1
    
    # If the array is not rotated at all
    if nums[low] <= nums[high]:
        return 0
        
    while low < high:
        mid = low + (high - low) // 2
        
        # Core Logic: Compare mid with high
        if nums[mid] > nums[high]:
            # Minimum must be in the right unsorted half
            low = mid + 1
        else:
            # Minimum is in the left half (including mid)
            high = mid
            
    # 'low' or 'high' will point to the minimum element
    return low
```

---

## Dry Run (Smart Example)

**Input:** `nums = [4, 5, 6, 7, 0, 1, 2]`

| Step | low | high | mid | nums[mid] vs nums[high] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | `7 > 2` | `nums[mid] > nums[high]`: Min is on the right. Set `low = mid + 1` (4). |
| 2 | 4 | 6 | 5 | `1 < 2` | `nums[mid] < nums[high]`: Min is on the left. Set `high = mid` (5). |
| 3 | 4 | 5 | 4 | `0 < 1` | `nums[mid] < nums[high]`: Min is at/left of mid. Set `high = mid` (4). |
| 4 | 4 | 4 | - | `low == high` | Loop terminates. Result is index 4. |

---

## Edge Cases

- **No rotation:** `[1, 2, 3]` returns `0`.
- **Single element:** `[1]` returns `0`.
- **Rotation by $N-1$:** `[2, 3, 1]` returns `2`.
- **Duplicates:** Standard binary search fails; requires $O(N)$ worst case (not covered in this specific distinct-integer logic).

---

## Mistakes

- **Mid vs High Logic:** Users often compare `mid` with `low`. This is risky because if the array is already sorted, `mid > low` suggests the right half is sorted, but it doesn't help isolate the "pivot" as effectively as comparing with `high`.
- **Returning the Value:** Forgetting that the question asks for the **count** (index), not the minimum value itself.
- **Infinite Loop:** Using `low <= high` with `high = mid` can lead to an infinite loop; use `low < high`.

---

## Complexity

- **Time:** $O(\log N)$ → Each step halves the search space.
- **Space:** $O(1)$ → Only uses a few pointer variables.

---

## Tags and Properties
- #dsa #important #revisit #binarysearch 
- [[Binary Search]] [[Searching Algorithms]]
- Revision Date: 2026-04-03
- Related: [[Find Minimum in Rotated Sorted Array]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-05)
- [ ] Day 7 Revision (2026-04-10)
- [ ] Day 15 Revision (2026-04-18)
- [ ] Day 30 Revision (2026-05-03)
