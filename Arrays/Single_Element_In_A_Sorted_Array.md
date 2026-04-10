---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

---
# Single Element In A Sorted Array

---

## 🧩 Key Idea
Leverage the **index parity of pairs** in a sorted array: before the single element, pairs start at `even` indices and end at `odd` indices $(e, o)$, but after the single element, this pattern shifts to $(o, e)$.

---

## 🚀 Approach
Since the array is sorted and we need an $O(\log n)$ solution, **Binary Search** is the optimal choice.

1.  **Observation:** In a "perfect" array where every element has a pair, for any pair at indices $(i, j)$, $i$ is even and $j$ is odd ($j = i + 1$).
2.  **The Shift:** The single element disrupts this pattern.
    *   **Left of Single Element:** `nums[mid] == nums[mid ^ 1]` holds true (where `mid ^ 1` gives the partner index: if mid is even, `mid+1`; if mid is odd, `mid-1`).
    *   **Right of Single Element:** The pattern breaks. `nums[mid] != nums[mid ^ 1]`.
3.  **Binary Search Logic:**
    *   Check the `mid` element and its partner (using the XOR trick `mid ^ 1`).
    *   If they are equal, we are still in the "normal" zone (left of the single element), so move `low = mid + 1`.
    *   If they are not equal, we are either at the single element or to its right, so move `high = mid`.

---

## 💻 Code
```python
def singleNonDuplicate(nums: list[int]) -> int:
    # We search in the range [0, n-1]
    low = 0
    high = len(nums) - 1
    
    # Standard Binary Search
    while low < high:
        mid = (low + high) // 2
        
        # XOR Trick Explanation:
        # If mid is even, mid ^ 1 = mid + 1
        # If mid is odd, mid ^ 1 = mid - 1
        # This checks if we are in the (even, odd) pair sequence
        if nums[mid] == nums[mid ^ 1]:
            # Pattern is correct, single element is on the right
            low = mid + 1
        else:
            # Pattern is broken, mid could be the single element 
            # or it's further to the left
            high = mid
            
    return nums[low]
```

---

## 🏗️ Pattern
> [!IMPORTANT]
> **Binary Search on Parity**
> This problem belongs to the "Binary Search on a property change" pattern, where we find the point where a boolean condition flips from `True` to `False`.

---

## 🏃 Dry Run
**Input:** `nums = [1, 1, 2, 3, 3, 4, 4]`

| Step | low | high | mid | `mid ^ 1` | `nums[mid] == nums[mid^1]` | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 2 | `nums[3](3) == nums[2](2)` → **False** | `high = 3` |
| 2 | 0 | 3 | 1 | 0 | `nums[1](1) == nums[0](1)` → **True** | `low = 2` |
| 3 | 2 | 3 | 2 | 3 | `nums[2](2) == nums[3](3)` → **False** | `high = 2` |
| **End** | **2** | **2** | - | - | **Return nums[2] = 2** | - |

---

## ⚠️ Edge Cases
*   **Single Element Array:** `[1]` → `low` and `high` start at 0, loop doesn't run, returns `nums[0]`.
*   **Single Element at Start:** `[1, 2, 2, 3, 3]` → Binary search will correctly shrink `high` towards index 0.
*   **Single Element at End:** `[1, 1, 2, 2, 3]` → Binary search will correctly push `low` towards the last index.

---

## 💡 Mistakes
*   **Manual Index Handling:** Trying to check `mid-1` and `mid+1` manually often leads to complex `if-else` blocks and "Index Out of Bounds" errors.
*   **User Note:** *No specific note provided.*
*   **Pro-Tip:** Use the `mid ^ 1` trick to avoid checking if `mid` is even or odd. It elegantly finds the "intended partner" index.

---

## 📊 Complexity
- **Time Complexity:** $O(\log N)$ — Binary search reduces the search space by half each iteration.
- **Space Complexity:** $O(1)$ — Only a constant amount of extra space used for pointers.

---

## 🏆 Difficulty
**Medium**

---

## 📎 Metadata & Placement Tags
#dsa #binary-search #leetcode #array

---

## 🔗 Similar Problems
*   [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
*   [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
*   [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
