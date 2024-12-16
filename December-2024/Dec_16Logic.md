To solve this problem efficiently without explicitly merging the two arrays, we can use a binary search approach. Here's the explanation and code for the solution:

### Approach:
1. **Binary Search on the Smaller Array**:
   - Perform binary search on one of the arrays, typically the smaller one (let's call it `a`).
   - Assume that the k-th element in the merged array is split into two parts: a part from array `a` and a part from array `b`.

2. **Splitting Logic**:
   - Let `low` be 0 and `high` be `min(k, size of a)`.
   - For a given partition index `mid` in `a`, calculate the corresponding partition index in `b` as `k - mid`.

3. **Compare and Adjust**:
   - Check if `a[mid - 1]` is less than or equal to `b[k - mid]` and `b[k - mid - 1]` is less than or equal to `a[mid]`.
   - If true, then the current partition satisfies the condition.
   - If not, adjust the binary search range based on the comparison.

4. **Edge Cases**:
   - Handle cases where the partition lies completely in one array or overlaps minimally.

5. **Time Complexity**:
   - The time complexity is \(O(\log(\min(m, n)))\), where \(m\) and \(n\) are the sizes of the two arrays.

---

### Code Implementation:

```java
class Solution {
    public int kthElement(int a[], int b[], int k) {
        // Ensure 'a' is the smaller array
        if (a.length > b.length) {
            return kthElement(b, a, k);
        }
        
        int n1 = a.length;
        int n2 = b.length;
        int low = Math.max(0, k - n2); // Ensure k is valid for 'b'
        int high = Math.min(k, n1);   // Ensure k is valid for 'a'
        
        while (low <= high) {
            int midA = (low + high) / 2;
            int midB = k - midA;
            
            int leftA = (midA == 0) ? Integer.MIN_VALUE : a[midA - 1];
            int leftB = (midB == 0) ? Integer.MIN_VALUE : b[midB - 1];
            int rightA = (midA == n1) ? Integer.MAX_VALUE : a[midA];
            int rightB = (midB == n2) ? Integer.MAX_VALUE : b[midB];
            
            if (leftA <= rightB && leftB <= rightA) {
                return Math.max(leftA, leftB);
            } else if (leftA > rightB) {
                high = midA - 1; // Move left in 'a'
            } else {
                low = midA + 1; // Move right in 'a'
            }
        }
        
        return -1; // Should not reach here if inputs are valid
    }
}
```

---

### Explanation of Edge Cases:
1. If `k` lies entirely in one array:
   - The binary search adjusts `low` and `high` to find the correct partition.
2. If one array is empty:
   - The k-th element is in the other array.

This solution avoids the inefficiency of merging and works well even for large arrays.




Let’s perform a dry run for the given solution with the example:

### Input:
- `a[] = [2, 3, 6, 7, 9]`
- `b[] = [1, 4, 8, 10]`
- `k = 5`

---

### Step-by-Step Execution:

#### Initial Setup:
1. **Check array sizes**: `a.length = 5`, `b.length = 4`. Since `a.length > b.length`, call `kthElement(b, a, k)` to ensure `a` is the smaller array.

    So now:
    - `a[] = [1, 4, 8, 10]`
    - `b[] = [2, 3, 6, 7, 9]`
    - `k = 5`

2. **Variables**:
    - `n1 = 4`, `n2 = 5`
    - `low = max(0, k - n2) = max(0, 5 - 5) = 0`
    - `high = min(k, n1) = min(5, 4) = 4`

---

#### Iteration 1:
1. **Midpoints**:
   - `midA = (low + high) / 2 = (0 + 4) / 2 = 2`
   - `midB = k - midA = 5 - 2 = 3`

2. **Partition Values**:
   - `leftA = a[midA - 1] = a[1] = 4`
   - `leftB = b[midB - 1] = b[2] = 6`
   - `rightA = a[midA] = a[2] = 8`
   - `rightB = b[midB] = b[3] = 7`

3. **Conditions**:
   - `leftA <= rightB`: `4 <= 7` (True)
   - `leftB <= rightA`: `6 <= 8` (True)

   Since both conditions are satisfied, the k-th element is:
   \[
   \text{k-th element} = \max(leftA, leftB) = \max(4, 6) = 6
   \]

---

### Final Result:
- The 5th element in the combined sorted array is **6**.

---

### Explanation of Partitions:
1. **Combined Sorted Array**:  
   Merge `[1, 4, 8, 10]` and `[2, 3, 6, 7, 9]` to get:  
   \[
   [1, 2, 3, 4, 6, 7, 8, 9, 10]
   \]
2. **Partition at Iteration 1**:
   - Left partition: `[1, 2, 3, 4, 6]`
   - Right partition: `[7, 8, 9, 10]`

The k-th element (5th in 1-based indexing) is **6**, as expected.