# java
```java
class Solution {
    static ArrayList<int[]> insertInterval(int[][] intervals, int[] newInterval) {
        ArrayList<int[]> result = new ArrayList<>();
        int i = 0; 
        int n = intervals.length;

        // Add all intervals that come before the newInterval
        while (i < n && intervals[i][1] < newInterval[0]) {
            result.add(intervals[i]);
            i++;
        }

        // Merge overlapping intervals
        while (i < n && intervals[i][0] <= newInterval[1]) {
            newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
            newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
            i++;
        }
        result.add(newInterval);

        // Add remaining intervals
        while (i < n) {
            result.add(intervals[i]);
            i++;
        }

        return result;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        try {
            // Read the number of intervals
            if (!sc.hasNextInt()) {
                System.out.println("No input provided");
                return;
            }
            int n = sc.nextInt();

            // Read the intervals
            int[][] intervals = new int[n][2];
            for (int i = 0; i < n; i++) {
                intervals[i][0] = sc.nextInt();
                intervals[i][1] = sc.nextInt();
            }

            // Read the new interval
            int[] newInterval = new int[2];
            newInterval[0] = sc.nextInt();
            newInterval[1] = sc.nextInt();

            // Process the intervals
            ArrayList<int[]> result = insertInterval(intervals, newInterval);

            // Print the result
            for (int[] interval : result) {
                System.out.println(interval[0] + " " + interval[1]);
            }
        } catch (NoSuchElementException e) {
            System.out.println("Invalid input or input format");
        } finally {
            sc.close(); // Ensure the scanner is closed
        }
    }
}



```

To solve this problem, we need to efficiently insert the new interval while merging any overlapping intervals. Here’s a step-by-step approach:

### Algorithm
1. **Iterate Through Existing Intervals**:
   - If the current interval ends before the new interval starts, add the interval to the result as it doesn't overlap.
   - If the current interval starts after the new interval ends, add the new interval to the result and reset it as the current interval. This ensures newInterval is added only once in the correct position.
   - If the intervals overlap, merge them by updating the new interval to cover the union of both.

2. **Add Remaining Intervals**:
   - After processing all intervals, if `newInterval` hasn't been added, append it to the result.

3. **Complexity**:
   - Time complexity: \(O(n)\), as we iterate through the intervals once.
   - Space complexity: \(O(n)\), for storing the result.



Let’s walk through a **dry run** of the `insertInterval` function in the `Solution` class with an example:

---

### Input:

- **Intervals**: `[[1, 3], [6, 9]]`
- **New Interval**: `[2, 5]`

---

### Step-by-Step Execution:

#### Step 1: Initializing Variables
- **Result List**: `[]` (Initially empty).
- **Index (`i`)**: `0`.
- **Number of Intervals (`n`)**: `2` (since there are 2 intervals in the input).

---

#### Step 2: Adding Non-Overlapping Intervals (Before `newInterval`)
- Loop condition: `while (i < n && intervals[i][1] < newInterval[0])`

**Iteration 1**:
- `intervals[i][1]` = `3`, and `newInterval[0]` = `2`.
- Condition `3 < 2` is **false**.
- **No intervals are added to the result list** in this step.

---

#### Step 3: Merging Overlapping Intervals
- Loop condition: `while (i < n && intervals[i][0] <= newInterval[1])`

**Iteration 1**:
- `intervals[i][0]` = `1`, and `newInterval[1]` = `5`.
- Condition `1 <= 5` is **true**.
  - Update `newInterval[0]` to `min(1, 2) = 1`.
  - Update `newInterval[1]` to `max(3, 5) = 5`.
- `newInterval` is now `[1, 5]`.
- Increment `i` to `1`.

**Iteration 2**:
- `intervals[i][0]` = `6`, and `newInterval[1]` = `5`.
- Condition `6 <= 5` is **false**.
- Exit the loop.

**Add the merged interval** `[1, 5]` to the result list:
- **Result**: `[[1, 5]]`.

---

#### Step 4: Adding Remaining Intervals
- Loop condition: `while (i < n)`

**Iteration 1**:
- Add `intervals[1]` = `[6, 9]` to the result list.
- Increment `i` to `2`.

**Result**: `[[1, 5], [6, 9]]`.

---

### Final Output
The merged intervals are:
```
1 5
6 9
```

---

### Additional Test Cases:

#### **Case 1**: No Overlap
**Input**:
- Intervals: `[[1, 2], [3, 5], [6, 7]]`
- New Interval: `[8, 10]`

**Output**:
```
1 2
3 5
6 7
8 10
```

---

#### **Case 2**: Full Overlap
**Input**:
- Intervals: `[[1, 5], [10, 15]]`
- New Interval: `[0, 20]`

**Output**:
```
0 20
```

---
