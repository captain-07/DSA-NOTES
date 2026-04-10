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
  - #Amazon #Microsoft #Google #Adobe #Walmart #Flipkart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #modified-binary-search [[Modified Binary Search]]

## Pattern

Modified Binary Search (Finding Inflection Point)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

- In a sorted array rotated $K$ times, the number of rotations $K$ is **exactly equal to the index of the minimum element**.
- The minimum element is the only element that is smaller than its predecessor (the "pivot" or "inflection point").

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Rotations = Index of the minimum element. Use Binary Search to find the unsorted half; the minimum always lies in the unsorted part or is the first element of a sorted part.

---

## Approach

### Brute Force
- Linearly traverse the array to find the minimum element or the first element where `arr[i] < arr[i-1]`.
- **Time Complexity:** O(N)
- **Space Complexity:** O(1)

### Optimal (Binary Search)
- Use two pointers `low` and `high`.
- If `arr[low] <= arr[high]`, the array is already sorted in that range; `arr[low]` is the minimum.
- Otherwise, find `mid`. If the left half `[low...mid]` is sorted (`arr[low] <= arr[mid]`), the minimum must be in the right half. If the right half is sorted, the minimum is in the left half (including `mid`).
- **Time Complexity:** O(log N)
- **Space Complexity:** O(1)

---

## Code (Python)

```python
class Solution:
    def findKRotation(self, arr: list[int]) -> int:
        n = len(arr)
        low, high = 0, n - 1
        ans = float('inf')
        index = 0
        
        while low <= high:
            # If the current search space is already sorted
            if arr[low] <= arr[high]:
                if arr[low] < ans:
                    index = low
                    ans = arr[low]
                break
            
            mid = (low + high) // 2
            
            # If left half is sorted, the min is in the right half
            if arr[low] <= arr[mid]:
                if arr[low] < ans:
                    index = low
                    ans = arr[low]
                low = mid + 1
            # If right half is sorted, the min is in the left half
            else:
                if arr[mid] < ans:
                    index = mid
                    ans = arr[mid]
                high = mid - 1
                
        return index
```

---

## Dry Run (Smart Example)

**Input:** `arr = [4, 5, 6, 7, 0, 1, 2]`

| Step | low | high | mid | arr[mid] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 7 | `arr[0] <= arr[3]` (4 <= 7). Left is sorted. Min might be `arr[0]=4`. Move `low = 4`. |
| 2 | 4 | 6 | 5 | 1 | `arr[4] <= arr[6]` (0 <= 2). Search space is sorted. `arr[4]=0` is min. |
| 3 | 4 | 6 | - | - | `ans = 0`, `index = 4`. Loop breaks. |

**Result:** 4 rotations.

---

## Edge Cases

- **Already Sorted:** `[1, 2, 3]` → Min at index 0, rotations = 0.
- **Rotated N-1 Times:** `[2, 3, 1]` → Min at index 2, rotations = 2.
- **Single Element:** `[5]` → Min at index 0, rotations = 0.
- **Two Elements:** `[2, 1]` → Min at index 1, rotations = 1.

---

## Mistakes

- **Returning the value instead of the index:** Always remember rotations = index.
- **Handling duplicates:** If duplicates exist, `arr[low] == arr[mid] == arr[high]` case requires shrinking the window (`low++, high--`).
- **Standard Binary Search:** Forgetting that if the search space is already sorted, the first element is the minimum.
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Reducing search space by half in each iteration using binary search.  
Space: O(1) → No extra data structures used; only pointer variables.

---

## Similar Problems

- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II (with duplicates)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #searching
  - [[Binary Search]] [[Modified Binary Search]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [GeeksforGeeks - Rotation](https://www.geeksforgeeks.org/problems/rotation4723/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
