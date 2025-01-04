### Approach to Solve the Problem:

To count all triplets \((i, j, k)\) in a **sorted array** such that \( \text{arr}[i] + \text{arr}[j] + \text{arr}[k] = \text{target} \), we can use the **two-pointer technique** for efficient computation.

---

#### **Steps in the Approach:**

1. **Sort the Array**:
   - Since the array is already sorted as per the problem statement, no additional sorting is required.

2. **Iterate Over the First Element of the Triplet**:
   - Use a loop to fix the first element of the triplet (`arr[i]`) at index `i`.
   - For each fixed element, we will search for the other two elements using the two-pointer technique.

3. **Two-Pointer Technique**:
   - Initialize two pointers:
     - `left = i + 1` (the next element after `i`).
     - `right = n - 1` (the last element of the array).
   - Calculate the sum of the triplet:  
     \[
     \text{sum} = \text{arr}[i] + \text{arr}[left] + \text{arr}[right]
     \]
   - Check the following conditions:
     - **If sum equals target**:  
       - Count all valid combinations of duplicates between `left` and `right`.
       - Increment the count by multiplying the duplicates:  
         \[
         \text{count} += \text{leftCount} \times \text{rightCount}
         \]
       - Move both pointers inward: `left++`, `right--`.
     - **If sum < target**:  
       - Move the `left` pointer rightward (`left++`) to increase the sum.
     - **If sum > target**:  
       - Move the `right` pointer leftward (`right--`) to decrease the sum.

4. **Handle Duplicates**:
   - If the array contains duplicates (e.g., `arr[left] == arr[left + 1]` or `arr[right] == arr[right - 1]`), count the number of occurrences of the duplicate elements:
     - Count duplicates on the left side (`leftCount`).
     - Count duplicates on the right side (`rightCount`).
   - Multiply `leftCount` and `rightCount` to get all combinations of triplets formed by these duplicate elements.

5. **Stop Condition**:
   - When `left` crosses `right`, exit the inner loop and proceed to the next value of `i`.

6. **Return the Count**:
   - After all iterations, return the total count of valid triplets.

---



# java
```java



class Solution {
    public int countTriplets(int[] arr, int target) {
        int n = arr.length;
        int count = 0;

        for (int i = 0; i < n - 2; i++) {
            int left = i + 1;
            int right = n - 1;

            while (left < right) {
                int sum = arr[i] + arr[left] + arr[right];

                if (sum == target) {
                    if (arr[left] == arr[right]) {
                        // If all elements between left and right are the same
                        int totalElements = right - left + 1;
                        count += (totalElements * (totalElements - 1)) / 2; // Choose 2 from totalElements
                        break; // Move to the next i as all combinations are counted
                    } else {
                        // Count duplicates for left and right separately
                        int leftCount = 1, rightCount = 1;

                        while (left + 1 < right && arr[left] == arr[left + 1]) {
                            left++;
                            leftCount++;
                        }

                        while (right - 1 > left && arr[right] == arr[right - 1]) {
                            right--;
                            rightCount++;
                        }

                        // Add all combinations of these duplicates
                        count += leftCount * rightCount;

                        left++;
                        right--;
                    }
                } else if (sum < target) {
                    left++;
                } else {
                    right--;
                }
            }
        }

        return count;
    }
}


```



### **Complexity Analysis**:
1. **Time Complexity**:  
   - Outer loop: \(O(n)\) (to iterate over `i`).
   - Inner loop (two-pointer): \(O(n)\) in the worst case for each `i`.
   - Total complexity: \(O(n^2)\), which is efficient given the constraints \(3 \leq n \leq 10^4\).

2. **Space Complexity**:  
   - \(O(1)\), as no additional data structures are used.

---
Let’s **dry run** the given code with an example input to understand how it works step by step:

---

### **Input:**
```plaintext
arr = [-3, -1, -1, 0, 1, 2]
target = -2
```

### **Expected Output:**
There are **4 triplets** whose sum equals \(-2\):
1. \(-3 + 0 + 1 = -2\)
2. \(-3 + (-1) + 2 = -2\)  
   (counted twice due to duplicate \(-1\))
3. \(-1 + (-1) + 0 = -2\)

---

### **Dry Run**:

#### **Initialization:**
- \(n = 6\), \(count = 0\).

---

#### **Outer Loop Iteration \(i = 0\):**
- Fixed element: \(arr[i] = -3\).
- Initialize \(left = 1\) (\(arr[left] = -1\)) and \(right = 5\) (\(arr[right] = 2\)).

---

##### **First Inner Loop (\(left = 1, right = 5\)):**
- Compute \(sum = -3 + (-1) + 2 = -2\) → Matches \(target\).
- Since \(arr[left] \neq arr[right]\):
  - \(leftCount = 1\), \(rightCount = 1\) (no duplicates).
- Increment \(count\) by \(leftCount \times rightCount = 1\).
- Move \(left++ = 2\), \(right-- = 4\).

---

##### **Second Inner Loop (\(left = 2, right = 4\)):**
- Compute \(sum = -3 + (-1) + 1 = -3\) → Less than \(target\).
- Move \(left++ = 3\).

---

##### **Third Inner Loop (\(left = 3, right = 4\)):**
- Compute \(sum = -3 + 0 + 1 = -2\) → Matches \(target\).
- Since \(arr[left] \neq arr[right]\):
  - \(leftCount = 1\), \(rightCount = 1\).
- Increment \(count\) by \(leftCount \times rightCount = 1\).
- Move \(left++ = 4\), \(right-- = 3\).

---

#### **Outer Loop Iteration \(i = 1\):**
- Fixed element: \(arr[i] = -1\).
- Initialize \(left = 2\) (\(arr[left] = -1\)) and \(right = 5\) (\(arr[right] = 2\)).

---

##### **First Inner Loop (\(left = 2, right = 5\)):**
- Compute \(sum = -1 + (-1) + 2 = 0\) → Greater than \(target\).
- Move \(right-- = 4\).

---

##### **Second Inner Loop (\(left = 2, right = 4\)):**
- Compute \(sum = -1 + (-1) + 1 = -2\) → Matches \(target\).
- Since \(arr[left] \neq arr[right]\):
  - \(leftCount = 1\), \(rightCount = 1\).
- Increment \(count\) by \(leftCount \times rightCount = 1\).
- Move \(left++ = 3\), \(right-- = 3\).

---

#### **Outer Loop Iteration \(i = 2\):**
- Fixed element: \(arr[i] = -1\).
- Initialize \(left = 3\) (\(arr[left] = 0\)) and \(right = 5\) (\(arr[right] = 2\)).

---

##### **First Inner Loop (\(left = 3, right = 5\)):**
- Compute \(sum = -1 + 0 + 2 = 1\) → Greater than \(target\).
- Move \(right-- = 4\).

---

##### **Second Inner Loop (\(left = 3, right = 4\)):**
- Compute \(sum = -1 + 0 + 1 = 0\) → Does not match \(target\).
- Move \(right-- = 3\).

---

#### **Outer Loop Iteration \(i = 3\):**
- Fixed element: \(arr[i] = 0\).  
- \(left = 4\), \(right = 5\).  
- Compute \(sum = 0 + 1 + 2 = 3\) → Greater than \(target\).  
- Exit inner loop.

---

### **Final Count**:
- Total \(count = 4\).

---

### **Output**:
```plaintext
4
```
