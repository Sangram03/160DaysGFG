Here's the implementation of the `findMaximum` method in Java:

```java
class Solution {
    public int findMaximum(int[] arr) {
        int left = 0, right = arr.length - 1;

        // Perform binary search
        while (left < right) {
            int mid = left + (right - left) / 2;

            // Compare mid with mid + 1
            if (arr[mid] > arr[mid + 1]) {
                // Move towards the decreasing part
                right = mid;
            } else {
                // Move towards the increasing part
                left = mid + 1;
            }
        }

        // `left` or `right` points to the bitonic point
        return arr[left];
    }
}
```

### Explanation:
1. **Binary Search**:
   - Start with the entire array (`left = 0` and `right = arr.length - 1`).
   - Use `mid = left + (right - left) / 2` to calculate the middle index.
   
2. **Comparison**:
   - If `arr[mid] > arr[mid + 1]`, the bitonic point is on the left or at `mid`. Set `right = mid`.
   - Otherwise, the bitonic point is on the right. Set `left = mid + 1`.

3. **Termination**:
   - When `left == right`, both pointers converge at the bitonic point.

4. **Return**:
   - The value at `arr[left]` is the maximum element in the array.

### Complexity:
- **Time Complexity**: \(O(\log n)\), where \(n\) is the size of the array.
- **Space Complexity**: \(O(1)\), as no additional space is used.

### Examples:
1. **Input**: `arr = [1, 2, 4, 5, 7, 8, 3]`
   - Output: `8`

2. **Input**: `arr = [10, 20, 30, 40, 50]`
   - Output: `50`

3. **Input**: `arr = [120, 100, 80, 20, 0]`
   - Output: `120`.