# java
```java
class Solution {
    public int findMin(int[] arr) {
        int low = 0, high = arr.length - 1;
        
        while (low < high) {
            int mid = low + (high - low) / 2;
            
            // If mid element is greater than the last element, the minimum is in the right half
            if (arr[mid] > arr[high]) {
                low = mid + 1;
            } else {
                // Otherwise, the minimum is in the left half or at mid
                high = mid;
            }
        }
        
        // At the end, low and high will point to the minimum element
        return arr[low];
    }
}





```


To find the minimum element in a sorted and rotated array, we can leverage a modified binary search approach. Here's how it works:

### Approach:
1. **Binary Search Logic**:
   - Since the array is sorted and then rotated, the minimum element is the "pivot point" where the rotation occurs.
   - Use the `mid` index to compare with the `high` index to decide the direction of the search:
     - If `arr[mid]` > `arr[high]`, the minimum element lies in the right half.
     - Otherwise, it lies in the left half (including `mid`).

2. **Key Observations**:
   - A sorted array without rotation will have the smallest element at `arr[0]`.
   - When `arr[mid]` is less than `arr[high]`, it indicates the minimum is to the left or at `mid`.

3. **Constraints**:
   - Time Complexity: \(O(\log n)\) due to binary search.
   - Space Complexity: \(O(1)\) as it uses constant space.




Let's dry-run the given code with an example to understand how it works step by step.

---

### Example Input: 
`arr = [5, 6, 1, 2, 3, 4]`

### Initial State:
- `low = 0`, `high = 5` (indices of the first and last elements)
- **Goal**: Find the minimum element.

---

### Iteration 1:
- Calculate `mid`:  
  \( \text{mid} = 0 + (5 - 0) / 2 = 2 \)
- `arr[mid] = arr[2] = 1`  
- Compare `arr[mid]` with `arr[high]`:  
  \( \text{arr[mid]} (1) \leq \text{arr[high]} (4) \)  
  - This indicates the minimum is in the **left half** or at `mid`.
  - Update `high = mid = 2`.

---

### Iteration 2:
- New range: `low = 0`, `high = 2`.
- Calculate `mid`:  
  \( \text{mid} = 0 + (2 - 0) / 2 = 1 \)
- `arr[mid] = arr[1] = 6`  
- Compare `arr[mid]` with `arr[high]`:  
  \( \text{arr[mid]} (6) > \text{arr[high]} (1) \)  
  - This indicates the minimum is in the **right half**.
  - Update `low = mid + 1 = 2`.

---

### Iteration 3:
- New range: `low = 2`, `high = 2`.
- Since `low == high`, the loop exits.

---

### Result:
- The minimum element is `arr[low] = arr[2] = 1`.

---

### Summary of Steps:
| Iteration | `low` | `high` | `mid` | `arr[mid]` | Condition               | Action         |
|-----------|-------|--------|-------|------------|-------------------------|----------------|
| 1         | 0     | 5      | 2     | 1          | `arr[mid] <= arr[high]` | `high = mid`   |
| 2         | 0     | 2      | 1     | 6          | `arr[mid] > arr[high]`  | `low = mid + 1`|
| 3         | 2     | 2      | -     | -          | `low == high`           | Exit loop      |

### Output:
`1`

---

### Test Additional Example:
#### Input:
`arr = [3, 4, 5, 1, 2]`

#### Dry Run:
1. Initial state: `low = 0`, `high = 4`.
2. Iteration 1:  
   `mid = 2`, `arr[mid] = 5`.  
   \( \text{arr[mid]} > \text{arr[high]} (2) \).  
   Update `low = mid + 1 = 3`.
3. Iteration 2:  
   `low = 3`, `high = 4`.  
   `mid = 3`, `arr[mid] = 1`.  
   \( \text{arr[mid]} \leq \text{arr[high]} (2) \).  
   Update `high = mid = 3`.
4. Exit loop (`low == high`): `arr[low] = 1`.

**Output**: `1`

