Here's the complete Java code to rotate a square matrix by 180 degrees counterclockwise in place:

```java
class Solution {
    public void rotateMatrix(int[][] mat) {
        int n = mat.length;

        // Rotate the matrix by 180 degrees in place
        for (int i = 0; i < n / 2; i++) {
            for (int j = 0; j < n; j++) {
                // Swap elements between top and bottom rows
                int temp = mat[i][j];
                mat[i][j] = mat[n - i - 1][n - j - 1];
                mat[n - i - 1][n - j - 1] = temp;
            }
        }

        // If n is odd, reverse the middle row
        if (n % 2 != 0) {
            int middle = n / 2;
            for (int j = 0; j < n / 2; j++) {
                int temp = mat[middle][j];
                mat[middle][j] = mat[middle][n - j - 1];
                mat[middle][n - j - 1] = temp;
            }
        }
    }
}
```

### Explanation:
1. **Key Idea**:
   - To rotate a matrix by 180 degrees counterclockwise, swap each element `(i, j)` with its counterpart `(n-1-i, n-1-j)`.

2. **Optimization**:
   - We traverse only the top half of the matrix. For odd-sized matrices, the middle row swaps only halfway.

3. **Time Complexity**:
   - \(O(n^2)\), as we visit each element once.

4. **Space Complexity**:
   - \(O(1)\), as the matrix is rotated in place without using extra space.

---

### Example Usage:

```java
public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();

        int[][] mat1 = {
            {1, 2},
            {3, 4}
        };
        sol.rotateMatrix(mat1);
        printMatrix(mat1);

        int[][] mat2 = {
            {1, 2, 3, 4},
            {5, 6, 7, 8},
            {9, 10, 11, 12},
            {13, 14, 15, 16}
        };
        sol.rotateMatrix(mat2);
        printMatrix(mat2);
    }

    private static void printMatrix(int[][] mat) {
        for (int[] row : mat) {
            for (int val : row) {
                System.out.print(val + " ");
            }
            System.out.println();
        }
        System.out.println();
    }
}
```

---

### Example Output:

**Input**:
```java
mat1 = [[1, 2], [3, 4]];
mat2 = [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16]];
```

**Output**:
```
4 3 
2 1 

16 15 14 13 
12 11 10 9 
8 7 6 5 
4 3 2 1 
``` 

This implementation directly modifies the matrix as required and handles constraints efficiently.