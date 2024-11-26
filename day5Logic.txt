Here's the detailed dry run for the **nextPermutation** algorithm.

---

### Input Example:
```java
arr = {1, 2, 3};
```

---

### Goal:
Find the next lexicographical permutation of the given array. If no such permutation exists, rearrange the array into its smallest permutation (sorted in ascending order).

---

### Steps in the Algorithm:

#### Initial Values:
- `arr = {1, 2, 3}`
- `n = 3`, `i = 1` (initialized to `n - 2`), `j = 2` (initialized to `n - 1`).

---

#### **Step 1: Find the first decreasing element (`i`):**
Iterate backward from the second-to-last element (`i = n - 2`) and find the first index where `arr[i] < arr[i + 1]`.

- **Iteration 1:** `i = 1`, check `arr[1] = 2` and `arr[2] = 3`.  
  - Since `arr[1] < arr[2]`, we stop.  
  - `i = 1`.

---

#### **Step 2: Find the smallest element larger than `arr[i]` (`j`):**
Iterate backward from the last element (`j = n - 1`) and find the smallest element larger than `arr[i]`.

- **Iteration 1:** `j = 2`, check `arr[2] = 3` and `arr[1] = 2`.  
  - Since `arr[2] > arr[1]`, we stop.  
  - `j = 2`.

---

#### **Step 3: Swap `arr[i]` and `arr[j]`:**
Swap the values of `arr[i]` and `arr[j]`.

- Swap `arr[1]` and `arr[2]`:  
  - Before swap: `arr = {1, 2, 3}`.  
  - After swap: `arr = {1, 3, 2}`.

---

#### **Step 4: Reverse the subarray from `i + 1` to `n - 1`:**
Reverse the portion of the array starting from `i + 1` to the end (`n - 1`).

- Reverse `arr[2]` to `arr[2]` (only one element, so no change):  
  - Final `arr = {1, 3, 2}`.

---

### Final Output:
```java
arr = {1, 3, 2};
```

---

### Dry Run Summary for Example 1:

#### Initial Array:
```plaintext
{1, 2, 3}
```

#### Step 1 (Find `i`):  
- First decreasing element: `arr[1] = 2` at index `1`.

#### Step 2 (Find `j`):  
- Smallest element larger than `arr[1] = 2`: `arr[2] = 3` at index `2`.

#### Step 3 (Swap):  
- Swap `arr[1]` and `arr[2]`:  
  - Result: `{1, 3, 2}`.

#### Step 4 (Reverse):  
- Reverse subarray from index `2` to `2` (no change).  

---

### Additional Example:

#### Input:
```java
arr = {3, 2, 1};
```

#### Step-by-Step Dry Run:
1. **Find `i`:**
   - `arr[2] = 1` and `arr[1] = 2` → `arr[1] >= arr[2]`, decrement `i`.
   - `arr[1] = 2` and `arr[0] = 3` → `arr[0] >= arr[1]`, decrement `i`.  
   - `i = -1`.

2. **No valid `i`:**
   - Reverse the entire array:  
     - Final `arr = {1, 2, 3}`.

#### Output:
```java
arr = {1, 2, 3};
```

---

### Complexity:

1. **Time Complexity:**  
   - Finding `i` and `j`: \( O(n) \).  
   - Reversing subarray: \( O(n) \).  
   - Total: \( O(n) \).

2. **Space Complexity:**  
   - \( O(1) \) (in-place).

This algorithm efficiently computes the next permutation with minimal overhead.