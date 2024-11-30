Here's the detailed dry run for the **nextPermutation** algorithm.

---

# java
```java
class Solution {
    void nextPermutation(int[] arr) {
        int n = arr.length;
        int i = n - 2, j = n - 1;

        while (i >= 0 && arr[i] >= arr[i + 1])
            i--;

        if (i >= 0) {

            while (arr[j] <= arr[i])
                j--;

            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }

        reverse(arr, i + 1, n - 1);
    }

    void reverse(int[] arr, int start, int end) {
        while (start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }
}
```






Let’s dry-run the given `nextPermutation` algorithm step by step for clarity.

### Example Input
```java
arr = [1, 2, 3]
```

### Step 1: Find the First Decreasing Element
1. Start at `i = n - 2` (i.e., `i = 1`).
   - Compare `arr[i]` (2) and `arr[i+1]` (3). Since `2 < 3`, stop the loop.
   - Now, `i = 1`.

### Step 2: Find the Element to Swap
1. Start at `j = n - 1` (i.e., `j = 2`).
   - Compare `arr[j]` (3) and `arr[i]` (2). Since `3 > 2`, stop the loop.
   - Now, `j = 2`.

### Step 3: Swap `arr[i]` and `arr[j]`
1. Swap `arr[i]` and `arr[j]`:
   - `arr[1] = 2`, `arr[2] = 3`.
   - After swapping, `arr = [1, 3, 2]`.

### Step 4: Reverse the Remaining Array
1. Reverse the subarray from `i+1` to `n-1` (i.e., `reverse(arr, 2, 2)`).
   - Since `start == end`, no changes are made.
   - Final `arr = [1, 3, 2]`.

### Final Output
The next permutation of `[1, 2, 3]` is `[1, 3, 2]`.

---

### Another Example
```java
arr = [3, 2, 1]
```

### Step 1: Find the First Decreasing Element
1. Start at `i = n - 2` (i.e., `i = 1`).
   - Compare `arr[1]` (2) and `arr[2]` (1). Since `2 >= 1`, decrement `i`.
   - Compare `arr[0]` (3) and `arr[1]` (2). Since `3 >= 2`, decrement `i`.
   - Now, `i = -1`.

### Step 2: No Valid `i` Found
1. Since `i < 0`, skip the swapping step.

### Step 3: Reverse the Entire Array
1. Reverse the subarray from `0` to `n-1` (i.e., `reverse(arr, 0, 2)`).
   - Swap `arr[0]` (3) and `arr[2]` (1): `arr = [1, 2, 3]`.
   - Final `arr = [1, 2, 3]`.

### Final Output
The next permutation of `[3, 2, 1]` is `[1, 2, 3]`.

This implementation correctly generates the next lexicographical permutation or resets to the smallest permutation if the input is the largest.