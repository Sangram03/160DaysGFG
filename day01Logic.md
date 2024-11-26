The provided code snippet is for finding the second largest element in an array. Here's a detailed explanation of how it works:

---

### Code Explanation:
# java
```java
class Solution {
    public int getSecondLargest(int[] arr) {
        int first = Integer.MIN_VALUE; // To store the largest element
        int second = Integer.MIN_VALUE; // To store the second largest element

        for (int num : arr) { // Iterate through the array
            if (num > first) { // If the current number is greater than the largest
                second = first; // Update second largest
                first = num; // Update largest
            } else if (num > second && num < first) { // If the current number is between first and second
                second = num; // Update second largest
            }
        }
        
        // If second largest doesn't exist, return -1
        return second == Integer.MIN_VALUE ? -1 : second;
    }
}
```

---

### Key Points:
1. **Initialization:**
   - Both `first` and `second` are initialized to `Integer.MIN_VALUE`, which is the smallest possible integer value in Java.
   - This ensures that even if all array elements are negative, the logic remains valid.

2. **First Condition (`if (num > first)`):**
   - If the current number is greater than the largest number (`first`), update `second` to the value of `first` and then update `first` to the current number.

3. **Second Condition (`else if (num > second && num < first)`):**
   - If the current number is smaller than `first` but greater than `second`, update `second`.

4. **Edge Case Handling:**
   - If the array contains all identical numbers or has only one distinct element, `second` will remain `Integer.MIN_VALUE`.
   - In such cases, the method returns `-1`.

---

### Example Walkthrough:

#### Input:
```java
int[] arr = {3, 1, 4, 4, 5, 2};
```

#### Execution:
- Initial `first = Integer.MIN_VALUE`, `second = Integer.MIN_VALUE`.
- Iterate over the array:
  - `num = 3`: Update `first = 3`, `second = Integer.MIN_VALUE`.
  - `num = 1`: No change (`1 < first` and `1 < second`).
  - `num = 4`: Update `first = 4`, `second = 3`.
  - `num = 4`: No change (`4 == first`).
  - `num = 5`: Update `first = 5`, `second = 4`.
  - `num = 2`: No change (`2 < second`).

Final values: `first = 5`, `second = 4`.

#### Output:
```plaintext
4
```

---

### Complexity Analysis:
1. **Time Complexity:** \( O(n) \)
   - The loop iterates through the array once.
2. **Space Complexity:** \( O(1) \)
   - No extra space is used apart from a few variables.

---

### Edge Cases:
1. **Single Element:**
   ```java
   int[] arr = {10};
   System.out.println(sol.getSecondLargest(arr)); // Output: -1
   ```

2. **All Identical Elements:**
   ```java
   int[] arr = {5, 5, 5, 5};
   System.out.println(sol.getSecondLargest(arr)); // Output: -1
   ```

3. **Negative Numbers:**
   ```java
   int[] arr = {-3, -1, -4, -2};
   System.out.println(sol.getSecondLargest(arr)); // Output: -2
   ```

The implementation is concise, efficient, and robust for a wide range of input cases.