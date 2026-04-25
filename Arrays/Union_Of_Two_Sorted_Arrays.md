---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Union Of Two Sorted Arrays

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #GoldmanSachs #TCS

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]]
  - #twopointers [[Two Pointers]]
  - #hashing [[Hashing]]

---
## Pattern

Two Pointers (Optimal) / Hashing (Better)

---
## Difficulty

Easy | #easy

---

## ⚡ Key Idea (Core Insight)

Since arrays are **sorted**, we can traverse both simultaneously using two pointers. To handle duplicates without extra space (like a Set), only append an element if it is different from the last element added to the result list.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare $arr1[i]$ and $arr2[j]$; move the smaller pointer. If equal, move both. Only add to `res` if `res[-1] != val`.

---

## Approach

### Brute Force
- Put all elements from both arrays into a `Set`, then convert the set back to a sorted list.
- **Complexity:** $O((N+M) \log (N+M))$ time due to sorting the set.

### Better
- Use a `Set` to store unique elements while iterating through both arrays (Merge step).
- **Complexity:** $O((N+M) \log (\text{unique elements}))$ if using a TreeMap/OrderedSet, or $O(N+M)$ with a HashSet.

### Optimal
1. Use two pointers `i` and `j` starting at index 0.
2. Compare $arr1[i]$ and $arr2[j]$.
3. Add the smaller element to `res` if it's not already at `res[-1]`.
4. If elements are equal, add once and increment both pointers.
5. Handle remaining elements in either array using the same duplicate check.

---

## Code (Python)

```python
class Solution:
    def findUnion(self, a, b):
        n, m = len(a), len(b)
        i, j = 0, 0
        res = []
        
        def add_to_res(val):
            # Only add if res is empty or val is not a duplicate of the last element
            if not res or res[-1] != val:
                res.append(val)
        
        while i < n and j < m:
            if a[i] <= b[j]:
                add_to_res(a[i])
                if a[i] == b[j]:
                    j += 1 # Move j if elements are identical
                i += 1
            else:
                add_to_res(b[j])
                j += 1
        
        # Add remaining elements from array a
        while i < n:
            add_to_res(a[i])
            i += 1
            
        # Add remaining elements from array b
        while j < m:
            add_to_res(b[j])
            j += 1
            
        return res
```

---

## Dry Run (Smart Example)

**Input:** `a = [1, 2, 2, 3]`, `b = [2, 3, 3, 4, 5]`

| Step | i, j | Comparison | res | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 0, 0 | 1 < 2 | [1] | a[0] added. i++ |
| 2 | 1, 0 | 2 == 2 | [1, 2] | a[1] added. i++, j++ |
| 3 | 2, 1 | 2 < 3 | [1, 2] | a[2]=2. Dupe of res[-1], skip. i++ |
| 4 | 3, 1 | 3 == 3 | [1, 2, 3] | a[3] added. i++, j++ |
| 5 | 4, 2 | j < m | [1, 2, 3, 4, 5] | Exhaust b elements 4, 5. |

---

## Edge Cases

- **One array is empty:** The union is the unique elements of the other array.
- **Arrays are identical:** Result contains unique elements of one array.
- **All duplicates:** `[1,1,1]` and `[1,1]` results in `[1]`.
- **No overlapping elements:** `[1,2]` and `[3,4]` results in `[1,2,3,4]`.

---

## Mistakes

- **Index Out of Bounds:** Forgetting to process remaining elements after the main `while` loop.
- **Duplicate Handling:** Adding an element without checking `res[-1]`.
- **Empty Result Check:** Accessing `res[-1]` when `res` is empty (causes `IndexError`).
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(N + M)$ → We traverse both arrays exactly once.
- **Space:** $O(N + M)$ → Worst case, all elements are unique and stored in the result list.

---

## Similar Problems

- [Intersection of Two Sorted Arrays](https://leetcode.com/problems/intersection-of-two-arrays-ii/) - Easy
- [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/) - Easy
- [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) - Hard

---

## Tags and Properties
  - #dsa #important #revisit #arrays
  - [[Two Pointers]] [[Merging]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [GeeksforGeeks - Union of Two Sorted Arrays](https://www.geeksforgeeks.org/problems/union-of-two-sorted-arrays-1587115621/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
