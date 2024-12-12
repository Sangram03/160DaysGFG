# java
```java
class Solution {
    int countFreq(int[] arr, int target) {
        int first = findFirstOccurrence(arr, target);
        if (first == -1) {
            return 0; // Target not found
        }
        int last = findLastOccurrence(arr, target);
        return last - first + 1; // Total occurrences
    }

    private int findFirstOccurrence(int[] arr, int target) {
        int low = 0, high = arr.length - 1, first = -1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (arr[mid] == target) {
                first = mid;
                high = mid - 1; // Move left to find earlier occurrence
            } else if (arr[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return first;
    }

    private int findLastOccurrence(int[] arr, int target) {
        int low = 0, high = arr.length - 1, last = -1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (arr[mid] == target) {
                last = mid;
                low = mid + 1; // Move right to find later occurrence
            } else if (arr[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return last;
    }
}





```
This problem can be efficiently solved using **binary search** because the array is sorted. Here's how:

1. **Approach**:  
   - Use two binary search calls:
     - First to find the **first occurrence** of the target.
     - Second to find the **last occurrence** of the target.
   - The number of occurrences is calculated as:  
     \[
     \text{Occurrences} = (\text{last occurrence index} - \text{first occurrence index} + 1)
     \]
   - If the target is not found, return `0`.


   Let's dry-run the given code using an example input to understand its behavior and validate the logic.

### Input:
```plaintext
arr = [1, 1, 2, 2, 2, 2, 3], target = 2
```

### Step-by-Step Execution:

#### 1. **Calling `countFreq`**
- `countFreq(arr, 2)` is called.

#### 2. **First Occurrence - `findFirstOccurrence`**
- Initialize: `low = 0`, `high = 6`, `first = -1`.
- **Iteration 1**:
  - `mid = 3` (`(0 + 6) / 2`).
  - `arr[mid] = 2`, which equals `target`.
  - Update `first = 3`.
  - Move `high = mid - 1 = 2`.
- **Iteration 2**:
  - `mid = 1` (`(0 + 2) / 2`).
  - `arr[mid] = 1`, which is less than `target`.
  - Move `low = mid + 1 = 2`.
- **Iteration 3**:
  - `mid = 2` (`(2 + 2) / 2`).
  - `arr[mid] = 2`, which equals `target`.
  - Update `first = 2`.
  - Move `high = mid - 1 = 1`.
- End loop: `first = 2`.

#### 3. **Last Occurrence - `findLastOccurrence`**
- Initialize: `low = 0`, `high = 6`, `last = -1`.
- **Iteration 1**:
  - `mid = 3` (`(0 + 6) / 2`).
  - `arr[mid] = 2`, which equals `target`.
  - Update `last = 3`.
  - Move `low = mid + 1 = 4`.
- **Iteration 2**:
  - `mid = 5` (`(4 + 6) / 2`).
  - `arr[mid] = 2`, which equals `target`.
  - Update `last = 5`.
  - Move `low = mid + 1 = 6`.
- **Iteration 3**:
  - `mid = 6` (`(6 + 6) / 2`).
  - `arr[mid] = 3`, which is greater than `target`.
  - Move `high = mid - 1 = 5`.
- End loop: `last = 5`.

#### 4. **Calculate Result**
- `first = 2`, `last = 5`.
- `Occurrences = last - first + 1 = 5 - 2 + 1 = 4`.

### Output:
```plaintext
4
```

---

### **Additional Example:**
#### Input:
```plaintext
arr = [1, 1, 2, 2, 2, 2, 3], target = 4
```

#### Execution:
1. `findFirstOccurrence`: Loop ends with `first = -1` because `target` is not found.
2. `countFreq` returns `0`.

---

### Final Notes:
The logic is correct, and the dry run demonstrates that it efficiently calculates the occurrences of a target in a sorted array.