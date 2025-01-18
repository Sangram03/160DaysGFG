Here is an efficient solution in Java to find the maximum distance between two occurrences of the same element:

### Code:

```java
class Solution {
    public int maxDistance(int[] arr) {
        // Code here
        Map<Integer, Integer> firstOccurrence = new HashMap<>();
        int maxDistance = 0;
        for (int i = 0; i < arr.length; i++) {
            if (firstOccurrence.containsKey(arr[i])) {
                int distance = i - firstOccurrence.get(arr[i]);
                maxDistance = Math.max(maxDistance, distance);
            }else {
                firstOccurrence.put(arr[i], i);
            }
        }
        return maxDistance;
    }
}
```

### Explanation:
1. **Using a HashMap**:
   - The key of the map is the element in the array.
   - The value is the first index where the element is encountered.

2. **Iterate through the Array**:
   - For each element, check if it already exists in the map.
   - If it exists, calculate the distance between the current index and the stored index in the map, and update `maxDistance` if this distance is greater.
   - If it doesn't exist, store the current index as the first occurrence of the element.

3. **Return the Result**:
   - After the loop, `maxDistance` contains the maximum distance between two occurrences of any element.

### Complexity:
- **Time Complexity**: \(O(n)\), where \(n\) is the size of the array. We traverse the array once and perform \(O(1)\) operations for each element in the map.
- **Space Complexity**: \(O(n)\), for storing the first occurrence index of each element in the map.

### Example Usage:
```java
public class Main {
    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.maxDistance(new int[]{1, 1, 2, 2, 2, 1})); // Output: 5
        System.out.println(solution.maxDistance(new int[]{3, 2, 1, 2, 1, 4, 5, 8, 6, 7, 4, 2})); // Output: 10
        System.out.println(solution.maxDistance(new int[]{1, 2, 3, 6, 5, 4})); // Output: 0
    }
}
```

### How It Works:
1. **First Example**:
   - Input: `[1, 1, 2, 2, 2, 1]`
   - First occurrence of `1` is at index `0`, and last occurrence is at index `5` → Distance = `5 - 0 = 5`.
   - First occurrence of `2` is at index `2`, and last occurrence is at index `4` → Distance = `4 - 2 = 2`.
   - Maximum distance = `5`.

2. **Second Example**:
   - Input: `[3, 2, 1, 2, 1, 4, 5, 8, 6, 7, 4, 2]`
   - Maximum distance is `10` for element `2`.

3. **Third Example**:
   - Input: `[1, 2, 3, 6, 5, 4]`
   - No element has two occurrences → Maximum distance = `0`.

This code satisfies the constraints and efficiently calculates the desired result.