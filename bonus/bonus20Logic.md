Here's the Java implementation of the `minDaysBloom` method:

```java
class Solution {
    public static int minDaysBloom(int m, int k, int[] arr) {
        if ((long) m * k > arr.length) {
            return -1;
        }

        int left = 1;
        int right = getMax(arr);
        int result = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (canMakeBouquets(arr, m, k, mid)) {
                result = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return result;
    }

    private static boolean canMakeBouquets(int[] arr, int m, int k, int day) {
        int bouquets = 0;
        int flowers = 0;

        for (int bloomDay : arr) {
            if (bloomDay <= day) {
                flowers++;
                if (flowers == k) {
                    bouquets++;
                    flowers = 0;
                }
            } else {
                flowers = 0;
            }

            if (bouquets >= m) {
                return true;
            }
        }

        return false;
    }

    private static int getMax(int[] arr) {
        int max = arr[0];
        for (int num : arr) {
            max = Math.max(max, num);
        }
        return max;
    }
}

```

### Explanation:

1. **Edge Case**:
   - If \( m \times k > \text{arr.length} \), it's impossible to make \( m \) bouquets, so return \(-1\).

2. **Binary Search**:
   - The possible range of days is from \( 1 \) (minimum bloom day) to \( \text{max(arr)} \) (maximum bloom day).
   - Use binary search to find the minimum day on which \( m \) bouquets can be made.

3. **Helper Function - `canMakeBouquets`**:
   - Iterate through the array and count consecutive bloomed flowers that can form bouquets within the given `day`.
   - Reset the flower count if a flower hasn't bloomed yet (i.e., \( \text{bloomDay} > \text{day} \)).
   - If \( \text{bouquets} \geq m \), return `true`.

4. **Helper Function - `getMax`**:
   - Find the maximum bloom day in the array, which determines the upper bound for the binary search.

### Complexity:
- **Time Complexity**:
  - \( O(n \log(\text{max(arr)})) \): Binary search over bloom days (\( \log(\text{max(arr)}) \)) and iterating through the array (\( O(n) \)) to count bouquets.
- **Space Complexity**: \( O(1) \), as no extra space is used.

### Examples:
1. **Input**: `m = 3, k = 2, arr = [3, 4, 2, 7, 13, 8, 5]`
   - **Output**: `8`

2. **Input**: `m = 2, k = 3, arr = [5, 5, 5, 5, 10, 5, 5]`
   - **Output**: `10`

3. **Input**: `m = 3, k = 2, arr = [1, 10, 3, 10, 2]`
   - **Output**: `-1`