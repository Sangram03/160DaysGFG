Here is the Java implementation for the Triplet Sum problem using sorting and the two-pointer technique:

### Java Code:
Here is my optimise code 

```java
class Solution {
    // Should return true if there is a triplet with sum equal
    // to x in arr[], otherwise false
    public static boolean hasTripletSum(int arr[], int target) {
        // Your code Here
        Arrays.sort(arr);
        for(int i=0;i<arr.length-2;i++)
        {
            int left=i+1;
            int right=arr.length-1;
            while(left<right)
            {
                int currentSum=arr[i]+arr[left]+arr[right];
                if(currentSum==target)
                {
                    return true;
                }else if(currentSum<target)
                {
                    left++;
                }else{
                    right--;
                }
            }
        }
        return false;
    }
}
```

```java
import java.util.Arrays;

public class TripletSum {

    public static boolean find3Numbers(int[] arr, int target) {
        // Sort the array
        Arrays.sort(arr);
        
        // Iterate through each element to fix one element
        for (int i = 0; i < arr.length - 2; i++) {
            int left = i + 1;  // Left pointer starts just after i
            int right = arr.length - 1;  // Right pointer starts at the end of the array
            
            while (left < right) {
                int currentSum = arr[i] + arr[left] + arr[right];
                
                // If we found a triplet, return true
                if (currentSum == target) {
                    return true;
                }
                // If the sum is too small, increase the left pointer
                else if (currentSum < target) {
                    left++;
                }
                // If the sum is too large, decrease the right pointer
                else {
                    right--;
                }
            }
        }
        
        // If no triplet is found, return false
        return false;
    }

    public static void main(String[] args) {
        // Test cases
        int[] arr1 = {1, 4, 45, 6, 10, 8};
        int target1 = 13;
        System.out.println(find3Numbers(arr1, target1));  // Output: true

        int[] arr2 = {1, 2, 4, 3, 6, 7};
        int target2 = 10;
        System.out.println(find3Numbers(arr2, target2));  // Output: true

        int[] arr3 = {40, 20, 10, 3, 6, 7};
        int target3 = 24;
        System.out.println(find3Numbers(arr3, target3));  // Output: false
    }
}
```

### Explanation:

1. **Sorting**: The array is sorted using `Arrays.sort()`. Sorting is crucial because it allows us to efficiently use the two-pointer technique to find a valid triplet.
   
2. **Outer Loop (`i`)**: We iterate over each element of the array (up to `arr.length - 2` because we need at least 3 elements to form a triplet).

3. **Two Pointers**:
   - `left` pointer starts just after the fixed element (`i + 1`).
   - `right` pointer starts at the last index (`arr.length - 1`).

4. **Sum Calculation**: For each fixed element `arr[i]`, we calculate the sum of `arr[i]`, `arr[left]`, and `arr[right]`:
   - If the sum equals the target, we return `true` (a valid triplet is found).
   - If the sum is smaller than the target, we move the `left` pointer right (`left++`) to increase the sum.
   - If the sum is larger than the target, we move the `right` pointer left (`right--`) to decrease the sum.

5. **Return False**: If no valid triplet is found after checking all possibilities, return `false`.

### Time Complexity:
- Sorting the array takes \(O(n \log n)\).
- The two-pointer approach inside the loop runs in \(O(n)\) for each fixed element.
- Therefore, the overall time complexity is \(O(n^2)\), which is efficient for the input size \(n \leq 1000\).

### Example Output:

For the following input:
```java
int[] arr1 = {1, 4, 45, 6, 10, 8};
int target1 = 13;
System.out.println(find3Numbers(arr1, target1));  // Output: true

int[] arr2 = {1, 2, 4, 3, 6, 7};
int target2 = 10;
System.out.println(find3Numbers(arr2, target2));  // Output: true

int[] arr3 = {40, 20, 10, 3, 6, 7};
int target3 = 24;
System.out.println(find3Numbers(arr3, target3));  // Output: false
```

- **First Example**: The triplet `{1, 4, 8}` sums up to 13, so the output is `true`.
- **Second Example**: The triplets `{1, 3, 6}` and `{1, 2, 7}` both sum to 10, so the output is `true`.
- **Third Example**: No triplet sums to 24, so the output is `false`.

### Conclusion:
This Java solution efficiently checks for a triplet that sums to the target using sorting and the two-pointer technique with a time complexity of \(O(n^2)\).