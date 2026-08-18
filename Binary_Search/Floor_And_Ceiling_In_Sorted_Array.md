---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Floor And Ceiling In Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Samsung #Adobe #Flipkart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]

## Pattern

Binary Search (Boundary Search)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Since the array is sorted, we use **Binary Search** to find the transition points. 
- **Floor:** The largest element $\leq X$. If `arr[mid] <= X`, `mid` is a potential floor; search the right half for a larger one.
- **Ceiling:** The smallest element $\geq X$. If `arr[mid] >= X`, `mid` is a potential ceiling; search the left half for a smaller one.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Floor is the "last element $\leq X$"; Ceiling is the "first element $\geq X$". Both are found in $O(\log N)$ using modified binary search logic.

---

## Approach

### Brute Force
- Iterate through the array once and track the maximum element $\leq X$ and minimum element $\geq X$.
- Time Complexity: $O(N)$

### Optimal
- Use two separate binary searches (or one combined search) to identify the floor and ceiling.
- **Floor Search:** If `arr[mid] <= X`, update `floor = arr[mid]` and move `low = mid + 1`.
- **Ceiling Search:** If `arr[mid] >= X`, update `ceil = arr[mid]` and move `high = mid - 1`.
- Time Complexity: $O(\log N)$

---

## Code (Python)

```python
class Solution:
    def getFloorAndCeil(self, arr: list, n: int, x: int) -> list:
        # Array must be sorted for Binary Search
        arr.sort() 
        
        floor = -1
        ceil = -1
        
        # Binary Search for Floor
        low, high = 0, n - 1
        while low <= high:
            mid = (low + high) // 2
            if arr[mid] <= x:
                floor = arr[mid]
                low = mid + 1
            else:
                high = mid - 1
                
        # Binary Search for Ceiling
        low, high = 0, n - 1
        while low <= high:
            mid = (low + high) // 2
            if arr[mid] >= x:
                ceil = arr[mid]
                high = mid - 1
            else:
                low = mid + 1
                
        return [floor, ceil]
```

---

## Dry Run (Smart Example)

**Input:** `arr = [3, 4, 7, 8, 10], x = 5`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `low=0, high=4, mid=2` | `arr[2]=7`. `7 > 5`. Ceil becomes `7`, move `high=1`. |
| 2 | `low=0, high=1, mid=0` | `arr[0]=3`. `3 < 5`. Floor becomes `3`, move `low=1`. |
| 3 | `low=1, high=1, mid=1` | `arr[1]=4`. `4 < 5`. Floor becomes `4`, move `low=2`. |
| 4 | `low > high` | Loop terminates. Floor = `4`, Ceil = `7`. |

---

## Edge Cases

- **X is smaller than all elements:** Floor is `-1`, Ceiling is `arr[0]`.
- **X is larger than all elements:** Floor is `arr[n-1]`, Ceiling is `-1`.
- **X is present in the array:** Floor and Ceiling are both `X`.
- **Array has duplicates:** Binary search correctly identifies the values.

---

## Mistakes

- Not handling the case where floor or ceiling does not exist (should return -1).
- Forgetting that the array must be sorted (if not provided sorted).
- Confusion between `low = mid + 1` and `high = mid - 1` when updating candidates.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(\log N)$ → We perform two binary searches over the array of size $N$.  
Space: $O(1)$ → No extra space used besides variables (unless sorting is required, then $O(\log N)$ or $O(N)$ depending on sort).

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #searching #boundaryconditions
  - [[Binary Search]] [[Lower Bound]]
  - Revision Date: 2026-04-10
  - **Problem Link:** [GeeksforGeeks - Ceil the Floor](https://www.geeksforgeeks.org/problems/ceil-the-floor2802/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
