---
created: 2026-04-03
revisions:
  - 2026-04-05
  - 2026-04-10
  - 2026-04-18
  - 2026-05-03
---

# Single Element In A Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Flipkart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #bitmanipulation [[Bit Manipulation]]

## Pattern
Binary Search on Index Parity (Even-Odd logic)

---
## Difficulty
Medium #medium

---

## ⚡ Key Idea (Core Insight)
In a sorted array where every element appears twice except one:
1. **Before the single element:** Pairs follow the pattern `(even index, odd index)`.
2. **After the single element:** Pairs follow the pattern `(odd index, even index)`.
3. Binary search identifies the point where this pattern breaks.

---

## ⚡ Quick Recall (VERY IMPORTANT)
Check `nums[mid]` against `nums[mid ^ 1]`. If they are equal, the single element is on the **right** (`low = mid + 1`); otherwise, it is on the **left** or is the **mid** itself.

---

## Approach

### Brute Force
- Iterate through the array and XOR all elements. The result is the single element.
- **Time:** O(N)

### Better (Linear Search)
- Compare adjacent elements `nums[i]` and `nums[i+1]` with a step of 2.
- **Time:** O(N)

### Optimal (Binary Search)
1. Initialize `low = 0`, `high = len(nums) - 1`.
2. While `low < high`:
   - Calculate `mid`.
   - Use the **XOR index trick**: `mid ^ 1`.
     - If `mid` is even, `mid ^ 1` is `mid + 1`.
     - If `mid` is odd, `mid ^ 1` is `mid - 1`.
   - If `nums[mid] == nums[mid ^ 1]`, we are in the left half; move `low = mid + 1`.
   - Else, we are in the right half (or at the answer); move `high = mid`.
3. Return `nums[low]`.

---

## Code (Python)

```python
def singleNonDuplicate(nums: list[int]) -> int:
    low, high = 0, len(nums) - 1
    
    while low < high:
        mid = low + (high - low) // 2
        
        # The XOR trick (mid ^ 1) elegantly handles:
        # If mid is even, checks mid + 1
        # If mid is odd, checks mid - 1
        if nums[mid] == nums[mid ^ 1]:
            # Pattern is intact; single element is further right
            low = mid + 1
        else:
            # Pattern broken; single element is at mid or to the left
            high = mid
            
    return nums[low]
```

---

## Dry Run (Smart Example)
Input: `nums = [1, 1, 2, 3, 3, 4, 4]`

| Step | low | high | mid | nums[mid] | nums[mid ^ 1] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 3 | nums[2] = 2 | 3 != 2. Pattern broken. `high = 3`. |
| 2 | 0 | 3 | 1 | 1 | nums[0] = 1 | 1 == 1. Pattern intact. `low = 2`. |
| 3 | 2 | 3 | 2 | 2 | nums[3] = 3 | 2 != 3. Pattern broken. `high = 2`. |
| 4 | 2 | 2 | - | - | - | `low == high`. Return `nums[2] = 2`. |

---

## Edge Cases
- **Single element array:** `[1]` → `low` and `high` start equal, loop skips, returns `nums[0]`.
- **Single element at start:** `[1, 2, 2, 3, 3]` → Binary search correctly shifts `high` left.
- **Single element at end:** `[1, 1, 2, 2, 3]` → Binary search correctly shifts `low` right.

---

## Mistakes
- **Using XOR only:** While simple, it takes O(N). If the array is **sorted**, the interviewer expects O(log N).
- **Boundary checks:** Using `high = len(nums)` instead of `len(nums) - 1` can cause out-of-bounds if not careful.
- **Index logic:** Overcomplicating the `even/odd` check instead of using the `mid ^ 1` trick.

---

## Complexity
- **Time:** O(log N) → Standard binary search halving the search space.
- **Space:** O(1) → Only constant extra space for pointers.

---

## Tags and Properties
- #dsa #important #revisit #binarysearch 
- [[Binary Search]] [[Array]]
- Revision Date: 2026-04-03
- Related: [[Find Minimum in Rotated Sorted Array]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-05)
- [ ] Day 7 Revision (2026-04-10)
- [ ] Day 15 Revision (2026-04-18)
- [ ] Day 30 Revision (2026-05-03)
