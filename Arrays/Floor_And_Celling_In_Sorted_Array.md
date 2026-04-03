---
created: 2026-04-03
revisions:
  - 2026-04-05
  - 2026-04-10
  - 2026-04-18
  - 2026-05-03
---

# Floor And Celling In Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Samsung #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

## Pattern

Modified Binary Search (Range Seeking)

---
## Difficulty

Easy
#easy 

---

## ⚡ Key Idea (Core Insight)

Since the array is sorted, use **Binary Search** to find the boundaries. 
- **Floor:** The largest element $\le X$. If `arr[mid] <= X`, it's a candidate for floor; move right to find a larger one.
- **Ceiling:** The smallest element $\ge X$. If `arr[mid] >= X`, it's a candidate for ceiling; move left to find a smaller one.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Floor is the "rightmost" valid element $\le X$; Ceiling is the "leftmost" valid element $\ge X$. If `arr[mid] == X`, both floor and ceiling are $X$.

---

## Approach

### Brute Force
- Linearly traverse the array to find the last element $\le X$ and first element $\ge X$.
- Time: $O(N)$

### Optimal
1. Initialize `floor = -1` and `ceil = -1`.
2. Perform Binary Search.
3. If `arr[mid] == X`: both floor and ceil are $X$, return immediately.
4. If `arr[mid] < X`: Update `floor = arr[mid]`, search right half (`low = mid + 1`).
5. If `arr[mid] > X`: Update `ceil = arr[mid]`, search left half (`high = mid - 1`).
- Time: $O(\log N)$

---

## Code (Python)

```python
def findFloorCeil(arr, x):
    low, high = 0, len(arr) - 1
    floor, ceil = -1, -1
    
    while low <= high:
        mid = (low + high) // 2
        
        if arr[mid] == x:
            return (arr[mid], arr[mid])
        
        if arr[mid] < x:
            floor = arr[mid] # Potential floor found
            low = mid + 1    # Try to find a larger one
        else:
            ceil = arr[mid]  # Potential ceiling found
            high = mid - 1   # Try to find a smaller one
            
    return (floor, ceil)
```

---

## Dry Run (Smart Example)

**Input:** `arr = [3, 4, 7, 8, 10]`, `X = 5`

| Step | Variables (low, high, mid) | arr[mid] | Action | Floor | Ceil |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | L=0, H=4, M=2 | 7 | 7 > 5: search left | -1 | 7 |
| 2 | L=0, H=1, M=0 | 3 | 3 < 5: search right | 3 | 7 |
| 3 | L=1, H=1, M=1 | 4 | 4 < 5: search right | 4 | 7 |
| 4 | L=2, H=1 | - | Loop terminates | **4** | **7** |

---

## Edge Cases

- **X is smaller than arr[0]:** Floor remains -1, Ceil is arr[0].
- **X is larger than arr[n-1]:** Floor is arr[n-1], Ceil remains -1.
- **X exists in array:** Both floor and ceil equal X.
- **Array size is 1:** Compare single element with X and update accordingly.

---

## Mistakes

- Returning index instead of value (read problem carefully).
- Forgetting to handle the "not found" case (return -1).
- **User Mistake:** No specific note provided (ensure revision notes are created for all fundamental BS variations).

---

## Complexity

Time: $O(\log N)$ → Binary search halves the search space each iteration.  
Space: $O(1)$ → Only a few pointers/variables used.

---

## Tags and Properties
- #dsa #important #revisit #searching 
- [[Binary Search]] [[Arrays]]
- Revision Date: 2026-04-03
- Related: [[Search Insert Position]], [[Lower Bound and Upper Bound]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-05)
- [ ] Day 7 Revision (2026-04-10)
- [ ] Day 15 Revision (2026-04-18)
- [ ] Day 30 Revision (2026-05-03)
