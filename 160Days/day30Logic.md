To solve the "Search in Rotated Sorted Array" problem efficiently, you can use a modified binary search. Here's the step-by-step approach:

### Implementation in Java
Here is the completed function:

```java
class Solution {
    int search(int[] arr, int key) {
        int start = 0, end = arr.length - 1;

        while (start <= end) {
            int mid = start + (end - start) / 2;

            // Check if mid is the key
            if (arr[mid] == key) {
                return mid;
            }

            // Determine if the left half is sorted
            if (arr[start] <= arr[mid]) {
                // Check if the key lies in the sorted left half
                if (key >= arr[start] && key < arr[mid]) {
                    end = mid - 1;
                } else {
                    start = mid + 1;
                }
            } else {
                // Right half must be sorted
                if (key > arr[mid] && key <= arr[end]) {
                    start = mid + 1;
                } else {
                    end = mid - 1;
                }
            }
        }

        // Key not found
        return -1;
    }
}
```


### Approach
1. **Identify the pivot**:
   - The array is rotated, so the pivot divides the array into two sorted halves.
2. **Binary Search**:
   - Use the middle element to decide whether to search in the left or right half.
   - Compare the middle element with the start and end of the current range to determine whether the left or right half is sorted.
   - Narrow down the search range accordingly.



### Explanation of the Code
1. **Mid-point Calculation**: 
   - `int mid = start + (end - start) / 2` prevents overflow in case of large values of `start` and `end`.
2. **Checking the Sorted Half**:
   - Compare `arr[start]` and `arr[mid]` to determine if the left half is sorted.
3. **Key Search**:
   - Depending on whether the key lies in the sorted half, update the `start` or `end` pointer.
4. **End of Loop**:
   - If `start > end`, the key does not exist in the array, so return `-1`.

### Complexity Analysis
- **Time Complexity**: \(O(\log n)\) because we reduce the search range by half at each step.
- **Space Complexity**: \(O(1)\) as no additional space is used.

Let's dry run the code with an example to understand how it works.

### Example
**Input**:  
`arr = [5, 6, 7, 8, 9, 10, 1, 2, 3]`, `key = 3`

---

### Initial Setup:
- `start = 0`, `end = 8` (array indices)
- `arr[start] = 5`, `arr[end] = 3`

---

### Step-by-step Execution

#### Iteration 1:
- **Calculate `mid`**:  
  `mid = start + (end - start) / 2 = 0 + (8 - 0) / 2 = 4`  
  `arr[mid] = 9`

- **Check if `arr[mid] == key`**:  
  `arr[mid] = 9`, `key = 3` → Not equal.

- **Determine sorted half**:  
  Since `arr[start] <= arr[mid]` (`5 <= 9`), the left half `[5, 6, 7, 8, 9]` is sorted.

- **Check if `key` lies in the sorted half**:  
  `key >= arr[start] && key < arr[mid]` → `3 >= 5 && 3 < 9` → False.  
  Update: `start = mid + 1 = 5`.

---

#### Iteration 2:
- **Calculate `mid`**:  
  `mid = start + (end - start) / 2 = 5 + (8 - 5) / 2 = 6`  
  `arr[mid] = 1`

- **Check if `arr[mid] == key`**:  
  `arr[mid] = 1`, `key = 3` → Not equal.

- **Determine sorted half**:  
  Since `arr[start] > arr[mid]` (`10 > 1`), the right half `[1, 2, 3]` is sorted.

- **Check if `key` lies in the sorted half**:  
  `key > arr[mid] && key <= arr[end]` → `3 > 1 && 3 <= 3` → True.  
  Update: `start = mid + 1 = 7`.

---

#### Iteration 3:
- **Calculate `mid`**:  
  `mid = start + (end - start) / 2 = 7 + (8 - 7) / 2 = 7`  
  `arr[mid] = 2`

- **Check if `arr[mid] == key`**:  
  `arr[mid] = 2`, `key = 3` → Not equal.

- **Determine sorted half**:  
  Since `arr[start] <= arr[mid]` (`2 <= 2`), the left half `[2]` is sorted.

- **Check if `key` lies in the sorted half**:  
  `key >= arr[start] && key < arr[mid]` → `3 >= 2 && 3 < 2` → False.  
  Update: `start = mid + 1 = 8`.

---

#### Iteration 4:
- **Calculate `mid`**:  
  `mid = start + (end - start) / 2 = 8 + (8 - 8) / 2 = 8`  
  `arr[mid] = 3`

- **Check if `arr[mid] == key`**:  
  `arr[mid] = 3`, `key = 3` → Match found!  
  **Return**: `8`.

---

### Final Output:
The key `3` is found at index `8`.

---

### Key Points Observed
1. The algorithm narrows down the range with each iteration by using the sorted property of the array.
2. It handles rotation by identifying the sorted half in each step. 
3. The solution works efficiently in \(O(\log n)\) time.