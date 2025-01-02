### **Approach for "Two Sum - Pair with Given Sum"**

The task is to find if there exists a pair of distinct indices \(i\) and \(j\) in the array such that the sum of their elements equals the given target. 

---

### **Optimal Approach (Using a HashSet)**

1. **Use a HashSet**:
   - A HashSet is used to store the elements of the array as we iterate through it. 
   - While traversing, we check if the complement of the current element (i.e., `target - current element`) exists in the set.

2. **Logic**:
   - For each element \( arr[i] \):
     - Check if \( \text{target} - arr[i] \) exists in the set:
       - If yes, return `true` since we found a pair.
       - If no, add \( arr[i] \) to the set.
   - If we traverse the entire array without finding a pair, return `false`.

3. **Why it Works**:
   - The HashSet allows constant time complexity (\(O(1)\)) for insertions and lookups.
   - The algorithm ensures that any potential pair is checked efficiently during traversal.

4. **Edge Cases**:
   - If the array has fewer than 2 elements, return `false`.
   - Handle cases where no such pair exists (e.g., all numbers are too small or too large compared to the target).

---

### **Algorithm Steps**:

1. Initialize an empty HashSet `seen` to store the elements we have processed.
2. Traverse the array:
   - For the current element `num`, calculate the complement: \( \text{target} - \text{num} \).
   - Check if the complement exists in the HashSet:
     - If yes, return `true`.
     - If no, add the current element to the HashSet.
3. If the loop completes without finding a pair, return `false`.

---

### **Complexity Analysis**:
- **Time Complexity**: \( O(n) \)
  - Each element is processed once, and HashSet operations (insert and lookup) take \( O(1) \) on average.
- **Space Complexity**: \( O(n) \)
  - The HashSet stores up to \( n \) elements in the worst case.

---

### **Code Implementation**:

```java

class Solution {
    boolean twoSum(int[] arr, int target) {
        Set<Integer> seen = new HashSet<>();
        for (int num : arr) {
            // Check if the complement exists
            if (seen.contains(target - num)) {
                return true;
            }
            // Add the current element to the set
            seen.add(num);
        }
        return false; // No pair found
    }
}
```

### **Dry Run for `twoSum`**

### **Input:**
```java
arr = [1, 4, 45, 6, 10, 8];
target = 16;
```

---

### **Execution Steps**:

1. **Initialization**:
   - `seen = {}` (empty set).

2. **Iteration**:
   - **Step 1**:
     - `num = 1`
     - Complement: \( \text{target} - \text{num} = 16 - 1 = 15 \)
     - Is \( 15 \) in `seen`? **No**.
     - Add \( 1 \) to `seen`: `seen = {1}`.
   - **Step 2**:
     - `num = 4`
     - Complement: \( 16 - 4 = 12 \)
     - Is \( 12 \) in `seen`? **No**.
     - Add \( 4 \) to `seen`: `seen = {1, 4}`.
   - **Step 3**:
     - `num = 45`
     - Complement: \( 16 - 45 = -29 \)
     - Is \( -29 \) in `seen`? **No**.
     - Add \( 45 \) to `seen`: `seen = {1, 4, 45}`.
   - **Step 4**:
     - `num = 6`
     - Complement: \( 16 - 6 = 10 \)
     - Is \( 10 \) in `seen`? **No**.
     - Add \( 6 \) to `seen`: `seen = {1, 4, 45, 6}`.
   - **Step 5**:
     - `num = 10`
     - Complement: \( 16 - 10 = 6 \)
     - Is \( 6 \) in `seen`? **Yes**.
     - **Return `true`** because we found a pair (\(6\) and \(10\)).

---

### **Output**:
`true`  
Explanation: The pair \( (6, 10) \) gives the sum \( 16 \). 

---

### **Another Example**

#### **Input**:
```java
arr = [1, 2, 4, 3, 6];
target = 11;
```

---

### **Execution Steps**:

1. **Initialization**:
   - `seen = {}`.

2. **Iteration**:
   - **Step 1**:
     - `num = 1`
     - Complement: \( 11 - 1 = 10 \)
     - Is \( 10 \) in `seen`? **No**.
     - Add \( 1 \) to `seen`: `seen = {1}`.
   - **Step 2**:
     - `num = 2`
     - Complement: \( 11 - 2 = 9 \)
     - Is \( 9 \) in `seen`? **No**.
     - Add \( 2 \) to `seen`: `seen = {1, 2}`.
   - **Step 3**:
     - `num = 4`
     - Complement: \( 11 - 4 = 7 \)
     - Is \( 7 \) in `seen`? **No**.
     - Add \( 4 \) to `seen`: `seen = {1, 2, 4}`.
   - **Step 4**:
     - `num = 3`
     - Complement: \( 11 - 3 = 8 \)
     - Is \( 8 \) in `seen`? **No**.
     - Add \( 3 \) to `seen`: `seen = {1, 2, 3, 4}`.
   - **Step 5**:
     - `num = 6`
     - Complement: \( 11 - 6 = 5 \)
     - Is \( 5 \) in `seen`? **No**.
     - Add \( 6 \) to `seen`: `seen = {1, 2, 3, 4, 6}`.

3. End of iteration. No pair was found.

---

### **Output**:
`false`  
Explanation: No pair sums up to \( 11 \).