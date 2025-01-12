Here's a simple and efficient solution to count the number of pairs whose sum is less than the target. We'll use a two-pointer approach to optimize the solution, which sorts the array first and then calculates the pairs.

### Approach:
1. **Sort the Array** – Sorting helps in efficiently finding pairs with the two-pointer technique.  
2. **Two-Pointer Technique** – Initialize two pointers, one at the beginning (`i`) and one at the end (`j`).  
3. **Calculate Pair Sums**:  
   - If the sum of `arr[i] + arr[j]` is less than the target, all pairs between `i` and `j` will be valid.  
   - Move the left pointer (`i`) to find more pairs.  
   - If the sum is greater than or equal to the target, move the right pointer (`j`) left.  
4. **Count Pairs Efficiently** – Instead of checking each combination (O(n²)), the sorted array and two-pointer reduce it to O(n log n) due to sorting.

---

### Code Implementation (Java):
```java


class Solution {
    int countPairs(int arr[], int target) {
        Arrays.sort(arr);  // Step 1: Sort the array
        int count = 0;
        int i = 0, j = arr.length - 1;
        
        while (i < j) {
            if (arr[i] + arr[j] < target) {
                // All pairs between i and j will be valid
                count += (j - i);
                i++;  // Move the left pointer
            } else {
                j--;  // Move the right pointer
            }
        }
        return count;
    }
}
```

---

### How it Works (Example Walkthrough):
- **Example 1:**  
  - `arr = [7, 2, 5, 3]` and `target = 8`  
  - After sorting: `[2, 3, 5, 7]`  
  - Pairs: `(2, 5), (2, 3)` → **Count = 2**  
- **Example 2:**  
  - `arr = [5, 2, 3, 2, 4, 1]` and `target = 5`  
  - After sorting: `[1, 2, 2, 3, 4, 5]`  
  - Pairs: `(1, 2), (1, 2), (1, 3), (2, 2)` → **Count = 4**  

---

### Complexity Analysis:
- **Time Complexity:**  
  - Sorting: `O(n log n)`  
  - Two-pointer traversal: `O(n)`  
  - Total: `O(n log n)`  

- **Space Complexity:**  
  - `O(1)` (No extra space used except for sorting)

---

### Why This Approach?
- **Efficient for Large Arrays** – Handles up to `10^5` elements within constraints.  
- **Optimized Counting** – The use of two-pointer skips unnecessary comparisons.  
- **Scalable** – Works well within the provided constraints.


---

### Example:  
**Input:**  
`arr = [7, 2, 5, 3]`  
`target = 8`  

---

### Step 1: Sort the Array  
- After sorting:  
`arr = [2, 3, 5, 7]`  

---

### Step 2: Initialize Pointers and Variables  
- `i = 0` (left pointer at 2)  
- `j = 3` (right pointer at 7)  
- `count = 0`  

---

### Step 3: Start the `while` Loop  
- **Condition:** `i < j`  

---

### Iterations:

1. **First Iteration:**  
   - `arr[i] + arr[j] = 2 + 7 = 9` (greater than or equal to target)  
   - **Action:** Move `j` left → `j = 2` (points to 5)  

2. **Second Iteration:**  
   - `arr[i] + arr[j] = 2 + 5 = 7` (less than target)  
   - **Action:**  
     - Add pairs: `(j - i) = (2 - 0) = 2` → `count = 2`  
     - Move `i` right → `i = 1` (points to 3)  

3. **Third Iteration:**  
   - `arr[i] + arr[j] = 3 + 5 = 8` (greater than or equal to target)  
   - **Action:** Move `j` left → `j = 1` (points to 3)  

---

### Step 4: Exit Loop  
- **Condition:** `i < j` fails (`i = 1`, `j = 1`)  

---

### Final Count:  
- **Result:** `count = 2`  

---

### Pairs that Meet the Condition:  
- `(2, 5)`  
- `(2, 3)`  

---

### How the Algorithm Works:  
- The algorithm effectively counts all pairs without unnecessary comparisons by leveraging the sorted array and two-pointer technique.  
- By moving the left pointer `i` when the sum is less than the target, all pairs between `i` and `j` are counted at once, reducing redundant checks.  

Would you like to try another example or go over edge cases?