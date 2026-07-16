---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Left Rotate Array By K Places

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Samsung #Adobe #TCS #Infosys

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #array [[Arrays]]
  - #twopointers [[Two Pointers]]
  - #reversal [[Reversal Algorithm]]

## Pattern

Reversal Algorithm (Divide and Conquer approach to rotation)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

- Handle $k > n$ by using $k = k \pmod n$ to avoid redundant rotations.
- To rotate **Left** by $k$: Reverse the first $k$ elements, reverse the remaining $n-k$ elements, then reverse the entire array. This effectively "shunts" the first $k$ elements to the end in the correct relative order.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Reverse $[0 \dots k-1]$, Reverse $[k \dots n-1]$, then Reverse $[0 \dots n-1]$.

---

## Approach

### Brute Force
- Store the first $k$ elements in a temporary array.
- Shift the rest of the array $k$ positions to the left.
- Copy the $k$ elements from the temporary array back to the end.
- **Complexity:** Time: $O(n)$, Space: $O(k)$.

### Better (Juggling Algorithm)
- Divide array into $GCD(n, k)$ sets and rotate elements within sets.
- **Complexity:** Time: $O(n)$, Space: $O(1)$. (Harder to implement in interviews).

### Optimal (Reversal Algorithm)
1. Normalize $k$: $k = k \% n$.
2. Reverse the first $k$ elements: `arr[0...k-1]`.
3. Reverse the rest: `arr[k...n-1]`.
4. Reverse the whole array: `arr[0...n-1]`.
- **Complexity:** Time: $O(n)$, Space: $O(1)$.

---

## Code (Python)

```python
class Solution:
    def leftRotate(self, arr: list[int], k: int) -> None:
        """
        Rotates the array to the left by k steps in-place.
        """
        n = len(arr)
        if n == 0: return
        
        # Step 1: Normalize k
        k = k % n
        if k == 0: return
        
        # Step 2: Reverse first k elements [0...k-1]
        self._reverse(arr, 0, k - 1)
        
        # Step 3: Reverse remaining elements [k...n-1]
        self._reverse(arr, k, n - 1)
        
        # Step 4: Reverse the whole array [0...n-1]
        self._reverse(arr, 0, n - 1)

    def _reverse(self, arr: list[int], start: int, end: int) -> None:
        while start < end:
            arr[start], arr[end] = arr[end], arr[start]
            start += 1
            end -= 1
```

---

## Dry Run (Smart Example)

**Input:** `arr = [10, 20, 30, 40, 50, 60]`, `k = 2`, `n = 6`

| Step | Operation | Array State | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | $k = 2 \% 6$ | `[10, 20, 30, 40, 50, 60]` | No change, $k=2$. |
| 2 | Reverse `arr[0:2]` | `[20, 10, 30, 40, 50, 60]` | First 2 elements reversed. |
| 3 | Reverse `arr[2:6]` | `[20, 10, 60, 50, 40, 30]` | Remaining 4 elements reversed. |
| 4 | Reverse `arr[0:6]` | `[30, 40, 50, 60, 10, 20]` | Final result achieved. |

---

## Edge Cases

- **$k = 0$ or $k = n$:** Array remains unchanged.
- **$k > n$:** Use modulo operator ($k \% n$).
- **Single element array:** No change possible.
- **Large $k$:** Ensure $k = k \% n$ is performed first to prevent out-of-bounds.

---

## Mistakes

- Forgetting to take $k = k \% n$.
- Off-by-one errors in the reversal indices (e.g., reversing up to $k$ instead of $k-1$).
- Confusing Left Rotate with Right Rotate (Right rotation reverses the whole array *first*).
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(n)$ → We iterate through the array roughly twice (reversing parts then the whole).
- **Space:** $O(1)$ → All operations are performed in-place.

---

## Similar Problems

- [Rotate Array (Right Rotate)](https://leetcode.com/problems/rotate-array/) - Medium
- [Check if Array Is Sorted and Rotated](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/) - Easy
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #arrays #rotation
- [[Arrays]] [[Two Pointers]] [[Reversal Algorithm]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [Left Rotate an Array - GeeksforGeeks](https://www.geeksforgeeks.org/problems/left-rotate-an-array-by-d-nodes/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
