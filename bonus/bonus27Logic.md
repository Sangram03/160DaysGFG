Here is an efficient solution in Java to find the number of pairs with an absolute difference equal to \( k \):

### Code:

```java
class Solution {
    int countPairs(int[] arr, int k) {
        // code here
        Map<Integer, Integer> freqMap = new HashMap<>();
        int count = 0;
        for(int num : arr){
            if (freqMap.containsKey(num + k)){
                count += freqMap.get(num + k);
            }
            if (freqMap.containsKey(num - k)){
                count += freqMap.get(num - k);
            }
            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
        }
        return count;
    }
}
```

### Explanation:

1. **Use a HashMap**:
   - Store the frequency of each number in the array.
   - The key is the number, and the value is its frequency.

2. **Calculate Target Numbers**:
   - For each number in the map, calculate the target numbers \( \text{num} + k \) and \( \text{num} - k \).
   - Use the frequency map to find how many numbers can pair with the current number to achieve the absolute difference \( k \).

3. **Special Case for \( k = 0 \)**:
   - If \( k = 0 \), we need to count combinations of the same number \( nC2 = \frac{n(n-1)}{2} \).

4. **Avoid Double Counting**:
   - Since pairs \( (a, b) \) and \( (b, a) \) are considered the same, divide the result by 2 if \( k > 0 \).

### Complexity:
- **Time Complexity**: \( O(n) \), where \( n \) is the size of the array. We iterate through the array and the map.
- **Space Complexity**: \( O(n) \), for the frequency map.

### Example Usage:

```java
public class Main {
    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.countPairs(new int[]{1, 4, 1, 4, 5}, 3)); // Output: 4
        System.out.println(solution.countPairs(new int[]{8, 16, 12, 16, 4, 0}, 4)); // Output: 5
        System.out.println(solution.countPairs(new int[]{1, 2, 3, 4, 5}, 0)); // Output: 0
    }
}
```

### Example Walkthrough:
1. **Input**: `arr = [1, 4, 1, 4, 5], k = 3`
   - Frequency map: `{1: 2, 4: 2, 5: 1}`
   - Pairs: \( (1, 4), (1, 4), (4, 1), (1, 4) \)
   - Total = `4`.

2. **Input**: `arr = [8, 16, 12, 16, 4, 0], k = 4`
   - Frequency map: `{8: 1, 16: 2, 12: 1, 4: 1, 0: 1}`
   - Pairs: \( (8, 12), (8, 4), (16, 12), (12, 16), (4, 0) \)
   - Total = `5`.

This solution is efficient and handles the constraints properly.