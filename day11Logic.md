Let's dry run the provided code for the `maxProduct` method using an example input. The goal is to find the maximum product of a contiguous subarray.


# java
```java
class Solution {

    int maxProduct(int[] nums) {
        int maxProduct = nums[0];
        int maxVal = nums[0];
        int minVal = nums[0];

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < 0) {

                int temp = maxVal;
                maxVal = minVal;
                minVal = temp;
            }

            maxVal = Math.max(nums[i], maxVal * nums[i]);
            minVal = Math.min(nums[i], minVal * nums[i]);

            maxProduct = Math.max(maxProduct, maxVal);
        }

        return maxProduct;
    }
}
```


### Code Explanation:
- We maintain two variables, `maxVal` and `minVal`, which track the maximum and minimum products up to the current element. The reason we track both is that a negative number can turn the smallest product into the largest product, so we need to handle this case.
- `maxProduct` keeps track of the overall maximum product encountered during the iteration.

### Example Input:
```java
nums = [2, 3, -2, 4]
```

### Initial Values:
- `maxProduct = nums[0] = 2`
- `maxVal = nums[0] = 2`
- `minVal = nums[0] = 2`

---

### Step-by-Step Execution:

#### **Iteration 1: `i = 1`, `nums[i] = 3`**
- Since `nums[i] = 3` is positive, we do not swap `maxVal` and `minVal`.
- `maxVal = Math.max(3, maxVal * 3) = Math.max(3, 2 * 3) = Math.max(3, 6) = 6`.
- `minVal = Math.min(3, minVal * 3) = Math.min(3, 2 * 3) = Math.min(3, 6) = 3`.
- `maxProduct = Math.max(maxProduct, maxVal) = Math.max(2, 6) = 6`.

---

#### **Iteration 2: `i = 2`, `nums[i] = -2`**
- Since `nums[i] = -2` is negative, we swap `maxVal` and `minVal`:
  - `maxVal = minVal = 3`
  - `minVal = maxVal = 6`
- Now, we calculate:
  - `maxVal = Math.max(-2, maxVal * -2) = Math.max(-2, 3 * -2) = Math.max(-2, -6) = -2`.
  - `minVal = Math.min(-2, minVal * -2) = Math.min(-2, 6 * -2) = Math.min(-2, -12) = -12`.
- `maxProduct = Math.max(maxProduct, maxVal) = Math.max(6, -2) = 6`.

---

#### **Iteration 3: `i = 3`, `nums[i] = 4`**
- Since `nums[i] = 4` is positive, we do not swap `maxVal` and `minVal`.
- `maxVal = Math.max(4, maxVal * 4) = Math.max(4, -2 * 4) = Math.max(4, -8) = 4`.
- `minVal = Math.min(4, minVal * 4) = Math.min(4, -12 * 4) = Math.min(4, -48) = -48`.
- `maxProduct = Math.max(maxProduct, maxVal) = Math.max(6, 4) = 6`.

---

### Final Result:
After iterating through the entire array, the `maxProduct` remains `6`, which is the maximum product of any contiguous subarray.

### Dry Run Summary:

#### Input:
```plaintext
nums = [2, 3, -2, 4]
```

#### Iterations:
| i  | `nums[i]` | `maxVal` | `minVal` | `maxProduct` |
|----|-----------|----------|----------|--------------|
| 0  | 2         | 2        | 2        | 2            |
| 1  | 3         | 6        | 3        | 6            |
| 2  | -2        | -2       | -12      | 6            |
| 3  | 4         | 4        | -48      | 6            |

#### Final Output:
```plaintext
maxProduct = 6
```

---

### Time Complexity:
- The algorithm runs in **O(n)** time where `n` is the length of the input array because it makes a single pass through the array.

### Space Complexity:
- The space complexity is **O(1)** since we are using only a constant amount of extra space.