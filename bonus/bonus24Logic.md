Here is the Java implementation to find the minimum number of operations required to make a matrix beautiful:

```java
class Solution {
    public static int findMinOperation(int[][] mat) {
        int n = mat.length;
        int[] rowSum = new int[n];
        int[] colSum = new int[n];
        int maxSum = 0;

        // Calculate row sums and column sums
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                rowSum[i] += mat[i][j];
                colSum[j] += mat[i][j];
            }
        }

        // Find the maximum sum among all rows and columns
        for (int i = 0; i < n; i++) {
            maxSum = Math.max(maxSum, rowSum[i]);
            maxSum = Math.max(maxSum, colSum[i]);
        }

        // Calculate the total operations needed
        int operations = 0;
        for (int i = 0; i < n; i++) {
            operations += maxSum - rowSum[i];
        }

        return operations;
    }
}
```

---

### Explanation:
1. **Key Observations**:
   - A "beautiful matrix" has all rows and columns with the same sum.
   - The maximum sum of any row or column in the matrix becomes the target sum for all rows and columns.

2. **Steps**:
   - Calculate the sum of each row and column.
   - Find the maximum value among these sums, which will be the target sum (`maxSum`).
   - For each row, calculate the difference between `maxSum` and the current row sum, and add it to the operations count.

3. **Complexity**:
   - **Time Complexity**: \(O(n^2)\), as we iterate over all cells of the matrix.
   - **Space Complexity**: \(O(n)\), for storing row and column sums.

---

### Example Usage:

```java
public class Main {
    public static void main(String[] args) {
        int[][] mat1 = {
            {1, 2},
            {3, 4}
        };
        System.out.println(Solution.findMinOperation(mat1)); // Output: 4

        int[][] mat2 = {
            {1, 2, 3},
            {4, 2, 3},
            {3, 2, 1}
        };
        System.out.println(Solution.findMinOperation(mat2)); // Output: 6

        int[][] mat3 = {
            {0, 2},
            {3, 4}
        };
        System.out.println(Solution.findMinOperation(mat3)); // Output: 5
    }
}
```

---

### Example Outputs:

**Input**:
```java
mat1 = [[1, 2], [3, 4]];
mat2 = [[1, 2, 3], [4, 2, 3], [3, 2, 1]];
mat3 = [[0, 2], [3, 4]];
```

**Output**:
```
4
6
5
```

This solution efficiently calculates the minimum operations while adhering to the problem constraints.