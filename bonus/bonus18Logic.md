Here is the Java implementation of the `floorSqrt` method:

### Code:
```java
class Solution {
    int floorSqrt(int n) {
        if (n == 0 || n == 1) {
            return n;
        }

        int left = 1, right = n, ans = 0;

        // Binary search for floor of square root
        while (left <= right) {
            int mid = left + (right - left) / 2;

            // Check if mid*mid equals n
            if (mid <= n / mid) {
                ans = mid; // Store the current result
                left = mid + 1; // Move to the right half
            } else {
                right = mid - 1; // Move to the left half
            }
        }

        return ans;
    }
}
```

### Explanation:
1. **Base Cases**:
   - If `n` is 0 or 1, its square root is itself.

2. **Binary Search**:
   - We use binary search to find the floor of the square root.
   - Define the search space between 1 and \(n\).
   - Calculate `mid` and check if \( \text{mid}^2 \leq n \).
   - If true, update `ans` to `mid` and move the left pointer to `mid + 1`.
   - If false, move the right pointer to `mid - 1`.

3. **Final Result**:
   - The variable `ans` stores the floor value of the square root.

### Complexity:
- **Time Complexity**: \(O(\log n)\), because binary search halves the search space at each step.
- **Space Complexity**: \(O(1)\), as no extra space is used.

### Examples:
1. **Input**: `n = 4`
   - Output: `2`

2. **Input**: `n = 11`
   - Output: `3`

3. **Input**: `n = 1`
   - Output: `1`.