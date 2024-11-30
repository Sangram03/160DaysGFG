### Code Explanation:
# java
```java

class Solution {

    public List<Integer> findSplit(int[] arr) {
        // Calculate the total sum of the array
        int totalSum = 0;
        for (int num : arr) {
            totalSum += num;
        }

        // If the total sum is not divisible by 3, return [-1, -1]
        if (totalSum % 3 != 0) {
            return Arrays.asList(-1, -1);
        }

        int target = totalSum / 3;
        int currentSum = 0, count = 0;
        int firstSplit = -1, secondSplit = -1;

        // Traverse the array to find the splits
        for (int i = 0; i < arr.length; i++) {
            currentSum += arr[i];

            if (currentSum == target) {
                count++;
                currentSum = 0;

                if (count == 1) {
                    firstSplit = i;
                } else if (count == 2) {
                    secondSplit = i;
                    break;
                }
            }
        }

        // If we found two splits, return them; otherwise, return [-1, -1]
        if (firstSplit != -1 && secondSplit != -1) {
            return Arrays.asList(firstSplit, secondSplit);
        }
        return Arrays.asList(-1, -1);
    }

    public static void main(String[] args) {
        Solution solution = new Solution();

        // Test cases
        System.out.println(solution.findSplit(new int[]{1, 3, 4, 0, 4})); // Output: [1, 2]
        System.out.println(solution.findSplit(new int[]{2, 3, 4}));       // Output: [-1, -1]
        System.out.println(solution.findSplit(new int[]{0, 1, 1}));       // Output: [-1, -1]
    }
}
```


Let's perform a dry run of the provided `findSplit` method for the given test cases to verify the logic.

---

### **Test Case 1: `arr = [1, 3, 4, 0, 4]`**
- **Step 1**: Calculate `totalSum`:
  - \(1 + 3 + 4 + 0 + 4 = 12\)
- **Step 2**: Check if `totalSum % 3 == 0`:
  - \(12 \mod 3 = 0\) → Valid for splitting.
- **Step 3**: Calculate `target`:
  - \( \text{target} = 12 / 3 = 4\).
- **Step 4**: Traverse the array:
  - `i = 0`: `currentSum += 1` → `currentSum = 1`.
  - `i = 1`: `currentSum += 3` → `currentSum = 4` → Matches `target`.
    - `count = 1`, `firstSplit = 1`, reset `currentSum = 0`.
  - `i = 2`: `currentSum += 4` → `currentSum = 4` → Matches `target`.
    - `count = 2`, `secondSplit = 2`, reset `currentSum = 0`.
    - Stop traversal.
- **Result**: `[1, 2]`.

---

### **Test Case 2: `arr = [2, 3, 4]`**
- **Step 1**: Calculate `totalSum`:
  - \(2 + 3 + 4 = 9\)
- **Step 2**: Check if `totalSum % 3 == 0`:
  - \(9 \mod 3 = 0\) → Valid for splitting.
- **Step 3**: Calculate `target`:
  - \( \text{target} = 9 / 3 = 3\).
- **Step 4**: Traverse the array:
  - `i = 0`: `currentSum += 2` → `currentSum = 2`.
  - `i = 1`: `currentSum += 3` → `currentSum = 5`.
  - `i = 2`: `currentSum += 4` → `currentSum = 9`.
- No splits found where `currentSum == target`.
- **Result**: `[-1, -1]`.

---

### **Test Case 3: `arr = [0, 1, 1]`**
- **Step 1**: Calculate `totalSum`:
  - \(0 + 1 + 1 = 2\)
- **Step 2**: Check if `totalSum % 3 == 0`:
  - \(2 \mod 3 \neq 0\) → Not valid for splitting.
- **Result**: `[-1, -1]`.

---

### Final Results:
1. Test Case 1: `[1, 2]` → Valid.
2. Test Case 2: `[-1, -1]` → Valid.
3. Test Case 3: `[-1, -1]` → Valid.

### Conclusion:
The logic and implementation work as expected.