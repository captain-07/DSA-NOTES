---
created: 2026-03-22
revisions:
  - 2026-03-24
  - 2026-03-29
  - 2026-04-06
  - 2026-04-21
---

## Metadata & Placement Tags
- **Target Companies:** #TCS #Amazon #Microsoft #Google #Service-Based
- **Confidence Level:** [ ] Low [ ] Mid [ ] High
- **Related Concepts:** #bitwise [[Bitwise Operations]] #mathematics [[Mathematical Logic]] #arrays [[Array Traversal]]

---

## Difficulty
- **Level:** Easy
- **Tag:** #easy

---

## Pattern
- **Algorithmic Pattern:** Bit Manipulation / Arithmetic Series

---

## Key Idea
The core intuition relies on the mathematical property of **XOR**: $a \oplus a = 0$ and $a \oplus 0 = a$. By XORing all integers from $1$ to $n$ with all elements present in the array, every number appearing twice will cancel out to zero, leaving only the missing element (which appears only once in the combined set).

---

## Approach

### Brute Force
The naive approach involves sorting the array first, which takes $O(n \log n)$ time. After sorting, we iterate through the array and check if `arr[i]` equals $i + 1$. The first mismatch identifies the missing element. Alternatively, using a Hash Map or a boolean frequency array would take $O(n)$ time but requires $O(n)$ extra space, which is inefficient for large datasets.

### Optimal (XOR Method)
The XOR approach is the most memory-efficient method as it avoids the potential integer overflow associated with the summation formula ($S = \frac{n(n+1)}{2}$) in languages with fixed-size integers.
1. Initialize a variable `xor_all` by XORing all numbers from $1$ to $n$.
2. Initialize another variable `xor_arr` by XORing all elements currently in the array.
3. The result of `xor_all ^ xor_arr` is the missing number.
*Note: You can also do this in a single loop to further optimize.*

---

## Code

```python
def find_missing_element(nums, n):
    """
    Finds the missing element in an array of size n-1 
    containing distinct numbers in the range [1, n].
    """
    xor_val = 0
    
    # XOR all numbers from 1 to n
    for i in range(1, n + 1):
        xor_val ^= i
        
    # XOR the result with all elements in the array
    # Elements present in the array will cancel out (x ^ x = 0)
    for num in nums:
        xor_val ^= num
        
    return xor_val

# Example usage:
# arr = [1, 2, 4, 5], n = 5
# Output: 3
```

---

## Dry Run
**Input:** `nums = [1, 2, 4, 5]`, `n = 5`

| Step | Operation | Current `xor_val` (Decimal) | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Init & Loop $1 \dots 5$ | $1 \oplus 2 \oplus 3 \oplus 4 \oplus 5 = 1$ | XORing sequence $1$ to $n$ result is $1$ |
| 2 | `xor_val ^ nums[0]` | $1 \oplus 1 = 0$ | $1$ cancels out |
| 3 | `xor_val ^ nums[1]` | $0 \oplus 2 = 2$ | $2$ is tracked |
| 4 | `xor_val ^ nums[2]` | $2 \oplus 4 = 6$ | Bitwise $010 \oplus 100 = 110$ |
| 5 | `xor_val ^ nums[3]` | $6 \oplus 5 = 3$ | **Final Result:** All except $3$ cancelled out |

---

## Edge Cases
1. **Missing First Element:** Array is `[2, 3, 4]`, $n=4$. The logic should correctly return $1$.
2. **Missing Last Element:** Array is `[1, 2, 3]`, $n=4$. The logic should correctly return $4$.
3. **$n = 2$:** Smallest possible range where the array has only one element (e.g., `[1]`, $n=2$, missing $2$).
4. **Unsorted Input:** The XOR method is order-independent, so an input like `[4, 1, 5, 2]` should still return $3$.

---

## Mistakes

> [!CAUTION] Mistakes & XOR Logic
> - **User Note - XOR Operation:** A common mistake is starting the XOR loop from $0$ to $n-1$ (array indices) but forgetting that the numbers range from $1$ to $n$. You must ensure you XOR the **values** $1 \dots n$, not just the indices.
> - **Off-by-one:** Forgetting to include $n$ in the XOR sequence. If the array has $n-1$ elements, the range is inclusive of $n$.
> - **Initialization:** Ensure `xor_val` is initialized to $0$. Initializing to the first element of the array and then looping can lead to skipping the $1 \dots n$ XOR logic.

---

## Complexity
- **Time Complexity:** $O(n)$
  - Justification: We perform two linear passes (one for the range $1 \dots n$ and one for the array elements).
- **Space Complexity:** $O(1)$
  - Justification: We only use a single integer variable `xor_val` regardless of the input size.

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-03-24)
- [ ] Day 7 Revision (2026-03-29)
- [ ] Day 15 Revision (2026-04-06)
- [ ] Day 30 Revision (2026-04-21)
