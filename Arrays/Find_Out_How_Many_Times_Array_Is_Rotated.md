---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Find Out How Many Times Array Is Rotated

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Adobe #Flipkart #Samsung

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #searching [[Searching]]

## Pattern

Binary Search on Sorted Rotated Array

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The number of times a sorted array is rotated is exactly equal to the **index of the minimum element** in that array. In a rotated sorted array, the minimum element is the only element that is smaller than its predecessor (the "pivot").

---

## ⚡ Quick Recall (VERY IMPORTANT)

Number of Rotations = **Index of Minimum Element**. Use Binary Search to find the pivot point where the sorted property breaks.

---

## Approach

### Brute Force
- Linearly traverse the array to find the minimum element. The index of this element is the answer.
- **Time Complexity:** O(N)

### Optimal
- Use **Binary Search**. In each step, determine which half of the array is sorted.
- If `nums[low] <= nums[high]`, the entire range is sorted; `nums[low]` is the minimum.
- Otherwise, if `nums[low] <= nums[mid]`, the left half is sorted. The minimum must be in the right half, but `nums[low]` is a candidate for the global minimum.
- If the right half is sorted, the minimum is in the left half (including `mid`).
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
class Solution:
    def findKRotation(self, nums: list[int]) -> int:
        low, high = 0, len(nums) - 1
        ans = float('inf')
        index = 0
        
        while low <= high:
            mid = (low + high) // 2
            
            # Optimization: If the current search space is already sorted
            if nums[low] <= nums[high]:
                if nums[low] < ans:
                    index = low
                    ans = nums[low]
                break
            
            # Identify which half is sorted
            if nums[low] <= nums[mid]:
                # Left half is sorted, nums[low] is the min of this half
                if nums[low] < ans:
                    ans = nums[low]
                    index = low
                # Minimum must be in the unsorted right half
                low = mid + 1
            else:
                # Right half is sorted, nums[mid] is the min of this half
                if nums[mid] < ans:
                    ans = nums[mid]
                    index = mid
                # Minimum must be in the unsorted left half
                high = mid - 1
                
        return index
```

---

## Dry Run (Smart Example)

Input: `nums = [4, 5, 6, 1, 2, 3]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `low=0, high=5, mid=2` | `nums[0]=4`, `nums[2]=6`. Left half `[4,5,6]` is sorted. `ans=4, index=0`. Set `low=3`. |
| 2 | `low=3, high=5, mid=4` | `nums[3]=1`, `nums[5]=3`. `nums[low] <= nums[high]` is True. `[1,2,3]` is sorted. |
| 3 | `ans=min(4, 1)=1` | `index=3`. Minimum found at index 3. |
| 4 | `Break` | Return `index = 3`. |

---

## Edge Cases

- **No Rotation:** `[1, 2, 3, 4, 5]` → Returns 0 (Index of 1).
- **Single Element:** `[10]` → Returns 0.
- **Max Rotation:** `[2, 3, 4, 5, 1]` → Returns 4 (Index of 1).
- **Duplicates:** Standard logic requires O(N) if `nums[low] == nums[mid] == nums[high]`.

---

## Mistakes

- Forgetting that rotation count = index of the minimum.
- Returning the minimum value instead of its index.
- Not handling the case where the array is already sorted (0 rotations).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Binary search halves the search space at each step.  
Space: O(1) → Constant space used for pointers.

---

## Similar Problems

- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #arrays
  - [[Binary Search]] [[Arrays]] [[Searching]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [Find Rotation Count (GeeksforGeeks)](https://www.geeksforgeeks.org/find-rotation-count-rotated-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
