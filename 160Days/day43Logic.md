### **Approach for "Count pairs with given sum"**

The task is to count the number of distinct pairs in the array whose sum equals the given target. We'll use a **HashMap** to efficiently solve this problem.

---

### **Optimal Approach (Using a HashMap)**

#### Key Idea:
- A HashMap is used to store the frequency of each element as we traverse the array.  
- For each element, calculate its complement (\( \text{target} - \text{current\_element} \)) and check if the complement exists in the HashMap.  
- If it exists, add its frequency to the count of valid pairs.

---

### **Steps**:

1. **Initialize Data Structures**:
   - Create a `HashMap<Integer, Integer>` called `map` to store the frequency of elements.
   - Initialize a variable `count` to `0` to store the number of pairs.

2. **Iterate Through Array**:
   - For each element \( \text{num} \) in the array:
     1. Calculate the complement: \( \text{target} - \text{num} \).
     2. Check if the complement exists in the `map`:
        - If yes, add its frequency (value in `map`) to `count`.
     3. Add/update the current element in `map` with its frequency:  
        \( \text{map[num] = map.getOrDefault(num, 0) + 1} \).

3. **Return the Count**:
   - After processing the entire array, `count` will hold the number of valid pairs.

---

### **Complexity Analysis**:
- **Time Complexity**: \( O(n) \)
  - The array is traversed once, and HashMap operations (get, put) are \( O(1) \) on average.
- **Space Complexity**: \( O(n) \)
  - The HashMap can store up to \( n \) elements in the worst case.

---

### **Code Implementation**:

```java
import java.util.HashMap;

class Solution {
    int countPairs(int[] arr, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int count = 0;

        for (int num : arr) {
            // Check for complement and add its frequency to count
            count += map.getOrDefault(target - num, 0);
            
            // Update the frequency of the current number
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        return count;
    }
}
```

---

### **Dry Run Example**

#### Input:
```java
arr = [1, 5, 7, -1, 5];
target = 6;
```

---

### **Execution**:

1. **Initialization**:
   - `map = {}` (empty HashMap).
   - `count = 0`.

2. **Iteration**:
   - **Step 1**:
     - \( \text{num} = 1 \)
     - Complement: \( 6 - 1 = 5 \).
     - \( 5 \) is not in `map`. No pairs.
     - Add \( 1 \) to `map`: `map = {1: 1}`.
   - **Step 2**:
     - \( \text{num} = 5 \)
     - Complement: \( 6 - 5 = 1 \).
     - \( 1 \) is in `map` with frequency 1. Add \( 1 \) to `count`.
     - Update \( 5 \)'s frequency: `map = {1: 1, 5: 1}`.
     - `count = 1`.
   - **Step 3**:
     - \( \text{num} = 7 \)
     - Complement: \( 6 - 7 = -1 \).
     - \( -1 \) is not in `map`. No pairs.
     - Add \( 7 \) to `map`: `map = {1: 1, 5: 1, 7: 1}`.
   - **Step 4**:
     - \( \text{num} = -1 \)
     - Complement: \( 6 - (-1) = 7 \).
     - \( 7 \) is in `map` with frequency 1. Add \( 1 \) to `count`.
     - Update \( -1 \)'s frequency: `map = {1: 1, 5: 1, 7: 1, -1: 1}`.
     - `count = 2`.
   - **Step 5**:
     - \( \text{num} = 5 \)
     - Complement: \( 6 - 5 = 1 \).
     - \( 1 \) is in `map` with frequency 1. Add \( 1 \) to `count`.
     - Update \( 5 \)'s frequency: `map = {1: 1, 5: 2, 7: 1, -1: 1}`.
     - `count = 3`.

3. End of iteration.

---

### **Output**:
```java
3
```

Explanation: The pairs are \( (1, 5) \), \( (7, -1) \), and \( (1, 5) \) (repeated).