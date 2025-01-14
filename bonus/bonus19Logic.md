Here is the Java implementation of the `kokoEat` method:

### Code:
```java
class Solution {
    public static int kokoEat(int[] arr, int k) {
        int left = 1; // Minimum eating speed
        int right = getMax(arr); // Maximum eating speed
        int result = right;

        // Binary search for the minimum eating speed
        while (left <= right) {
            int mid = left + (right - left) / 2;

            // Check if Koko can finish at this speed
            if (canFinish(arr, mid, k)) {
                result = mid; // Update result
                right = mid - 1; // Try for a smaller speed
            } else {
                left = mid + 1; // Try for a larger speed
            }
        }

        return result;
    }

    // Function to check if Koko can finish eating at speed `speed` in `k` hours
    private static boolean canFinish(int[] arr, int speed, int k) {
        int hoursNeeded = 0;

        for (int bananas : arr) {
            hoursNeeded += Math.ceil((double) bananas / speed);
            if (hoursNeeded > k) {
                return false; // Too many hours needed
            }
        }

        return true;
    }

    // Helper function to find the maximum element in the array
    private static int getMax(int[] arr) {
        int max = arr[0];
        for (int bananas : arr) {
            max = Math.max(max, bananas);
        }
        return max;
    }
}
```

### Explanation:
1. **Binary Search**:
   - The search space for the eating speed ranges from 1 (minimum) to the maximum pile size in the array.
   - Use binary search to narrow down the minimum speed `s` that allows Koko to finish all piles within `k` hours.

2. **Helper Functions**:
   - `canFinish`: Checks if Koko can finish all piles at a given speed `s` within `k` hours.
     - For each pile, calculate the hours needed as \( \text{ceil}(\text{pile size} / \text{speed}) \).
     - Accumulate the total hours and compare with `k`.
   - `getMax`: Returns the maximum element in the array, which serves as the upper bound of the search.

3. **Update Result**:
   - If `canFinish` is true for a mid-speed, update the result and continue searching for a smaller speed.

4. **Terminate**:
   - When `left > right`, the smallest valid speed is stored in `result`.

### Complexity:
- **Time Complexity**:
  - \(O(n \log m)\), where \(n\) is the size of the array, and \(m\) is the maximum pile size. Each iteration of binary search requires \(O(n)\) to check feasibility.
- **Space Complexity**: \(O(1)\), as no extra space is used.

### Examples:
1. **Input**: `arr = [3, 6, 7, 11]`, `k = 8`
   - Output: `4`

2. **Input**: `arr = [30, 11, 23, 4, 20]`, `k = 5`
   - Output: `30`

3. **Input**: `arr = [5, 10, 15, 20]`, `k = 7`
   - Output: `10`