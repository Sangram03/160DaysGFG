# java
```java

class Solution {
    static int minRemoval(int intervals[][]) {
        // Step 1: Sort intervals by their end times
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[1], b[1]));

        // Step 2: Initialize variables
        int removed = 0; // Count of intervals to remove
        int prevEnd = Integer.MIN_VALUE; // Tracks the end time of the last non-overlapping interval

        // Step 3: Iterate through intervals
        for (int[] interval : intervals) {
            if (interval[0] >= prevEnd) {
                // Non-overlapping case: update prevEnd
                prevEnd = interval[1];
            } else {
                // Overlapping case: increment removal counter
                removed++;
            }
        }

        // Step 4: Return the total number of removals
        return removed;
    }
}



```
The problem of removing the minimum number of intervals to make the rest non-overlapping can be solved efficiently using a **greedy algorithm**. Here's the step-by-step approach:

---

### Approach:

1. **Sort the Intervals by End Time:**
   - Sort the given intervals based on their ending times. This helps in always keeping the smallest ending interval, which minimizes overlaps.

2. **Iterate Through the Sorted Intervals:**
   - Keep track of the `end` of the last added interval to the non-overlapping set.
   - For each interval, check if it overlaps with the previously added interval:
     - If it doesn't overlap, update `end` to the current interval's end time.
     - If it overlaps, increment a counter for removed intervals.

3. **Output the Number of Removed Intervals:**
   - The counter gives the number of intervals removed.



Let’s dry-run the code with an example to see how it works step by step. We’ll use the input:

### Input:
```java
intervals = [[1, 2], [2, 3], [3, 4], [1, 3]]
```

---

### Step 1: Sort Intervals
The intervals are sorted by their end times:

```java
[[1, 2], [1, 3], [2, 3], [3, 4]]
```

---

### Step 2: Initialize Variables
- `removed = 0`
- `prevEnd = Integer.MIN_VALUE`

---

### Step 3: Iterate Through Intervals

#### Iteration 1:
- Current interval: `[1, 2]`
- Condition: `1 >= Integer.MIN_VALUE` (True)
- Action: Update `prevEnd = 2`
- Removed count remains `0`.

#### Iteration 2:
- Current interval: `[1, 3]`
- Condition: `1 >= 2` (False)
- Action: Increment `removed`. New `removed = 1`.

#### Iteration 3:
- Current interval: `[2, 3]`
- Condition: `2 >= 2` (True)
- Action: Update `prevEnd = 3`.
- Removed count remains `1`.

#### Iteration 4:
- Current interval: `[3, 4]`
- Condition: `3 >= 3` (True)
- Action: Update `prevEnd = 4`.
- Removed count remains `1`.

---

### Step 4: Return the Result
The total number of intervals removed is:

```java
return 1;
```

---

### Output:
For the input `[[1, 2], [2, 3], [3, 4], [1, 3]]`, the output is:

```
1
```

This aligns with the problem’s explanation that removing `[1, 3]` ensures the rest of the intervals are non-overlapping.

--- 

You can similarly dry-run the code with other examples to verify its correctness. Let me know if you'd like to try with another input!