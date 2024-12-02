# java
```java
class Solution {
    // Function to find the smallest positive number missing from the array.
    public int missingNumber(int[] arr) {
        int n = arr.length;

        // Step 1: Segregate positive and non-positive numbers
        int j = 0;
        for (int i = 0; i < n; i++) {
            if (arr[i] <= 0) {
                // Swap non-positive number to the front
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
                j++;
            }
        }

        // Step 2: Work only on the positive part of the array
        int[] positiveArr = arr; // Alias for clarity
        int size = n - j; // Size of the positive subarray
        for (int i = j; i < n; i++) {
            int val = Math.abs(positiveArr[i]);
            if (val - 1 < size && positiveArr[j + val - 1] > 0) {
                // Mark as visited by making the value negative
                positiveArr[j + val - 1] = -positiveArr[j + val - 1];
            }
        }

        // Step 3: Find the first positive index in the positive subarray
        for (int i = j; i < n; i++) {
            if (positiveArr[i] > 0) {
                return i - j + 1;
            }
        }

        // If all indices are marked, return size + 1
        return size + 1;
    }
}

```


Let's perform a **dry run** for the given `missingNumber` method with the array:

### Input:
`arr = [2, -3, 4, 1, 1, 7]`

---

### **Step-by-Step Execution:**

#### Initial Array:
`arr = [2, -3, 4, 1, 1, 7]`

#### Step 1: Segregate Positive and Non-Positive Numbers
- Move all non-positive numbers (≤ 0) to the front, using a swapping approach.
- Iteration details:
  - \( i = 0 \): `arr[0] = 2` (positive), no swap, \( j = 0 \).
  - \( i = 1 \): `arr[1] = -3` (non-positive), swap with `arr[0]`:
    - After swap: `arr = [-3, 2, 4, 1, 1, 7]`, \( j = 1 \).
  - \( i = 2 \): `arr[2] = 4` (positive), no swap, \( j = 1 \).
  - \( i = 3 \): `arr[3] = 1` (positive), no swap, \( j = 1 \).
  - \( i = 4 \): `arr[4] = 1` (positive), no swap, \( j = 1 \).
  - \( i = 5 \): `arr[5] = 7` (positive), no swap, \( j = 1 \).

After segregation:
`arr = [-3, 2, 4, 1, 1, 7]`, \( j = 1 \) (positive numbers start from index 1).

---

#### Step 2: Mark Presence of Elements
- Focus only on the positive part of the array: `[2, 4, 1, 1, 7]` (from \( j = 1 \)).
- Mark indices corresponding to the values as negative:
  - \( i = 1 \): `val = abs(arr[1]) = 2`. Mark \( j + val - 1 = 2 \):
    - `arr[2] = -arr[2]`.
    - `arr = [-3, 2, -4, 1, 1, 7]`.
  - \( i = 2 \): `val = abs(arr[2]) = 4`. Mark \( j + val - 1 = 4 \):
    - `arr[4] = -arr[4]`.
    - `arr = [-3, 2, -4, 1, -1, 7]`.
  - \( i = 3 \): `val = abs(arr[3]) = 1`. Mark \( j + val - 1 = 1 \):
    - `arr[1] = -arr[1]`.
    - `arr = [-3, -2, -4, 1, -1, 7]`.
  - \( i = 4 \): `val = abs(arr[4]) = 1`. Already marked, no changes.
  - \( i = 5 \): `val = abs(arr[5]) = 7`. Out of range (\( val - 1 \geq size \)), ignore.

After marking:
`arr = [-3, -2, -4, 1, -1, 7]`.

---

#### Step 3: Find the First Missing Positive Number
- Traverse the positive subarray (`arr[j..n-1] = [-2, -4, 1, -1, 7]`):
  - \( i = 1 \): `arr[1] = -2` (negative), skip.
  - \( i = 2 \): `arr[2] = -4` (negative), skip.
  - \( i = 3 \): `arr[3] = 1` (positive), **missing number = \( 3 - j + 1 = 3 \)**.

---

### Output:
**Missing Number = 3**

---

### Summary:
- Segregation step separates non-positive numbers.
- Marking step identifies present numbers using indices.
- Traversal finds the first missing positive number effectively.