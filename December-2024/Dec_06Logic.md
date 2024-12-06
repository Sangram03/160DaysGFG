# java
```java

class Solution {
    // Function to find H-Index
    public int hIndex(int[] citations) {
        // Step 1: Sort the citations array in ascending order
        java.util.Arrays.sort(citations);
        int n = citations.length;

        // Step 2: Traverse the sorted array to find the H-Index
        for (int i = 0; i < n; i++) {
            int h = n - i; // Number of papers with at least 'h' citations
            if (citations[i] >= h) {
                return h;
            }
        }

        // Step 3: If no valid H-Index is found, return 0
        return 0;
    }

    // Example usage
    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] citations1 = {3, 0, 5, 3, 0};
        int[] citations2 = {5, 1, 2, 4, 1};
        int[] citations3 = {0, 0};

        System.out.println("H-Index (Example 1): " + solution.hIndex(citations1)); // Output: 3
        System.out.println("H-Index (Example 2): " + solution.hIndex(citations2)); // Output: 2
        System.out.println("H-Index (Example 3): " + solution.hIndex(citations3)); // Output: 0
    }
}



```


Let's perform a **dry run** of the program for better understanding. We'll trace the steps of the function for the given examples.

---

### **Example 1: `citations1 = {3, 0, 5, 3, 0}`**

1. **Input:** `citations = {3, 0, 5, 3, 0}`  
2. **Step 1: Sort the array:**  
   Sorted `citations = {0, 0, 3, 3, 5}`  
3. **Step 2: Traverse the sorted array:**  
   \[
   \text{n = 5 (length of array)}
   \]  

   - **Iteration 1 (i = 0):**  
     \[
     h = n - i = 5 - 0 = 5
     \]  
     Check: `citations[0] (0) >= h (5)` → False.

   - **Iteration 2 (i = 1):**  
     \[
     h = n - i = 5 - 1 = 4
     \]  
     Check: `citations[1] (0) >= h (4)` → False.

   - **Iteration 3 (i = 2):**  
     \[
     h = n - i = 5 - 2 = 3
     \]  
     Check: `citations[2] (3) >= h (3)` → True.  
     **Result:** `h = 3`.  

4. **Output:** `3`.

---

### **Example 2: `citations2 = {5, 1, 2, 4, 1}`**

1. **Input:** `citations = {5, 1, 2, 4, 1}`  
2. **Step 1: Sort the array:**  
   Sorted `citations = {1, 1, 2, 4, 5}`  
3. **Step 2: Traverse the sorted array:**  
   \[
   \text{n = 5 (length of array)}
   \]  

   - **Iteration 1 (i = 0):**  
     \[
     h = n - i = 5 - 0 = 5
     \]  
     Check: `citations[0] (1) >= h (5)` → False.

   - **Iteration 2 (i = 1):**  
     \[
     h = n - i = 5 - 1 = 4
     \]  
     Check: `citations[1] (1) >= h (4)` → False.

   - **Iteration 3 (i = 2):**  
     \[
     h = n - i = 5 - 2 = 3
     \]  
     Check: `citations[2] (2) >= h (3)` → False.

   - **Iteration 4 (i = 3):**  
     \[
     h = n - i = 5 - 3 = 2
     \]  
     Check: `citations[3] (4) >= h (2)` → True.  
     **Result:** `h = 2`.  

4. **Output:** `2`.

---

### **Example 3: `citations3 = {0, 0}`**

1. **Input:** `citations = {0, 0}`  
2. **Step 1: Sort the array:**  
   Sorted `citations = {0, 0}`  
3. **Step 2: Traverse the sorted array:**  
   \[
   \text{n = 2 (length of array)}
   \]  

   - **Iteration 1 (i = 0):**  
     \[
     h = n - i = 2 - 0 = 2
     \]  
     Check: `citations[0] (0) >= h (2)` → False.

   - **Iteration 2 (i = 1):**  
     \[
     h = n - i = 2 - 1 = 1
     \]  
     Check: `citations[1] (0) >= h (1)` → False.

4. **Output:** `0`.

---

### **Final Results:**
1. **Example 1 Output:** `3`
2. **Example 2 Output:** `2`
3. **Example 3 Output:** `0`

This step-by-step dry run aligns with the expected outputs, confirming the correctness of the function.