### Approach:

To find the length of the longest substring with all distinct characters, we use a **sliding window** technique with a **HashMap** to track the last occurrence of each character.

---

### Steps:

1. **Initialization**:
   - Use a `HashMap<Character, Integer>` to store the last seen index of each character.
   - Maintain two pointers: 
     - `start`: the beginning of the sliding window.
     - `end`: the end of the sliding window, which moves through the string.
   - Initialize `maxLength = 0` to keep track of the maximum length of the substring.

2. **Iterate Over the String**:
   - For each character in the string:
     - If the character is already in the map **and** its last occurrence is **within or after the current window**:
       - Move the `start` pointer to one position after the last occurrence of the character.
     - Update the last occurrence of the character in the map.
     - Calculate the current length of the substring as `end - start + 1` and update `maxLength` if it's greater than the previous value.

3. **Return the Result**:
   - After the loop, return `maxLength`.

---

### Implementation:

```java
class Solution {
    public int longestUniqueSubstr(String s) {
        // HashMap to store the last occurrence of each character
        HashMap<Character, Integer> lastSeen = new HashMap<>();
        int maxLength = 0; // Variable to keep track of the maximum length
        int start = 0; // Start of the sliding window

        for (int end = 0; end < s.length(); end++) {
            char currentChar = s.charAt(end);

            // If the character is already in the map and its last occurrence is within the current window
            if (lastSeen.containsKey(currentChar) && lastSeen.get(currentChar) >= start) {
                start = lastSeen.get(currentChar) + 1; // Move the start to the next character
            }

            // Update the last occurrence of the character
            lastSeen.put(currentChar, end);

            // Update the maximum length
            maxLength = Math.max(maxLength, end - start + 1);
        }

        return maxLength;
    }
}
```

---

### Dry Run:

#### Input: `s = "geeksforgeeks"`

1. **Initialization**:
   - `lastSeen = {}` (empty map initially).
   - `start = 0, maxLength = 0`.

2. **Processing the string**:

| **Index (end)** | **Character** | **Window (start-end)** | **lastSeen Map**             | **maxLength** |
|------------------|---------------|-------------------------|------------------------------|---------------|
| 0                | g             | [0-0]                  | {g: 0}                      | 1             |
| 1                | e             | [0-1]                  | {g: 0, e: 1}                | 2             |
| 2                | e             | [2-2]                  | {g: 0, e: 2}                | 2             |
| 3                | k             | [2-3]                  | {g: 0, e: 2, k: 3}          | 2             |
| 4                | s             | [2-4]                  | {g: 0, e: 2, k: 3, s: 4}    | 3             |
| 5                | f             | [2-5]                  | {g: 0, e: 2, k: 3, s: 4, f: 5}| 4           |
| 6                | o             | [2-6]                  | {g: 0, e: 2, k: 3, s: 4, f: 5, o: 6}| 5    |
| 7                | r             | [2-7]                  | {g: 0, e: 2, k: 3, s: 4, f: 5, o: 6, r: 7}| 6|
| 8                | g             | [3-8]                  | {g: 8, e: 2, k: 3, s: 4, f: 5, o: 6, r: 7}| 6|
| 9                | e             | [3-9]                  | {g: 8, e: 9, k: 3, s: 4, f: 5, o: 6, r: 7}| 6|
| 10               | e             | [10-10]                | {g: 8, e: 10, k: 3, s: 4, f: 5, o: 6, r: 7}| 6|
| 11               | k             | [11-11]                | {g: 8, e: 10, k: 11, s: 4, f: 5, o: 6, r: 7}| 6|
| 12               | s             | [11-12]                | {g: 8, e: 10, k: 11, s: 12, f: 5, o: 6, r: 7}| 6|

**Output**: `7` (substring: "eksforg").

---

### Complexity:

1. **Time Complexity**:
   - Each character is visited at most twice (once when added to the map and once when removed from the window).
   - Total: \(O(n)\), where \(n\) is the length of the string.

2. **Space Complexity**:
   - The `HashMap` can store at most \(26\) keys (for lowercase English letters), so \(O(1)\) space in practical terms.
   - However, for generic characters, the space complexity is \(O(min(n, m))\), where \(m\) is the character set size.

---

This solution efficiently handles the problem and works well even for large inputs.