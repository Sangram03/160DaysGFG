To rotate a square matrix by 90 degrees anti-clockwise in place without using extra space, you can follow these steps:

1. **Transpose the Matrix**: Convert rows into columns by swapping `mat[i][j]` with `mat[j][i]` for all \(i < j\).
2. **Reverse Each Column**: For every column, reverse its elements.

Here’s the Java implementation:

```java
class Solution {
    // Function to rotate matrix anticlockwise by 90 degrees.
    static void rotateby90(int mat[][]) {
        int n = mat.length;

        // Step 1: Transpose the matrix
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = mat[i][j];
                mat[i][j] = mat[j][i];
                mat[j][i] = temp;
            }
        }

        // Step 2: Reverse each column
        for (int j = 0; j < n; j++) {
            int start = 0, end = n - 1;
            while (start < end) {
                int temp = mat[start][j];
                mat[start][j] = mat[end][j];
                mat[end][j] = temp;
                start++;
                end--;
            }
        }
    }
}
```

### Explanation:

#### Input:
```plaintext
mat = [[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]]
```

#### Step 1: Transpose the matrix
Swap elements to make rows into columns:
```plaintext
mat = [[1, 4, 7],
       [2, 5, 8],
       [3, 6, 9]]
```

#### Step 2: Reverse each column
Reverse the elements in each column to rotate 90° anti-clockwise:
```plaintext
mat = [[3, 6, 9],
       [2, 5, 8],
       [1, 4, 7]]
```

### Output:
```plaintext
Rotated Matrix:
[3, 6, 9]
[2, 5, 8]
[1, 4, 7]
```

This approach has a **time complexity** of \(O(n^2)\) and uses **constant extra space** \(O(1)\), fulfilling the requirements.



Let's perform a **dry run** of the provided code using the input matrix:

### Input:
```plaintext
mat = [[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]]
```

### Step 1: Transpose the Matrix
For a transpose, swap `mat[i][j]` with `mat[j][i]` for \(i < j\).

#### Initial Matrix:
```plaintext
mat = [[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]]
```

**Loop iterations:**
1. \(i = 0, j = 1\): Swap `mat[0][1]` with `mat[1][0]`  
   Result:  
   ```plaintext
   mat = [[1, 4, 3],
          [2, 5, 6],
          [7, 8, 9]]
   ```
2. \(i = 0, j = 2\): Swap `mat[0][2]` with `mat[2][0]`  
   Result:  
   ```plaintext
   mat = [[1, 4, 7],
          [2, 5, 6],
          [3, 8, 9]]
   ```
3. \(i = 1, j = 2\): Swap `mat[1][2]` with `mat[2][1]`  
   Result:  
   ```plaintext
   mat = [[1, 4, 7],
          [2, 5, 8],
          [3, 6, 9]]
   ```

**Transposed Matrix:**
```plaintext
mat = [[1, 4, 7],
       [2, 5, 8],
       [3, 6, 9]]
```

---

### Step 2: Reverse Each Column
Reverse the elements in each column.

#### Initial Transposed Matrix:
```plaintext
mat = [[1, 4, 7],
       [2, 5, 8],
       [3, 6, 9]]
```

**Loop through each column:**
1. \(j = 0\): Reverse column 0  
   Swap `mat[0][0]` with `mat[2][0]`  
   Result:  
   ```plaintext
   mat = [[3, 4, 7],
          [2, 5, 8],
          [1, 6, 9]]
   ```
2. \(j = 1\): Reverse column 1  
   Swap `mat[0][1]` with `mat[2][1]`  
   Result:  
   ```plaintext
   mat = [[3, 6, 7],
          [2, 5, 8],
          [1, 4, 9]]
   ```
3. \(j = 2\): Reverse column 2  
   Swap `mat[0][2]` with `mat[2][2]`  
   Result:  
   ```plaintext
   mat = [[3, 6, 9],
          [2, 5, 8],
          [1, 4, 7]]
   ```

---

### Final Output:
```plaintext
Rotated Matrix:
[3, 6, 9]
[2, 5, 8]
[1, 4, 7]
```