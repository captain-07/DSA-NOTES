---
created: 2026-04-04
revisions:
  - 2026-04-06
  - 2026-04-11
  - 2026-04-19
  - 2026-05-04
---

# Single Element In A Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #bitmanipulation [[Bit Manipulation]]
  - #arrays [[Arrays]]

---
## Pattern

Binary Search (Index Parity Partitioning)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

In a sorted array where every element appears twice except one:
- **Before the single element:** Pairs start at **even** indices and end at **odd** indices (`(even, odd)`).
- **After the single element:** Pairs start at **odd** indices and end at **even** indices (`(odd, even)`).
- We use Binary Search to find the point where this parity rule breaks.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use the XOR trick: `mid ^ 1`. 
- If `mid` is even, `mid ^ 1` is `mid + 1`.
- If `mid` is odd, `mid ^ 1` is `mid - 1`.
Check if `nums[mid] == nums[mid ^ 1]` to decide the search direction.

---

## Approach

### Brute Force
- Linear scan through the array comparing `nums[i]` with `nums[i+1]`.
- Time: $O(n)$
- Space: $O(1)$

### Better
- XOR all elements in the array. The result is the single element.
- Time: $O(n)$
- Space: $O(1)$

### Optimal
1. Initialize `low = 0`, `high = len(nums) - 2`.
2. While `low <= high`:
   - Calculate `mid`.
   - Use the **XOR trick**: if `nums[mid] == nums[mid ^ 1]`, it means we are in the "left" part of the array (before the single element). Move `low = mid + 1`.
   - Otherwise, we are in the "right" part or at the single element. Move `high = mid - 1`.
3. Return `nums[low]`.

---

## Code (Python)

```python
def singleNonDuplicate(nums: list[int]) -> int:
    # We search in the range [0, n-2] to avoid index out of bounds
    low, high = 0, len(nums) - 2
    
    while low <= high:
        mid = (low + high) // 2
        
        # XOR Trick: 
        # If mid is even, mid^1 is mid+1. If mid is odd, mid^1 is mid-1.
        # This checks if the pair (even, odd) is intact.
        if nums[mid] == nums[mid ^ 1]:
            # Pair is correct, single element is further right
            low = mid + 1
        else:
            # Parity broken, single element is to the left (including mid)
            high = mid - 1
            
    return nums[low]
```

---

## Dry Run (Smart Example)

Input: `nums = [1, 1, 2, 3, 3, 4, 4]`

| Step | low | high | mid | `mid ^ 1` | Comparison (`nums[mid] == nums[mid^1]`) | Action |
| :--- | :-- | :--- | :-- | :------- | :------------------------------------- | :----- |
| 1 | 0 | 5 | 2 | 3 | `nums[2](2) == nums[3](3)` -> **False** | `high = 1` |
| 2 | 0 | 1 | 0 | 1 | `nums[0](1) == nums[1](1)` -> **True** | `low = 1` |
| 3 | 1 | 1 | 1 | 0 | `nums[1](1) == nums[0](1)` -> **True** | `low = 2` |
| 4 | 2 | 1 | - | - | Loop terminates (`low > high`) | Return `nums[2] = 2` |

---

## Edge Cases

- **Single element at index 0:** `[1, 2, 2, 3, 3]` -> Binary search correctly shifts `high` left.
- **Single element at the end:** `[1, 1, 2, 2, 3]` -> Binary search correctly shifts `low` right.
- **Array size 1:** `[1]` -> `high` starts at -1, returns `nums[0]`.
- **Large numbers:** Handled correctly by standard comparison.

---

## Mistakes

- **User Mistake:** Manually checking `if mid % 2 == 0` and comparing with `mid + 1` or `mid - 1`. 
- **Fix:** Use the **`mid ^ 1` trick** to handle both even/odd cases in one line.
- Searching up to `n-1` instead of `n-2` can lead to index out of bounds if not careful.
- Forgetting the array is **sorted** (if it weren't sorted, only the XOR $O(n)$ approach would work).

---

## Complexity

Time: $O(\log n)$ → Binary search halves the search space each iteration.  
Space: $O(1)$ → Only a few pointers used.

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch 
  - [[Binary Search]] [[Bit Manipulation]]
  - Revision Date: 2026-04-04
  - Related: [[Find Peak Element]], [[Search in Rotated Sorted Array]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-06)
- [ ] Day 7 Revision (2026-04-11)
- [ ] Day 15 Revision (2026-04-19)
- [ ] Day 30 Revision (2026-05-04)
