### Approach:

The goal is to count the number of pairs in a sorted array whose sum equals the given target. Since the array is sorted, we can efficiently solve the problem using the **Two-Pointer Technique**. Alternatively, we can also use a **HashMap** to track the frequency of required complements for each number.

---

### Steps:
#### 1. **HashMap Approach**:
   - Use a `HashMap` to keep track of the frequency of elements encountered so far.
   - For each element in the array:
     - Check if the complement (`target - num`) exists in the map. If it does, add the frequency of the complement to the result.
     - Add the current element to the frequency map.
   - Return the total count of pairs.

---

### Implementation:

```java
import java.util.HashMap;

class Solution {
    int countPairs(int[] arr, int target) {
        // HashMap to store frequencies of elements
        HashMap<Integer, Integer> freq = new HashMap<>();
        int count = 0;

        // Iterate through the array
        for (int num : arr) {
            // Check if the complement exists
            count += freq.getOrDefault(target - num, 0);
            // Update the frequency of the current number
            freq.put(num, freq.getOrDefault(num, 0) + 1);
        }

        return count;
    }
}
```

---

### Dry Run:

#### Example 1:
**Input**: `arr[] = [-1, 1, 5, 5, 7]`, `target = 6`

**Steps**:
1. Initialize `freq = {}`, `count = 0`
2. Process elements:
   - **num = -1**:
     - Complement: `6 - (-1) = 7`
     - `freq = {-1: 1}`, `count = 0`
   - **num = 1**:
     - Complement: `6 - 1 = 5`
     - `freq = {-1: 1, 1: 1}`, `count = 0`
   - **num = 5**:
     - Complement: `6 - 5 = 1`
     - `freq = {-1: 1, 1: 1, 5: 1}`, `count = 1`
   - **num = 5**:
     - Complement: `6 - 5 = 1`
     - `freq = {-1: 1, 1: 1, 5: 2}`, `count = 2`
   - **num = 7**:
     - Complement: `6 - 7 = -1`
     - `freq = {-1: 1, 1: 1, 5: 2, 7: 1}`, `count = 3`

**Output**: `3`

---

#### Example 2:
**Input**: `arr[] = [1, 1, 1, 1]`, `target = 2`

**Steps**:
1. Initialize `freq = {}`, `count = 0`
2. Process elements:
   - **num = 1**:
     - Complement: `2 - 1 = 1`
     - `freq = {1: 1}`, `count = 0`
   - **num = 1**:
     - Complement: `2 - 1 = 1`
     - `freq = {1: 2}`, `count = 1`
   - **num = 1**:
     - Complement: `2 - 1 = 1`
     - `freq = {1: 3}`, `count = 3`
   - **num = 1**:
     - Complement: `2 - 1 = 1`
     - `freq = {1: 4}`, `count = 6`

**Output**: `6`

---

#### Example 3:
**Input**: `arr[] = [-1, 10, 10, 12, 15]`, `target = 125`

**Steps**:
1. Initialize `freq = {}`, `count = 0`
2. Process elements:
   - **num = -1**:
     - Complement: `125 - (-1) = 126`
     - `freq = {-1: 1}`, `count = 0`
   - **num = 10**:
     - Complement: `125 - 10 = 115`
     - `freq = {-1: 1, 10: 1}`, `count = 0`
   - **num = 10**:
     - Complement: `125 - 10 = 115`
     - `freq = {-1: 1, 10: 2}`, `count = 0`
   - **num = 12**:
     - Complement: `125 - 12 = 113`
     - `freq = {-1: 1, 10: 2, 12: 1}`, `count = 0`
   - **num = 15**:
     - Complement: `125 - 15 = 110`
     - `freq = {-1: 1, 10: 2, 12: 1, 15: 1}`, `count = 0`

**Output**: `0`

---

### Complexity Analysis:
1. **Time Complexity**: 
   - Iterating through the array: \(O(n)\)
   - Accessing/updating the `HashMap`: \(O(1)\) (average case)
   - Total: \(O(n)\)
   
2. **Space Complexity**: 
   - HashMap stores at most \(n\) elements: \(O(n)\)

---

### Advantages of the HashMap Approach:
- Handles duplicate elements in the array efficiently.
- Works in linear time, making it ideal for large input sizes.