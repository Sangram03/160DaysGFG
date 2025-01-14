Here's the implementation of the `lowerBound` method in Java:

```java
class Solution {
    int lowerBound(int[] arr, int target) {
        int left = 0, right = arr.length;
        
        // Perform binary search
        while (left < right) {
            int mid = left + (right - left) / 2;
            
            if (arr[mid] < target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        
        // `left` will be the smallest index where arr[left] >= target
        return left;
    }
}
```

### Explanation:
1. **Binary Search**: 
   - Start with the entire range (`left = 0` to `right = arr.length`).
   - Use `mid = left + (right - left) / 2` to avoid overflow.

2. **Condition**:
   - If `arr[mid] < target`, we know that the target must be in the right half, so we move `left` to `mid + 1`.
   - Otherwise, we narrow the search to the left half by setting `right = mid`.

3. **Result**:
   - When the loop exits, `left` is the smallest index where `arr[left] >= target`.
   - If no such index exists, `left` equals `arr.length`, which satisfies the constraints.

### Complexity:
- **Time Complexity**: \(O(\log n)\), where \(n\) is the size of the array.
- **Space Complexity**: \(O(1)\), as no additional space is used.

### Example:
1. **Input**: `arr = [2, 3, 7, 10, 11, 11, 25], target = 9`
   - Output: `3`

2. **Input**: `arr = [2, 3, 7, 10, 11, 11, 25], target = 11`
   - Output: `4`

3. **Input**: `arr = [2, 3, 7, 10, 11, 11, 25], target = 100`
   - Output: `7`