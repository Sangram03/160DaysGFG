### Approach:

The task is to find the indices of the first subarray whose sum equals a given target. This problem can be efficiently solved using a **sliding window (two-pointer)** approach because the array contains only non-negative integers.

---

### Steps:

1. **Initialize Variables**:
   - `s` (start pointer): Tracks the start of the current subarray.
   - `curr` (current sum): Tracks the sum of the current subarray.
   - Iterate through the array with `e` (end pointer).

2. **Expand the Window**:
   - Add `arr[e]` to `curr` to expand the subarray.

3. **Shrink the Window**:
   - If `curr > target`, increment `s` (move the start pointer) and subtract `arr[s]` from `curr` to shrink the subarray. Repeat this until `curr <= target`.

4. **Check for the Target**:
   - If `curr == target`, return the 1-based indices `[s + 1, e + 1]`.

5. **Return Default**:
   - If no subarray with the given sum is found, return `[-1]`.

---

### Implementation:

```java
class Solution {
    static ArrayList<Integer> subarraySum(int[] arr, int target) {
        int s = 0, curr = 0;

        // Traverse the array with the end pointer
        for (int e = 0; e < arr.length; e++) {
            // Add the current element to the running sum
            curr += arr[e];

            // Shrink the window until the sum is less than or equal to the target
            while (curr > target && s <= e) {
                curr -= arr[s];
                s++;
            }

            // Check if we found the target sum
            if (curr == target) {
                return new ArrayList<>(Arrays.asList(s + 1, e + 1));
            }
        }

        // No subarray found
        return new ArrayList<>(Arrays.asList(-1));
    }
}
```

---

### Dry Run:

#### Example 1:
**Input**: `arr[] = [1, 2, 3, 7, 5], target = 12`

1. `s = 0, curr = 0`
2. `e = 0`: `curr = 1` (1 not equal to 12).
3. `e = 1`: `curr = 1 + 2 = 3` (3 not equal to 12).
4. `e = 2`: `curr = 3 + 3 = 6` (6 not equal to 12).
5. `e = 3`: `curr = 6 + 7 = 13` (shrink: `curr = 13 - 1 = 12`), **found** `[2, 4]`.

**Output**: `[2, 4]`

---

#### Example 2:
**Input**: `arr[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], target = 15`

1. `s = 0, curr = 0`
2. `e = 0`: `curr = 1` (not equal to 15).
3. `e = 1`: `curr = 1 + 2 = 3` (not equal to 15).
4. `e = 4`: `curr = 1 + 2 + 3 + 4 + 5 = 15`, **found** `[1, 5]`.

**Output**: `[1, 5]`

---

#### Example 3:
**Input**: `arr[] = [5, 3, 4], target = 2`

1. `s = 0, curr = 0`
2. `e = 0`: `curr = 5` (shrink: `curr = 5 - 5 = 0`).
3. `e = 1`: `curr = 0 + 3 = 3` (not equal to 2).
4. `e = 2`: `curr = 3 + 4 = 7` (shrink: `curr = 7 - 3 = 4`), no match.

**Output**: `[-1]`

---

### Complexity:

1. **Time Complexity**: 
   - \(O(n)\): Each element is processed at most twice (once when expanding, once when shrinking).
2. **Space Complexity**: 
   - \(O(1)\): No extra space apart from variables.

---

### Advantages:
- Handles large arrays efficiently due to \(O(n)\) complexity.
- Simple implementation using the sliding window technique.