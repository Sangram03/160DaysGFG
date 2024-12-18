To solve the problem of allocating books to minimize the maximum pages assigned to any student, we can use a binary search approach combined with a feasibility check.

Here's the plan:

### Algorithm:
1. **Check Edge Cases:**
   - If the number of students \( k \) exceeds the number of books \( n \), return \(-1\), as it's not possible to assign at least one book to each student.

2. **Binary Search Setup:**
   - The lower bound for the search (\( \text{low} \)) is the maximum number of pages in a single book, because at least one student will need to read that book.
   - The upper bound (\( \text{high} \)) is the sum of all pages in the array, representing the case where one student reads all books.

3. **Feasibility Function:**
   - For a given maximum \( \text{pagesLimit} \), check if it's possible to allocate books to \( k \) students such that no student gets more than \( \text{pagesLimit} \) pages.

4. **Binary Search for the Optimal Allocation:**
   - Perform binary search on the range \([ \text{low}, \text{high} ]\).
   - If allocation is feasible for a mid-point \( \text{mid} \), try for a smaller maximum by updating \( \text{high} = \text{mid} - 1 \).
   - Otherwise, increase \( \text{low} \) to \( \text{mid} + 1 \).

5. **Return Result:**
   - The smallest feasible \( \text{mid} \) during the binary search is the answer.

### Java Code:
```java
class Solution {
    public static int findPages(int[] arr, int k) {
        int n = arr.length;

        // Edge case: If students are more than books
        if (k > n) {
            return -1;
        }

        int low = 0, high = 0;
        for (int pages : arr) {
            low = Math.max(low, pages); // Maximum single book pages
            high += pages;             // Sum of all pages
        }

        int result = -1;
        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (isFeasible(arr, n, k, mid)) {
                result = mid;         // Found a possible solution
                high = mid - 1;       // Try for smaller maximum
            } else {
                low = mid + 1;        // Increase the maximum limit
            }
        }

        return result;
    }

    // Helper function to check feasibility of current maxPages
    private static boolean isFeasible(int[] arr, int n, int k, int maxPages) {
        int studentsRequired = 1;
        int currentSum = 0;

        for (int pages : arr) {
            if (currentSum + pages > maxPages) {
                // Assign new student
                studentsRequired++;
                currentSum = pages;

                // If students required exceed available, return false
                if (studentsRequired > k) {
                    return false;
                }
            } else {
                currentSum += pages;
            }
        }

        return true;
    }
}
```

### Explanation of Code:
1. **Binary Search:**
   - We iteratively reduce the search range for the minimum possible maximum.

2. **Feasibility Check:**
   - The `isFeasible` function ensures that the books can be allocated to students within the current limit of \( \text{maxPages} \).

3. **Edge Cases Handled:**
   - More students than books.
   - Arrays with only one book or one student.

### Complexity:
- **Time Complexity:**
  - Binary search requires \( O(\log(\text{sum of pages})) \).
  - For each feasibility check, we iterate through the array, which is \( O(n) \).
  - Total: \( O(n \cdot \log(\text{sum of pages})) \).
- **Space Complexity:**
  - \( O(1) \), as no extra space is used.

### Dry Run for `findPages` Method

#### Example Input:
- `arr = [12, 34, 67, 90]`
- `k = 2`

#### Step-by-Step Execution:

---

**Step 1:** Initialization
- `n = 4` (number of books).
- `low = 90` (maximum single book pages, the largest element in `arr`).
- `high = 203` (sum of all pages in `arr`).
- `result = -1`.

---

**Step 2:** Binary Search
- Perform binary search on range `[90, 203]`.

---

**Iteration 1:** `mid = 90 + (203 - 90) / 2 = 146`
- Check if `isFeasible(arr, n, k, maxPages = 146)`:

    **Feasibility Check:**
    - `studentsRequired = 1`, `currentSum = 0`.
    - Loop through `arr`:
        1. `currentSum = 12` (add `arr[0]`).
        2. `currentSum = 46` (add `arr[1]`).
        3. `currentSum = 113` (add `arr[2]`).
        4. `currentSum + arr[3] = 113 + 90 > 146`. Assign a new student:
            - `studentsRequired = 2`, `currentSum = 90`.
    - Allocation is feasible (`studentsRequired = 2 ≤ k`).

    **Result:**
    - Feasible, update `result = 146`.
    - Update `high = 145`.

---

**Iteration 2:** `mid = 90 + (145 - 90) / 2 = 117`
- Check if `isFeasible(arr, n, k, maxPages = 117)`:

    **Feasibility Check:**
    - `studentsRequired = 1`, `currentSum = 0`.
    - Loop through `arr`:
        1. `currentSum = 12` (add `arr[0]`).
        2. `currentSum = 46` (add `arr[1]`).
        3. `currentSum = 113` (add `arr[2]`).
        4. `currentSum + arr[3] = 113 + 90 > 117`. Assign a new student:
            - `studentsRequired = 2`, `currentSum = 90`.
    - Allocation is feasible (`studentsRequired = 2 ≤ k`).

    **Result:**
    - Feasible, update `result = 117`.
    - Update `high = 116`.

---

**Iteration 3:** `mid = 90 + (116 - 90) / 2 = 103`
- Check if `isFeasible(arr, n, k, maxPages = 103)`:

    **Feasibility Check:**
    - `studentsRequired = 1`, `currentSum = 0`.
    - Loop through `arr`:
        1. `currentSum = 12` (add `arr[0]`).
        2. `currentSum = 46` (add `arr[1]`).
        3. `currentSum = 113` (add `arr[2]`), exceeds 103:
            - Assign a new student:
            - `studentsRequired = 2`, `currentSum = 67`.
        4. `currentSum + arr[3] = 67 + 90 > 103`. Assign another new student:
            - `studentsRequired = 3 > k`. Allocation not feasible.

    **Result:**
    - Not feasible, update `low = 104`.

---

**Iteration 4:** `mid = 104 + (116 - 104) / 2 = 110`
- Check if `isFeasible(arr, n, k, maxPages = 110)`:

    **Feasibility Check:**
    - `studentsRequired = 1`, `currentSum = 0`.
    - Loop through `arr`:
        1. `currentSum = 12` (add `arr[0]`).
        2. `currentSum = 46` (add `arr[1]`).
        3. `currentSum = 113` (add `arr[2]`), exceeds 110:
            - Assign a new student:
            - `studentsRequired = 2`, `currentSum = 67`.
        4. `currentSum + arr[3] = 67 + 90 > 110`. Assign another new student:
            - `studentsRequired = 3 > k`. Allocation not feasible.

    **Result:**
    - Not feasible, update `low = 111`.

---

**Iteration 5:** `mid = 111 + (116 - 111) / 2 = 113`
- Check if `isFeasible(arr, n, k, maxPages = 113)`:

    **Feasibility Check:**
    - `studentsRequired = 1`, `currentSum = 0`.
    - Loop through `arr`:
        1. `currentSum = 12` (add `arr[0]`).
        2. `currentSum = 46` (add `arr[1]`).
        3. `currentSum = 113` (add `arr[2]`), exactly 113.
        4. `currentSum + arr[3] = 113 + 90 > 113`. Assign a new student:
            - `studentsRequired = 2`, `currentSum = 90`.
    - Allocation is feasible (`studentsRequired = 2 ≤ k`).

    **Result:**
    - Feasible, update `result = 113`.
    - Update `high = 112`.

---

**Iteration 6:** `mid = 111 + (112 - 111) / 2 = 111`
- Check if `isFeasible(arr, n, k, maxPages = 111)`:

    **Feasibility Check:**
    - `studentsRequired = 1`, `currentSum = 0`.
    - Loop through `arr`:
        1. `currentSum = 12` (add `arr[0]`).
        2. `currentSum = 46` (add `arr[1]`).
        3. `currentSum = 113` (add `arr[2]`), exceeds 111:
            - Assign a new student:
            - `studentsRequired = 2`, `currentSum = 67`.
        4. `currentSum + arr[3] = 67 + 90 > 111`. Assign another new student:
            - `studentsRequired = 3 > k`. Allocation not feasible.

    **Result:**
    - Not feasible, update `low = 112`.

---

**Iteration 7:** `mid = 112`
- Check if `isFeasible(arr, n, k, maxPages = 112)`:

    **Feasibility Check:**
    - Same as above. Not feasible.

    **Result:**
    - Not feasible, update `low = 113`.

---

**End of Binary Search:**
- `low = high = 113`.
- Return `result = 113`.

---

**Final Output:**
- **Output:** `113`