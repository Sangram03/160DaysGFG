To solve the problem, we can use the following approach:

### **Approach**
1. The missing numbers can be determined by comparing the expected sequence of numbers with the elements in the given array.
2. As we traverse the array:
   - Count the numbers that are missing (gap between the expected numbers and the actual numbers in the array).
   - Stop once the count of missing numbers reaches `k`.
3. If the end of the array is reached and we haven’t yet found the `k`th missing number, calculate it using the difference between the remaining count and the last element of the array.

### **Algorithm**
1. Initialize:
   - `missingCount = 0` to track the total missing numbers so far.
   - `current = 1` as the current number to be checked against the array.
   - `index = 0` to iterate through the array.
2. Loop until `missingCount < k`:
   - If `current` matches `arr[index]`, increment `index`.
   - Otherwise, it means `current` is missing. Increment `missingCount`.
   - Increment `current` in each iteration.
3. When `missingCount == k`, `current - 1` will be the result.

Here is the implementation in Java:

```java
class Solution {
    public int kthMissing(int[] arr, int k) {
        int missingCount = 0; // Count of missing numbers found
        int current = 1; // Current number to check
        int index = 0; // Pointer to traverse the array
        
        while (missingCount < k) {
            if (index < arr.length && arr[index] == current) {
                // If current number is in the array, move to the next element
                index++;
            } else {
                // If current number is missing
                missingCount++;
            }
            if (missingCount == k) {
                return current; // Found the kth missing number
            }
            current++;
        }
        return -1; // This will never be reached
    }
}
```

### **Complexity Analysis**
- **Time Complexity**: \( O(n + k) \)
  - The loop runs until either all elements of the array are traversed or the \( k \)th missing number is found.
- **Space Complexity**: \( O(1) \)
  - No additional data structures are used.

### **Examples**
#### Input: `arr = [2, 3, 4, 7, 11], k = 5`
- Missing numbers: \( 1, 5, 6, 8, 9, 10, \dots \)
- Output: `9`

#### Input: `arr = [1, 2, 3], k = 2`
- Missing numbers: \( 4, 5, 6, \dots \)
- Output: `5`

#### Input: `arr = [3, 5, 9, 10, 11, 12], k = 2`
- Missing numbers: \( 1, 2, 4, 6, 7, 8, \dots \)
- Output: `2`


Let’s perform a **dry run** of the solution for the given code with the input `arr = [2, 3, 4, 7, 11]` and `k = 5`.

---

### **Initial Values**
- `arr = [2, 3, 4, 7, 11]`
- `k = 5`
- `missingCount = 0`
- `current = 1`
- `index = 0`

---

### **Step-by-Step Execution**

| **Iteration** | **current** | **index** | **arr[index]** | **missingCount** | **Action**             |
|---------------|-------------|-----------|-----------------|-------------------|------------------------|
| 1             | 1           | 0         | 2               | 0                 | `current` is missing. Increment `missingCount`. |
|               |             |           |                 | 1                 | Move `current` to 2.   |
| 2             | 2           | 0         | 2               | 1                 | `current` is in `arr`. Increment `index`.       |
|               |             |           |                 |                   | Move `current` to 3.   |
| 3             | 3           | 1         | 3               | 1                 | `current` is in `arr`. Increment `index`.       |
|               |             |           |                 |                   | Move `current` to 4.   |
| 4             | 4           | 2         | 4               | 1                 | `current` is in `arr`. Increment `index`.       |
|               |             |           |                 |                   | Move `current` to 5.   |
| 5             | 5           | 3         | 7               | 1                 | `current` is missing. Increment `missingCount`. |
|               |             |           |                 | 2                 | Move `current` to 6.   |
| 6             | 6           | 3         | 7               | 2                 | `current` is missing. Increment `missingCount`. |
|               |             |           |                 | 3                 | Move `current` to 7.   |
| 7             | 7           | 3         | 7               | 3                 | `current` is in `arr`. Increment `index`.       |
|               |             |           |                 |                   | Move `current` to 8.   |
| 8             | 8           | 4         | 11              | 3                 | `current` is missing. Increment `missingCount`. |
|               |             |           |                 | 4                 | Move `current` to 9.   |
| 9             | 9           | 4         | 11              | 4                 | `current` is missing. Increment `missingCount`. |
|               |             |           |                 | 5                 | Found the `k`th missing number! Return 9.       |

---

### **Final Output**
- **Result**: `9`

---

### **Explanation**
The missing numbers in the sequence are:  
`1, 5, 6, 8, 9, 10, ...`  
The 5th missing number is `9`.

---

