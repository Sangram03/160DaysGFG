### Approach:

To count the number of distinct elements in every window of size \(k\) in the array, we can use a **sliding window** approach along with a **hash map** to efficiently track the frequency of elements in the current window.

---

### Steps:

1. **Initialization**:
   - Create a `HashMap<Integer, Integer>` to store the frequency of elements in the current window.
   - Create an `ArrayList<Integer>` to store the results.

2. **Iterate Over the Array**:
   - For every element `arr[i]`:
     - Add it to the `freq` map and update its count.
     - If the index \(i\) is greater than or equal to \(k - 1\) (i.e., the first window is completed):
       - Add the size of the `freq` map (which gives the count of distinct elements) to the result list.
       - Remove the element going out of the window (`arr[i - k + 1]`) from the `freq` map:
         - Decrease its frequency count.
         - If the frequency becomes 0, remove the element from the map.

3. **Return the Results**:
   - Return the `res` list containing the count of distinct elements in each window.

---

### Implementation:

```java
class Solution {
    ArrayList<Integer> countDistinct(int arr[], int k) {
        // Frequency map for the current window
        HashMap<Integer, Integer> freq = new HashMap<>();
        // List to store the results
        ArrayList<Integer> res = new ArrayList<>();
        
        // Traverse the array
        for (int i = 0; i < arr.length; i++) {
            // Add the current element to the frequency map
            freq.put(arr[i], freq.getOrDefault(arr[i], 0) + 1);
            
            // Check if the window is complete
            if (i >= k - 1) {
                // Add the count of distinct elements in the current window
                res.add(freq.size());
                
                // Remove the element going out of the window
                int outElement = arr[i - k + 1];
                freq.put(outElement, freq.get(outElement) - 1);
                if (freq.get(outElement) == 0) {
                    freq.remove(outElement);
                }
            }
        }
        
        return res;
    }
}
```

---

### Dry Run:

#### Input: 
`arr[] = [1, 2, 1, 3, 4, 2, 3], k = 4`

1. **Initialization**:
   - `freq = {}` (empty map initially).
   - `res = []` (empty result list).

2. **Processing the array**:

| **i** | **Element** | **Window** | **freq map**               | **Distinct Count** | **res** |
|-------|-------------|------------|----------------------------|--------------------|---------|
| 0     | 1           | [1]        | {1: 1}                    | -                  | []      |
| 1     | 2           | [1, 2]     | {1: 1, 2: 1}              | -                  | []      |
| 2     | 1           | [1, 2, 1]  | {1: 2, 2: 1}              | -                  | []      |
| 3     | 3           | [1, 2, 1, 3]| {1: 2, 2: 1, 3: 1}        | 3                  | [3]     |
| 4     | 4           | [2, 1, 3, 4]| {2: 1, 1: 1, 3: 1, 4: 1}  | 4                  | [3, 4]  |
| 5     | 2           | [1, 3, 4, 2]| {1: 1, 3: 1, 4: 1, 2: 1}  | 4                  | [3, 4, 4]|
| 6     | 3           | [3, 4, 2, 3]| {3: 2, 4: 1, 2: 1}        | 3                  | [3, 4, 4, 3]|

**Output**: `[3, 4, 4, 3]`

---

### Complexity:

1. **Time Complexity**:
   - Traversing the array: \(O(n)\).
   - Each `put` and `remove` operation in the hash map is \(O(1)\) (amortized).
   - Total: \(O(n)\).

2. **Space Complexity**:
   - HashMap: Stores at most \(k\) elements, so \(O(k)\).

---

### Advantages:
- Efficient for large arrays due to \(O(n)\) time complexity.
- Simple to implement with a sliding window and hash map.