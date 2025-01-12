### Approach:

To solve the problem of trapping rainwater, we need to determine the amount of water that can be trapped over each block based on the heights of the blocks to the left and right of it.

#### Key Insight:
The water that can be trapped above a block \(i\) depends on the **minimum** of the highest blocks on its **left** and **right**, minus the height of the block itself.

---

### Steps:

1. **Precompute Left and Right Maximum Arrays**:
   - Create two arrays:
     - `leftMax[i]`: Stores the maximum height of the blocks to the left of (and including) \(i\).
     - `rightMax[i]`: Stores the maximum height of the blocks to the right of (and including) \(i\).

2. **Calculate Trapped Water**:
   - For each block \(i\), compute the water trapped:
     - \( \text{water[i]} = \text{min(leftMax[i], rightMax[i])} - \text{arr[i]} \)
   - If this value is positive, add it to the total trapped water.

3. **Return the Total**:
   - Return the sum of the water trapped at all indices.

---

### Implementation:

```java
class Solution {
    public int maxWater(int arr[]) {
        int n = arr.length;
        if (n <= 2) return 0; // Not enough blocks to trap water

        // Create arrays to store the left and right maximums
        int[] leftMax = new int[n];
        int[] rightMax = new int[n];

        // Fill the leftMax array
        leftMax[0] = arr[0];
        for (int i = 1; i < n; i++) {
            leftMax[i] = Math.max(leftMax[i - 1], arr[i]);
        }

        // Fill the rightMax array
        rightMax[n - 1] = arr[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            rightMax[i] = Math.max(rightMax[i + 1], arr[i]);
        }

        // Calculate the total trapped water
        int trappedWater = 0;
        for (int i = 0; i < n; i++) {
            trappedWater += Math.max(0, Math.min(leftMax[i], rightMax[i]) - arr[i]);
        }

        return trappedWater;
    }
}
```

---

### Dry Run:

#### Input: `arr[] = [3, 0, 2, 0, 4]`

1. **Step 1: Compute `leftMax` and `rightMax`**:
   - `leftMax`: `[3, 3, 3, 3, 4]`
   - `rightMax`: `[4, 4, 4, 4, 4]`

2. **Step 2: Calculate Trapped Water**:
   - For each block \(i\):
     - \( \text{water[i]} = \text{min(leftMax[i], rightMax[i])} - \text{arr[i]} \)
   - \( i = 0: \text{min(3, 4)} - 3 = 0 \)
   - \( i = 1: \text{min(3, 4)} - 0 = 3 \)
   - \( i = 2: \text{min(3, 4)} - 2 = 1 \)
   - \( i = 3: \text{min(3, 4)} - 0 = 3 \)
   - \( i = 4: \text{min(4, 4)} - 4 = 0 \)

3. **Total Trapped Water**:
   - \( 0 + 3 + 1 + 3 + 0 = 7 \)

**Output**: `7`

---

### Complexity:

1. **Time Complexity**:
   - Computing `leftMax` and `rightMax`: \(O(n)\)
   - Calculating trapped water: \(O(n)\)
   - Total: \(O(n)\)

2. **Space Complexity**:
   - Storing `leftMax` and `rightMax`: \(O(n)\)
   - Total: \(O(n)\)

---

This approach ensures optimal performance while maintaining clarity, making it suitable for large inputs.