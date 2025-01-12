### Approach:

The problem is to count the number of possible triangles that can be formed using three different elements of an array as sides, based on the triangle inequality rule:
1. **Triangle Inequality Rule**: The sum of any two sides of a triangle must be greater than the third side.

Since the array is not necessarily sorted, we first sort it. Once sorted, we use a **Two-Pointer Technique** combined with a loop to efficiently count the valid triangles.

---

### Steps:

1. **Sort the Array**:
   - Sorting ensures that we can easily check the triangle condition by fixing one side as the largest side (let's say `arr[i]`) and using two pointers for the other two sides.

2. **Fix the Largest Side**:
   - Iterate through the array from the end (as the largest side is easier to handle in sorted order).

3. **Use Two-Pointer Technique**:
   - For each fixed side (`arr[i]`), use two pointers (`l` and `r`) to iterate through the remaining smaller elements:
     - Start with `l = 0` (leftmost side) and `r = i - 1` (side just before `arr[i]`).
     - If the sum of the two sides (`arr[l] + arr[r]`) is greater than the fixed largest side (`arr[i]`), all pairs between `l` and `r` are valid (because the array is sorted). Count these pairs and decrement `r`.
     - If the sum is not greater, increment `l`.

4. **Return the Total Count**:
   - Sum up all the valid triangles across iterations and return the total count.

---

### Implementation:

```java
class Solution {
    static int countTriangles(int[] arr) {
        // Step 1: Sort the array
        Arrays.sort(arr);
        int count = 0, n = arr.length;

        // Step 2: Fix the largest side (arr[i])
        for (int i = n - 1; i >= 2; --i) {
            int l = 0, r = i - 1;

            // Step 3: Use two-pointer technique for smaller sides
            while (l < r) {
                if (arr[l] + arr[r] > arr[i]) {
                    // All pairs from l to r are valid
                    count += (r - l);
                    r--; // Decrease right pointer
                } else {
                    l++; // Increase left pointer
                }
            }
        }

        // Step 4: Return the total count
        return count;
    }
}
```

---

### Dry Run:

#### Example 1:
**Input**: `arr[] = [4, 6, 3, 7]`

**Sorted Array**: `[3, 4, 6, 7]`

**Steps**:
1. Fix `arr[i] = 7` (`i = 3`), `l = 0`, `r = 2`:
   - `arr[l] + arr[r] = 3 + 6 = 9 > 7` → Count = 2 (`[3, 6, 7]`, `[4, 6, 7]`), decrement `r → 1`.
   - `arr[l] + arr[r] = 3 + 4 = 7 ≤ 7` → Increment `l → 1`.
2. Fix `arr[i] = 6` (`i = 2`), `l = 0`, `r = 1`:
   - `arr[l] + arr[r] = 3 + 4 = 7 > 6` → Count = 3 (`[3, 4, 6]`), decrement `r → 0`.

**Output**: `3`

---

#### Example 2:
**Input**: `arr[] = [10, 21, 22, 100, 101, 200, 300]`

**Sorted Array**: `[10, 21, 22, 100, 101, 200, 300]`

**Steps**:
1. Fix `arr[i] = 300` (`i = 6`), `l = 0`, `r = 5`:
   - `arr[l] + arr[r] = 10 + 200 = 210 ≤ 300` → Increment `l → 1`.
   - ...
2. Repeat similar steps for all `i` values.

**Output**: `6`

---

### Complexity Analysis:

1. **Time Complexity**:
   - Sorting the array: \(O(n \log n)\)
   - Outer loop (fixing the largest side): \(O(n)\)
   - Two-pointer traversal: \(O(n)\) for each iteration of the outer loop.
   - Total: \(O(n^2)\)

2. **Space Complexity**:
   - \(O(1)\), as no extra space is used apart from variables.

---

### Advantages of This Approach:
- The sorting step ensures we only need one traversal with two pointers to check the triangle inequality efficiently.
- Handles larger constraints gracefully with \(O(n^2)\) complexity.