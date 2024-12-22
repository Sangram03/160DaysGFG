To solve this problem efficiently, we can leverage the sorted property of the matrix. Here's a common approach called the **staircase search**, which has a time complexity of \(O(n + m)\):

### Algorithm:
1. Start from the top-right corner of the matrix.
2. Compare the current element with \(x\):
   - If the current element equals \(x\), return `true`.
   - If the current element is greater than \(x\), move left (decrement column index).
   - If the current element is smaller than \(x\), move down (increment row index).
3. If you go out of bounds, return `false`.

This works because the rows and columns are sorted, allowing you to eliminate either a row or a column at each step.

### Implementation in Java:
Here’s the implementation of the `matSearch` method:

```java
class Solution {
    public static boolean matSearch(int mat[][], int x) {
        // Get the dimensions of the matrix
        int n = mat.length;
        int m = mat[0].length;

        // Start from the top-right corner
        int i = 0, j = m - 1;

        // Traverse the matrix
        while (i < n && j >= 0) {
            if (mat[i][j] == x) {
                return true; // Element found
            } else if (mat[i][j] > x) {
                j--; // Move left
            } else {
                i++; // Move down
            }
        }

        return false; // Element not found
    }
}
```

### Explanation of the Code:
- **Initialization**: Start from the top-right corner (`i = 0, j = m-1`).
- **Condition**: Loop while the indices are within bounds.
- **Comparison**:
  - If the element matches \(x\), return `true`.
  - If the element is larger than \(x\), move left (`j--`).
  - If the element is smaller than \(x\), move down (`i++`).
- **Out of Bounds**: If the loop ends without finding \(x\), return `false`.

### Example Execution:
#### Input:
```java
mat = {{3, 30, 38}, {20, 52, 54}, {35, 60, 69}}, x = 62
```
- Start at \(mat[0][2] = 38\):
  - \(38 < 62\): Move down.
- \(mat[1][2] = 54\):
  - \(54 < 62\): Move down.
- \(mat[2][2] = 69\):
  - \(69 > 62\): Move left.
- \(mat[2][1] = 60\):
  - \(60 < 62\): Move down (out of bounds).
- Return `false`.

#### Input:
```java
mat = {{18, 21, 27}, {38, 55, 67}}, x = 55
```
- Start at \(mat[0][2] = 27\):
  - \(27 < 55\): Move down.
- \(mat[1][2] = 67\):
  - \(67 > 55\): Move left.
- \(mat[1][1] = 55\):
  - \(55 == 55\): Return `true`.

### Time Complexity:
- **Traversal**: Each step eliminates a row or a column, so there are at most \(n + m\) steps.
- Total complexity: \(O(n + m)\).

### Space Complexity:
- \(O(1)\) since we use only a constant amount of extra space.

Let's perform a dry run of the given `matSearch` function to understand how it works step by step.

### **Input 1:**
```java
mat = {{3, 30, 38}, {20, 52, 54}, {35, 60, 69}}
x = 62
```

#### Steps:
1. **Initial Setup**:
   - \( n = 3 \), \( m = 3 \) (matrix dimensions).
   - Start at the top-right corner: \( i = 0 \), \( j = 2 \).
   - Current element: \( mat[0][2] = 38 \).

2. **Step 1**:
   - Compare \( mat[0][2] (38) \) with \( x (62) \).
   - \( 38 < 62 \): Move down (\( i++ \)).
   - New position: \( i = 1, j = 2 \).

3. **Step 2**:
   - Compare \( mat[1][2] (54) \) with \( x (62) \).
   - \( 54 < 62 \): Move down (\( i++ \)).
   - New position: \( i = 2, j = 2 \).

4. **Step 3**:
   - Compare \( mat[2][2] (69) \) with \( x (62) \).
   - \( 69 > 62 \): Move left (\( j-- \)).
   - New position: \( i = 2, j = 1 \).

5. **Step 4**:
   - Compare \( mat[2][1] (60) \) with \( x (62) \).
   - \( 60 < 62 \): Move down (\( i++ \)).
   - New position: \( i = 3, j = 1 \) (out of bounds).

6. **End Condition**:
   - \( i \geq n (3) \): Exit the loop.
   - Return `false` (element not found).

#### **Output**: `false`

---

### **Input 2:**
```java
mat = {{18, 21, 27}, {38, 55, 67}}
x = 55
```

#### Steps:
1. **Initial Setup**:
   - \( n = 2 \), \( m = 3 \) (matrix dimensions).
   - Start at the top-right corner: \( i = 0 \), \( j = 2 \).
   - Current element: \( mat[0][2] = 27 \).

2. **Step 1**:
   - Compare \( mat[0][2] (27) \) with \( x (55) \).
   - \( 27 < 55 \): Move down (\( i++ \)).
   - New position: \( i = 1, j = 2 \).

3. **Step 2**:
   - Compare \( mat[1][2] (67) \) with \( x (55) \).
   - \( 67 > 55 \): Move left (\( j-- \)).
   - New position: \( i = 1, j = 1 \).

4. **Step 3**:
   - Compare \( mat[1][1] (55) \) with \( x (55) \).
   - \( 55 == 55 \): Return `true`.

#### **Output**: `true`

---

### **Input 3:**
```java
mat = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}
x = 3
```

#### Steps:
1. **Initial Setup**:
   - \( n = 3 \), \( m = 3 \) (matrix dimensions).
   - Start at the top-right corner: \( i = 0 \), \( j = 2 \).
   - Current element: \( mat[0][2] = 3 \).

2. **Step 1**:
   - Compare \( mat[0][2] (3) \) with \( x (3) \).
   - \( 3 == 3 \): Return `true`.

#### **Output**: `true`

---

### Summary:
1. For \( x = 62 \): Output is `false`.
2. For \( x = 55 \): Output is `true`.
3. For \( x = 3 \): Output is `true`.

