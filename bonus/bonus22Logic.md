Here’s the Java code to create a spiral matrix of size \( n \times m \) using the given array:

```java
class Solution {
    public int[][] spiralFill(int n, int m, int[] arr) {
        int[][] matrix = new int[n][m];
        int top = 0, bottom = n - 1, left = 0, right = m - 1;
        int index = 0;

        while (top <= bottom && left <= right) {
            // Fill top row
            for (int i = left; i <= right; i++) {
                matrix[top][i] = arr[index++];
            }
            top++;

            // Fill right column
            for (int i = top; i <= bottom; i++) {
                matrix[i][right] = arr[index++];
            }
            right--;

            // Fill bottom row if still within bounds
            if (top <= bottom) {
                for (int i = right; i >= left; i--) {
                    matrix[bottom][i] = arr[index++];
                }
                bottom--;
            }

            // Fill left column if still within bounds
            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    matrix[i][left] = arr[index++];
                }
                left++;
            }
        }

        return matrix;
    }
}

```

---

### Explanation:
1. **Matrix Pointers**:
   - `top`: Points to the current top row.
   - `bottom`: Points to the current bottom row.
   - `left`: Points to the current left column.
   - `right`: Points to the current right column.

2. **Logic**:
   - Traverse the matrix in a spiral order:
     - Fill the top row from left to right.
     - Fill the right column from top to bottom.
     - Fill the bottom row from right to left (if the current layer still exists).
     - Fill the left column from bottom to top (if the current layer still exists).
   - Adjust the pointers (`top`, `bottom`, `left`, `right`) after each layer is filled.

3. **Edge Cases**:
   - Works for both rectangular and square matrices.

4. **Time Complexity**:
   - \(O(n \times m)\), as every element is visited once.

5. **Space Complexity**:
   - \(O(1)\) additional space, apart from the result matrix.

---

### Example Usage:

```java
public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();

        int n1 = 4, m1 = 4;
        int[] arr1 = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16};
        printMatrix(sol.spiralFill(n1, m1, arr1));

        int n2 = 3, m2 = 4;
        int[] arr2 = {1, 8, 6, 3, 8, 6, 1, 6, 3, 2, 5, 3};
        printMatrix(sol.spiralFill(n2, m2, arr2));

        int n3 = 2, m3 = 2;
        int[] arr3 = {1, 8, 6, 3};
        printMatrix(sol.spiralFill(n3, m3, arr3));
    }

    private static void printMatrix(int[][] matrix) {
        for (int[] row : matrix) {
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
n1 = 4, m1 = 4, arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16];
n2 = 3, m2 = 4, arr2 = [1, 8, 6, 3, 8, 6, 1, 6, 3, 2, 5, 3];
n3 = 2, m3 = 2, arr3 = [1, 8, 6, 3];
```

**Output**:
```
1 2 3 4 
12 13 14 5 
11 16 15 6 
10 9 8 7 

1 8 6 3 
2 5 3 8 
3 6 1 6 

1 8 
3 6 
``` 

This implementation is efficient and adheres to the constraints.