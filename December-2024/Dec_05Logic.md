# java
```java


class Solution {
    // Function to sort an array of 0s, 1s, and 2s
    public void sort012(int[] arr) {
        int low = 0, mid = 0, high = arr.length - 1;

        while (mid <= high) {
            switch (arr[mid]) {
                case 0:
                    // Swap arr[low] and arr[mid], and move both pointers forward
                    int temp0 = arr[low];
                    arr[low] = arr[mid];
                    arr[mid] = temp0;
                    low++;
                    mid++;
                    break;

                case 1:
                    // Move mid pointer forward
                    mid++;
                    break;

                case 2:
                    // Swap arr[mid] and arr[high], and move high pointer backward
                    int temp2 = arr[mid];
                    arr[mid] = arr[high];
                    arr[high] = temp2;
                    high--;
                    break;
            }
        }
    }
}



```


Let's do a **dry run** of the `sort012` function using the input array `arr = {0, 1, 2, 0, 1, 2}`. We will track the values of `low`, `mid`, `high`, and the array state after each step.

---

### Initial State:
- **Input Array**: `{0, 1, 2, 0, 1, 2}`
- `low = 0`, `mid = 0`, `high = 5`

---

### Iteration 1:
- **Value at `arr[mid]`**: `0`
- Swap `arr[low]` and `arr[mid]`: No change since both are `0`.
- Increment `low` and `mid`.
- **Updated Values**:
  - `low = 1`, `mid = 1`, `high = 5`
  - **Array**: `{0, 1, 2, 0, 1, 2}`

---

### Iteration 2:
- **Value at `arr[mid]`**: `1`
- No swap, increment `mid`.
- **Updated Values**:
  - `low = 1`, `mid = 2`, `high = 5`
  - **Array**: `{0, 1, 2, 0, 1, 2}`

---

### Iteration 3:
- **Value at `arr[mid]`**: `2`
- Swap `arr[mid]` and `arr[high]`: Swap `2` with `2` (no change).
- Decrement `high`.
- **Updated Values**:
  - `low = 1`, `mid = 2`, `high = 4`
  - **Array**: `{0, 1, 2, 0, 1, 2}`

---

### Iteration 4:
- **Value at `arr[mid]`**: `2`
- Swap `arr[mid]` and `arr[high]`: Swap `2` with `1`.
- Decrement `high`.
- **Updated Values**:
  - `low = 1`, `mid = 2`, `high = 3`
  - **Array**: `{0, 1, 1, 0, 2, 2}`

---

### Iteration 5:
- **Value at `arr[mid]`**: `1`
- No swap, increment `mid`.
- **Updated Values**:
  - `low = 1`, `mid = 3`, `high = 3`
  - **Array**: `{0, 1, 1, 0, 2, 2}`

---

### Iteration 6:
- **Value at `arr[mid]`**: `0`
- Swap `arr[low]` and `arr[mid]`: Swap `1` with `0`.
- Increment `low` and `mid`.
- **Updated Values**:
  - `low = 2`, `mid = 4`, `high = 3`
  - **Array**: `{0, 0, 1, 1, 2, 2}`

---

### End of Loop:
- `mid > high`, so the loop terminates.
- **Final Array**: `{0, 0, 1, 1, 2, 2}`

---

### Output:
The array is sorted as required: **`{0, 0, 1, 1, 2, 2}`**.