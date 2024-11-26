Here’s a detailed dry run of the **array rotation** algorithm provided in the code, which rotates the array `d` times to the left using the **reversal algorithm**.

---

### Input Example:
```java
int[] arr = {1, 2, 3, 4, 5};
int d = 2;
```

---

### Steps in the Algorithm:

1. **Step 1:** Adjust `d` to handle cases where `d > n`:
   ```java
   d %= n;
   ```
   Here, \( n = 5 \), \( d = 2 \) (already less than \( n \)), so no change.

2. **Step 2:** Reverse the first `d` elements:
   ```java
   reverse(arr, 0, d - 1);
   ```
   Reverse elements from index `0` to `1`.

   - Initial `arr = {1, 2, 3, 4, 5}`.
   - Swap `arr[0]` with `arr[1]`.
   - Result: `arr = {2, 1, 3, 4, 5}`.

3. **Step 3:** Reverse the remaining `n - d` elements:
   ```java
   reverse(arr, d, n - 1);
   ```
   Reverse elements from index `2` to `4`.

   - Initial `arr = {2, 1, 3, 4, 5}`.
   - Swap `arr[2]` with `arr[4]`.
   - Result: `arr = {2, 1, 5, 4, 3}`.

4. **Step 4:** Reverse the entire array:
   ```java
   reverse(arr, 0, n - 1);
   ```
   Reverse elements from index `0` to `4`.

   - Initial `arr = {2, 1, 5, 4, 3}`.
   - Swap `arr[0]` with `arr[4]`: `arr = {3, 1, 5, 4, 2}`.
   - Swap `arr[1]` with `arr[3]`: `arr = {3, 4, 5, 1, 2}`.

---

### Final Output:
```java
arr = {3, 4, 5, 1, 2};
```

---

### Dry Run Summary:

#### **Initial Array:**
```plaintext
{1, 2, 3, 4, 5}
```

#### **Step 2 (Reverse First `d` Elements):**
```plaintext
{2, 1, 3, 4, 5}
```

#### **Step 3 (Reverse Last `n - d` Elements):**
```plaintext
{2, 1, 5, 4, 3}
```

#### **Step 4 (Reverse Entire Array):**
```plaintext
{3, 4, 5, 1, 2}
```

---

### Complexity Analysis:

1. **Time Complexity:**  
   - Each reverse operation takes \( O(\text{length of subarray}) \).
   - Total time: \( O(d) + O(n - d) + O(n) = O(n) \).

2. **Space Complexity:**  
   - No additional space is used beyond a few variables: \( O(1) \).

This algorithm efficiently rotates the array in \( O(n) \) time and \( O(1) \) space.

---

### Key Points:
- The **reversal algorithm** rotates the array by dividing it into three parts:
  1. Reverse the first `d` elements.
  2. Reverse the last `n - d` elements.
  3. Reverse the entire array.
- It avoids extra space by performing rotations in-place.