### Code Explanation:
# java


Here’s the implementation for the `maxOnes` function in Java using the **sliding window technique**:

```java
class Solution {
    // Function to find the maximum number of consecutive 1's
    public int maxOnes(int arr[], int k) {
        int left = 0; // Left pointer of the window
        int maxLength = 0; // To store the maximum length of the subarray
        int zeroCount = 0; // To count the number of zeros in the current window

        // Traverse the array with the right pointer
        for (int right = 0; right < arr.length; right++) {
            // If the current element is 0, increment zeroCount
            if (arr[right] == 0) {
                zeroCount++;
            }

            // If zeroCount exceeds k, shrink the window from the left
            while (zeroCount > k) {
                if (arr[left] == 0) {
                    zeroCount--;
                }
                left++; // Move the left pointer
            }

            // Update the maximum length of the subarray
            maxLength = Math.max(maxLength, right - left + 1);
        }

        return maxLength; // Return the maximum length
    }

    // Test cases
    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.maxOnes(new int[]{1, 0, 1}, 1)); // Output: 3
        System.out.println(sol.maxOnes(new int[]{1, 0, 0, 1, 0, 1, 0, 1}, 2)); // Output: 5
        System.out.println(sol.maxOnes(new int[]{1, 1}, 2)); // Output: 2
    }
}
```

---

### Explanation of Code:

1. **Initialization**:
   - `left`: Start of the sliding window.
   - `maxLength`: Tracks the maximum number of consecutive 1's.
   - `zeroCount`: Keeps track of the number of 0's in the current window.

2. **Expanding the Window**:
   - Traverse the array using the `right` pointer.
   - If the current element is `0`, increment `zeroCount`.

3. **Shrinking the Window**:
   - If `zeroCount > k`, move the `left` pointer forward to maintain at most `k` zeros in the window.
   - If the element at `left` is `0`, decrement `zeroCount`.

4. **Updating Maximum Length**:
   - For each valid window (with at most `k` zeros), calculate the window size as `right - left + 1`.
   - Update `maxLength` with the larger value.

---

### Complexity Analysis:

1. **Time Complexity**: \(O(n)\)
   - Each element is visited at most twice (once by the `right` pointer and once by the `left` pointer).

2. **Space Complexity**: \(O(1)\)
   - Uses only constant extra space for variables.

---

### Example Dry Run:

#### Input:
```plaintext
arr = [1, 0, 0, 1, 0, 1, 0, 1], k = 2
```

#### Execution:

| **Step** | `right` | `arr[right]` | `zeroCount` | `left` | Window | `maxLength` |
|----------|---------|--------------|-------------|--------|--------|-------------|
| Start    |         |              | 0           | 0      |        | 0           |
| Step 1   | 0       | 1            | 0           | 0      | [1]    | 1           |
| Step 2   | 1       | 0            | 1           | 0      | [1,0]  | 2           |
| Step 3   | 2       | 0            | 2           | 0      | [1,0,0]| 3           |
| Step 4   | 3       | 1            | 2           | 0      | [1,0,0,1]| 4         |
| Step 5   | 4       | 0            | 3           | 1      | [0,0,1,0]| 4         |
| Step 6   | 5       | 1            | 2           | 1      | [0,1,0,1]| 4         |
| Step 7   | 6       | 0            | 3           | 3      | [1,0,1,0]| 4         |
| Step 8   | 7       | 1            | 2           | 3      | [1,0,1,0,1]| **5**   |

**Output**: `5`.