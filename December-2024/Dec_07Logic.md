# java
```java

class Solution {
    // Function to count inversions in the array
    static int inversionCount(int arr[]) {
        // Temporary array to help with merge sort
        int[] tempArr = new int[arr.length];
        return mergeSortAndCount(arr, tempArr, 0, arr.length - 1);
    }

    // Function to implement merge sort and count inversions
    static int mergeSortAndCount(int[] arr, int[] tempArr, int left, int right) {
        int invCount = 0;
        if (left < right) {
            // Find the middle point
            int mid = (left + right) / 2;

            // Count inversions in the left subarray
            invCount += mergeSortAndCount(arr, tempArr, left, mid);

            // Count inversions in the right subarray
            invCount += mergeSortAndCount(arr, tempArr, mid + 1, right);

            // Count cross inversions and merge the two halves
            invCount += mergeAndCount(arr, tempArr, left, mid, right);
        }
        return invCount;
    }

    // Function to merge two sorted subarrays and count inversions
    static int mergeAndCount(int[] arr, int[] tempArr, int left, int mid, int right) {
        int i = left;    // Starting index for left subarray
        int j = mid + 1; // Starting index for right subarray
        int k = left;    // Starting index to store sorted elements in temp array
        int invCount = 0;

        // Traverse both subarrays
        while (i <= mid && j <= right) {
            if (arr[i] <= arr[j]) {
                tempArr[k++] = arr[i++];
            } else {
                // There are (mid - i + 1) inversions because all remaining elements
                // in the left subarray are greater than arr[j]
                tempArr[k++] = arr[j++];
                invCount += (mid - i + 1);
            }
        }

        // Copy remaining elements of the left subarray
        while (i <= mid) {
            tempArr[k++] = arr[i++];
        }

        // Copy remaining elements of the right subarray
        while (j <= right) {
            tempArr[k++] = arr[j++];
        }

        // Copy sorted subarray back into the original array
        for (i = left; i <= right; i++) {
            arr[i] = tempArr[i];
        }

        return invCount;
    }
}


```



Let’s perform a **dry run** of the given implementation for an array `arr = {2, 4, 1, 3, 5}` to understand how the inversion count is calculated. 

---

### Initial Setup:
- **Input Array:** `arr = {2, 4, 1, 3, 5}`
- **Temporary Array:** `tempArr = {0, 0, 0, 0, 0}`
- **Inversions:** Initially `invCount = 0`.

---

### Step-by-Step Execution:

#### **Step 1:** Initial Call
- Call `mergeSortAndCount(arr, tempArr, 0, 4)`.
- `mid = (0 + 4) / 2 = 2`.

#### **Step 2:** Divide into Left Half
- Call `mergeSortAndCount(arr, tempArr, 0, 2)`.
- `mid = (0 + 2) / 2 = 1`.

#### **Step 3:** Further Divide Left Half
- Call `mergeSortAndCount(arr, tempArr, 0, 1)`.
- `mid = (0 + 1) / 2 = 0`.

#### **Step 4:** Base Case Reached
- Call `mergeSortAndCount(arr, tempArr, 0, 0)`. Return `0` since `left == right`.
- Call `mergeSortAndCount(arr, tempArr, 1, 1)`. Return `0`.

#### **Step 5:** Merge Left Subarray `[2]` and `[4]`
- Call `mergeAndCount(arr, tempArr, 0, 0, 1)`.
  - Compare `2 <= 4`. No inversion. Add `2` to `tempArr`.
  - Add `4` to `tempArr` since `j > right`.
- `tempArr = {2, 4, 0, 0, 0}`. Copy to `arr`.
- **Inversions:** `0`.

---

#### **Step 6:** Handle Right Subarray `[1]`
- Call `mergeSortAndCount(arr, tempArr, 2, 2)`. Return `0`.

#### **Step 7:** Merge `[2, 4]` and `[1]`
- Call `mergeAndCount(arr, tempArr, 0, 1, 2)`.
  - Compare `2 > 1`. Add `1` to `tempArr` and count `2 inversions` (`mid - i + 1 = 2`).
  - Add `2` and `4` to `tempArr` since `j > right`.
- `tempArr = {1, 2, 4, 0, 0}`. Copy to `arr`.
- **Inversions:** `2`.

---

#### **Step 8:** Divide Right Half `[3, 5]`
- Call `mergeSortAndCount(arr, tempArr, 3, 4)`.
- `mid = (3 + 4) / 2 = 3`.

#### **Step 9:** Base Case for Right Half
- Call `mergeSortAndCount(arr, tempArr, 3, 3)`. Return `0`.
- Call `mergeSortAndCount(arr, tempArr, 4, 4)`. Return `0`.

#### **Step 10:** Merge `[3]` and `[5]`
- Call `mergeAndCount(arr, tempArr, 3, 3, 4)`.
  - Compare `3 <= 5`. No inversion. Add `3` to `tempArr`.
  - Add `5` to `tempArr` since `j > right`.
- `tempArr = {1, 2, 4, 3, 5}`. Copy to `arr`.
- **Inversions:** `0`.

---

#### **Step 11:** Final Merge `[1, 2, 4]` and `[3, 5]`
- Call `mergeAndCount(arr, tempArr, 0, 2, 4)`.
  - Compare `1 <= 3`. No inversion. Add `1` to `tempArr`.
  - Compare `2 <= 3`. No inversion. Add `2` to `tempArr`.
  - Compare `4 > 3`. Add `3` to `tempArr` and count `1 inversion`.
  - Add `4` and `5` to `tempArr` since `j > right`.
- `tempArr = {1, 2, 3, 4, 5}`. Copy to `arr`.
- **Inversions:** `1`.

---

### Total Inversions:
Summing up all inversions:
- **Left Half:** `2`
- **Right Half:** `0`
- **Cross Inversions:** `1`
- **Total Inversions:** `2 + 0 + 1 = 3`.

---

### Final Array:
- `arr = {1, 2, 3, 4, 5}` (sorted).
- **Output:** `3`. 

This matches the expected result.
