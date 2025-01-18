Here is an efficient solution in Java to calculate the minimum number of subsets with consecutive numbers:

### Code:

```java
class Solution {
    public int numOfSubset(int[] arr) {
        // Your code goes here
        Arrays.sort(arr);
        int subsets = 1;
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] != arr[i - 1] + 1) {
                subsets++;
            }
        }
        return subsets;
    }
}
```

### Explanation:
1. **Sorting**:
   - Sorting ensures that consecutive numbers are adjacent in the array, making it easy to group them.

2. **Counting Subsets**:
   - Start with at least one subset.
   - Traverse the sorted array and check if the current number is consecutive to the previous one.
   - If not, it indicates the start of a new subset.

3. **Return the Result**:
   - The variable `subsets` tracks the number of subsets.

### Complexity:
- **Time Complexity**: \(O(n \log n)\), due to sorting the array.
- **Space Complexity**: \(O(1)\), as we are not using any additional data structures apart from a few variables.

### Example Usage:

```java
public class Main {
    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.numOfSubset(new int[]{100, 56, 5, 6, 102, 58, 101, 57, 7, 103})); // Output: 3
        System.out.println(solution.numOfSubset(new int[]{10, 100, 105})); // Output: 3
    }
}
```

### Example Walkthrough:
1. **Input**: `arr = [100, 56, 5, 6, 102, 58, 101, 57, 7, 103]`
   - Sorted array: `[5, 6, 7, 56, 57, 58, 100, 101, 102, 103]`
   - Subsets:
     - `{5, 6, 7}` (consecutive)
     - `{56, 57, 58}` (consecutive)
     - `{100, 101, 102, 103}` (consecutive)
   - Output: `3`.

2. **Input**: `arr = [10, 100, 105]`
   - Sorted array: `[10, 100, 105]`
   - Subsets:
     - `{10}` (not consecutive with others)
     - `{100}` (not consecutive with others)
     - `{105}` (not consecutive with others)
   - Output: `3`.

This solution is efficient, simple, and adheres to the given constraints.