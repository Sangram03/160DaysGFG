# java
```java

class Solution {
    public List<int[]> mergeOverlap(int[][] arr) {
        // Edge case: if the input is empty, return an empty list
        if (arr.length == 0) {
            return new ArrayList<>();
        }
        
        // Step 1: Sort intervals based on the start of each interval
        Arrays.sort(arr, (a, b) -> a[0] - b[0]);
        
        // List to hold the merged intervals
        List<int[]> result = new ArrayList<>();
        
        // Step 2: Initialize the first interval
        int[] currentInterval = arr[0];
        
        // Step 3: Iterate over the intervals
        for (int i = 1; i < arr.length; i++) {
            // If the current interval overlaps with the next interval
            if (arr[i][0] <= currentInterval[1]) {
                // Merge them by extending the end time of the current interval
                currentInterval[1] = Math.max(currentInterval[1], arr[i][1]);
            } else {
                // No overlap, so add the current interval to the result list
                result.add(currentInterval);
                // Move to the next interval
                currentInterval = arr[i];
            }
        }
        
        // Add the last merged interval to the result
        result.add(currentInterval);
        
        return result;
    }
}


```


### Approach:

1. **Sort the Intervals**:
   - Sort the intervals based on their start times. This makes it easier to compare consecutive intervals to see if they overlap.

2. **Merge Overlapping Intervals**:
   - Start with the first interval and compare it with the next one. If the start of the next interval is less than or equal to the end of the current interval, they overlap, and you merge them by updating the end of the current interval to be the maximum of the two ends.
   - If the intervals don't overlap, just add the current interval to the result and move to the next one.

3. **Edge Case**:
   - If there's only one interval, it should be returned as it is.
   
### Steps:

1. **Sort** the intervals by the start time.
2. **Iterate** through the sorted intervals.
3. **Merge** if the current interval overlaps with the next one, else add the current interval to the result list.
4. **Return** the result.


Let's dry run the `mergeOverlap` method for a sample input to understand how it works step by step.

### Example Input:

```java
int[][] arr = {{1, 3}, {2, 4}, {6, 8}, {9, 10}};
```

### Step-by-Step Dry Run:

1. **Initial Setup:**
   - We start by checking if `arr` is empty. In this case, it's not, so we proceed.
   - We then sort the intervals based on their start time.

   **Sorted intervals:**
   ```java
   arr = {{1, 3}, {2, 4}, {6, 8}, {9, 10}};
   ```

2. **Initialization:**
   - We create a `result` list to store the merged intervals.
   - We initialize the first interval as `currentInterval = {1, 3}`.
   
3. **First Iteration (i = 1):**
   - Compare `arr[1] = {2, 4}` with `currentInterval = {1, 3}`.
   - Since the start of `arr[1]` (2) is less than or equal to the end of `currentInterval` (3), they overlap.
   - We merge them by updating `currentInterval[1]` to `Math.max(3, 4) = 4`. So, `currentInterval` becomes `{1, 4}`.
   
   **Current state after the first iteration:**
   ```java
   currentInterval = {1, 4}
   result = []
   ```

4. **Second Iteration (i = 2):**
   - Compare `arr[2] = {6, 8}` with `currentInterval = {1, 4}`.
   - Since the start of `arr[2]` (6) is greater than the end of `currentInterval` (4), there is no overlap.
   - We add `currentInterval = {1, 4}` to the `result` list.
   - Now, we update `currentInterval` to `arr[2] = {6, 8}`.
   
   **Current state after the second iteration:**
   ```java
   currentInterval = {6, 8}
   result = [{1, 4}]
   ```

5. **Third Iteration (i = 3):**
   - Compare `arr[3] = {9, 10}` with `currentInterval = {6, 8}`.
   - Since the start of `arr[3]` (9) is greater than the end of `currentInterval` (8), there is no overlap.
   - We add `currentInterval = {6, 8}` to the `result` list.
   - Now, we update `currentInterval` to `arr[3] = {9, 10}`.
   
   **Current state after the third iteration:**
   ```java
   currentInterval = {9, 10}
   result = [{1, 4}, {6, 8}]
   ```

6. **After Loop:**
   - After the loop ends, we add the last `currentInterval = {9, 10}` to the `result` list.
   
   **Final state:**
   ```java
   currentInterval = {9, 10}
   result = [{1, 4}, {6, 8}, {9, 10}]
   ```

### Final Output:
The method will return the `result` list:

```java
[{1, 4}, {6, 8}, {9, 10}]
```

### Summary of Key Steps:
1. The intervals are sorted based on the start time.
2. The first interval is initialized as `currentInterval`.
3. Each interval is compared to `currentInterval`:
   - If they overlap, they are merged by updating the end time of `currentInterval`.
   - If they don't overlap, `currentInterval` is added to the result, and the current interval becomes the new `currentInterval`.
4. The final `currentInterval` is added to the result at the end of the loop.

This is how the `mergeOverlap` function works, and the example input results in merging the intervals `[1, 3]` and `[2, 4]` into `[1, 4]`, while the other intervals remain separate.


