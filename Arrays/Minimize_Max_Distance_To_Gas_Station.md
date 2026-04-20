---
created: 2026-04-20
revisions:
  - 2026-04-22
  - 2026-04-27
  - 2026-05-05
  - 2026-05-20
---

# Minimize Max Distance To Gas Station

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Directi

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #heap [[Heap]]
  - #greedy [[Greedy]]

## Pattern

Binary Search on Answer (Continuous Range)

---
## Difficulty

Hard  
#hard

---

## ⚡ Key Idea (Core Insight)

The goal is to find the minimum possible value of a "maximum distance" $D$. This is a classic **Binary Search on Answer** problem because the "feasibility" of a distance $D$ is monotonic: if we can achieve a max distance $D$, we can also achieve any $D' > D$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Binary search the **answer (distance)** in range $[0, 10^8]$. For a candidate distance `mid`, the number of stations required between $A$ and $B$ is $\lfloor (B - A) / mid \rfloor$.

---

## Approach

### Brute Force
- Iteratively find the largest gap between any two adjacent stations and insert one station there. Repeat $K$ times.
- **Time Complexity:** $O(K \cdot N)$

### Better (Heap)
- Use a **Max-Heap** to store all gaps. Extract the largest gap, "split" it by adding a station, and push the new resulting gaps back.
- **Time Complexity:** $O(K \log N)$ (Inefficient if $K$ is very large).

### Optimal (Binary Search)
1. **Range:** `low = 0`, `high = stations[-1] - stations[0]`.
2. **Precision:** Since the answer is floating-point, use a loop of 100 iterations or `while high - low > 1e-6`.
3. **Check Function:** For a distance `dist`, iterate through `stations` and calculate `count += math.floor((stations[i+1] - stations[i]) / dist)`.
4. **Logic:** If `count <= K`, `dist` is possible; try smaller (`high = mid`). Else, `low = mid`.

---

## Code (Python)

```python
import math

class Solution:
    def minmaxGasDist(self, stations: list[int], k: int) -> float:
        # Helper to check if a max distance 'dist' is achievable with k stations
        def can_place(dist):
            count = 0
            for i in range(len(stations) - 1):
                # Calculate how many stations needed to keep gaps <= dist
                count += math.floor((stations[i+1] - stations[i]) / dist)
            return count <= k

        low, high = 0, stations[-1] - stations[0]
        
        # Binary search for 100 iterations to ensure high precision (1e-6)
        for _ in range(100):
            mid = (low + high) / 2
            if can_place(mid):
                high = mid
            else:
                low = mid
                
        return high
```

---

## Dry Run (Smart Example)

**Input:** `stations = [1, 2, 8]`, `k = 2`

| Step | Mid (Dist) | Calculation (Gaps: 1, 6) | Total Needed | Result |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 3.5 | floor(1/3.5) + floor(6/3.5) = 0 + 1 | 1 <= 2 | high = 3.5 |
| 2 | 1.75 | floor(1/1.75) + floor(6/1.75) = 0 + 3 | 3 > 2 | low = 1.75 |
| 3 | 2.625 | floor(1/2.625) + floor(6/2.625) = 0 + 2 | 2 <= 2 | high = 2.625 |
| 4 | 2.1875 | floor(1/2.1875) + floor(6/2.1875) = 0 + 2 | 2 <= 2 | high = 2.1875 |

---

## Edge Cases

- **K = 0:** Max distance is simply the largest existing gap.
- **Large K:** New stations will be placed very close to each other, resulting in a very small `mid`.
- **Large Initial Gaps:** Binary search handles this naturally via the `count` calculation.

---

## Mistakes

- **Precision Error:** Using `while low < high` for floats instead of a fixed iteration count (100) or epsilon (`1e-6`).
- **Calculation Error:** Using `(gap // dist)` instead of `math.floor(gap / dist)` or not handling the edge case where `gap` is exactly a multiple of `dist` (though `floor` handles this correctly for "number of *additional* stations").
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(N \log(\frac{MaxDist}{\epsilon}))$ → $N$ is number of stations, $\epsilon$ is precision.  
Space: $O(1)$ → Only a few variables used for binary search.

---

## Similar Problems

- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #greedy #geometry
  - [[Binary Search]] [[Greedy]]
  - **Problem Link:** [LeetCode - Minimize Max Distance to Gas Station](https://leetcode.com/problems/minimize-max-distance-to-gas-station/) (Premium) / [LintCode 848](https://www.lintcode.com/problem/848/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-22)
- [ ] Day 7 Revision (2026-04-27)
- [ ] Day 15 Revision (2026-05-05)
- [ ] Day 30 Revision (2026-05-20)
