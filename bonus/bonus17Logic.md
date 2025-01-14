Here's the Java implementation to find the median of two sorted arrays of different sizes:

### Code:
```java
class Solution {
    public double medianOf2(int a[], int b[]) {
        // Ensure the first array is smaller or equal in size to the second array
        if (a.length > b.length) {
            return medianOf2(b, a);
        }

        int x = a.length;
        int y = b.length;
        int low = 0, high = x;

        while (low <= high) {
            int partitionX = (low + high) / 2;
            int partitionY = (x + y + 1) / 2 - partitionX;

            int maxX = (partitionX == 0) ? Integer.MIN_VALUE : a[partitionX - 1];
            int minX = (partitionX == x) ? Integer.MAX_VALUE : a[partitionX];

            int maxY = (partitionY == 0) ? Integer.MIN_VALUE : b[partitionY - 1];
            int minY = (partitionY == y) ? Integer.MAX_VALUE : b[partitionY];

            if (maxX <= minY && maxY <= minX) {
                // Found the correct partition
                if ((x + y) % 2 == 0) {
                    return ((double)Math.max(maxX, maxY) + Math.min(minX, minY)) / 2;
                } else {
                    return (double)Math.max(maxX, maxY);
                }
            } else if (maxX > minY) {
                // Move left in array a
                high = partitionX - 1;
            } else {
                // Move right in array a
                low = partitionX + 1;
            }
        }

        throw new IllegalArgumentException("Input arrays are not sorted");
    }
}
```

### Explanation:
1. **Binary Search on the Smaller Array**:
   - The solution uses binary search on the smaller array to partition both arrays at a point where the left side contains half the elements of the combined array.

2. **Partitioning**:
   - `partitionA`: Number of elements in the left partition of array `a`.
   - `partitionB`: Number of elements in the left partition of array `b`.
   - `maxLeftA` and `minRightA` represent the maximum and minimum elements on either side of the partition in `a`.
   - `maxLeftB` and `minRightB` do the same for `b`.

3. **Median Calculation**:
   - If the total number of elements is odd, the median is the maximum of the left partition.
   - If even, the median is the average of the maximum of the left partition and the minimum of the right partition.

4. **Edge Cases**:
   - Empty arrays are handled using `Integer.MIN_VALUE` and `Integer.MAX_VALUE`.

### Complexity:
- **Time Complexity**: \(O(\log \min(m, n))\), where \(m\) and \(n\) are the sizes of arrays `a` and `b`.
- **Space Complexity**: \(O(1)\), as no extra space is used.

### Examples:
1. **Input**: `a = [-5, 3, 6, 12, 15]`, `b = [-12, -10, -6, -3, 4, 10]`
   - Output: `3.0`

2. **Input**: `a = [2, 3, 5, 8]`, `b = [10, 12, 14, 16, 18, 20]`
   - Output: `11.0`

3. **Input**: `a = []`, `b = [2, 4, 5, 6]`
   - Output: `4.5`