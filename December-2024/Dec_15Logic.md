Here’s how you can solve the peak element problem in Java. We'll implement a function `peakElement` that uses a binary search approach to achieve \(O(\log n)\) time complexity, which is efficient for the given constraints.

### Implementation

```java
class Solution {
    public int peakElement(int[] arr) {
        int low = 0, high = arr.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            // Check if mid is a peak
            if ((mid == 0 || arr[mid] >= arr[mid - 1]) && 
                (mid == arr.length - 1 || arr[mid] >= arr[mid + 1])) {
                return mid;
            }

            // Move to the left side if the left neighbor is greater
            if (mid > 0 && arr[mid - 1] > arr[mid]) {
                high = mid - 1;
            } else { // Otherwise, move to the right side
                low = mid + 1;
            }
        }
        
        return -1; // This line should never be reached
    }
}
```

### Explanation

1. **Binary Search Logic**:
   - The array has no two adjacent elements that are the same, ensuring no ambiguity.
   - We check whether the middle element of the current range is a peak.
   - If not, based on the properties of the array, either the left or the right neighbor will lead us to a peak.

2. **Base Cases**:
   - If `mid` is at the start of the array, only compare it to the right neighbor.
   - If `mid` is at the end, compare it to the left neighbor.

3. **Why Binary Search**:
   - By moving towards the larger neighbor, you guarantee to find a peak due to the property that every array has at least one peak.


### Complexity

- **Time Complexity**: \(O(\log n)\), due to binary search.
- **Space Complexity**: \(O(1)\), as no additional space is used.



Let's perform a dry run of the provided code to ensure it works as expected.

### Input
Array: `arr = [10, 20, 15, 2, 23, 90, 80]`

### Execution Steps

#### Initial State:
- `low = 0`, `high = 6` (length of array - 1).

---

#### **Iteration 1:**
- Calculate `mid`:  
  \[
  mid = low + \frac{(high - low)}{2} = 0 + \frac{(6 - 0)}{2} = 3
  \]
- `arr[mid] = arr[3] = 2`
- Check if `arr[3]` is a peak:
  - Compare `arr[3]` with its neighbors: `arr[2] = 15` and `arr[4] = 23`.  
    - \(arr[3] < arr[2]\) → Not a peak.
- Since the left neighbor (`arr[2]`) is greater, update:
  - `high = mid - 1 = 2`.

---

#### **Iteration 2:**
- Update state: `low = 0`, `high = 2`.
- Calculate `mid`:  
  \[
  mid = 0 + \frac{(2 - 0)}{2} = 1
  \]
- `arr[mid] = arr[1] = 20`
- Check if `arr[1]` is a peak:
  - Compare `arr[1]` with its neighbors: `arr[0] = 10` and `arr[2] = 15`.  
    - \(arr[0] < arr[1] > arr[2]\) → Peak found.
- Return `mid = 1`.

---

### Output:
The function returns `1`, which is the index of a peak element (`arr[1] = 20`).

---

### Additional Test Case Dry Run

#### Input
Array: `arr = [1, 2, 4, 5, 7, 8, 3]`

#### Execution Steps

---

#### **Iteration 1:**
- Initial state: `low = 0`, `high = 6`.
- Calculate `mid`:  
  \[
  mid = 0 + \frac{(6 - 0)}{2} = 3
  \]
- `arr[mid] = arr[3] = 5`
- Check if `arr[3]` is a peak:
  - Compare `arr[3]` with its neighbors: `arr[2] = 4` and `arr[4] = 7`.  
    - \(arr[3] < arr[4]\) → Not a peak.
- Move to the right, update:
  - `low = mid + 1 = 4`.

---

#### **Iteration 2:**
- Update state: `low = 4`, `high = 6`.
- Calculate `mid`:  
  \[
  mid = 4 + \frac{(6 - 4)}{2} = 5
  \]
- `arr[mid] = arr[5] = 8`
- Check if `arr[5]` is a peak:
  - Compare `arr[5]` with its neighbors: `arr[4] = 7` and `arr[6] = 3`.  
    - \(arr[4] < arr[5] > arr[6]\) → Peak found.
- Return `mid = 5`.

---

### Output:
The function returns `5`, which is the index of a peak element (`arr[5] = 8`).

### Summary
The function efficiently identifies the index of a peak element using binary search, with \(O(\log n)\) time complexity.