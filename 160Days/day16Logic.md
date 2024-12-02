# java
```java
class Solution {
    // Function is to check whether two strings are anagram of each other or not.
    public static boolean areAnagrams(String s1, String s2) {
        // Check if lengths are different
        if (s1.length() != s2.length()) {
            return false;
        }

        // Array to count frequency of characters (for lowercase alphabets)
        int[] charCount = new int[26];

        // Count frequency of characters in s1 and subtract frequency for s2
        for (int i = 0; i < s1.length(); i++) {
            charCount[s1.charAt(i) - 'a']++;
            charCount[s2.charAt(i) - 'a']--;
        }

        // Check if all counts are zero
        for (int count : charCount) {
            if (count != 0) {
                return false;
            }
        }

        return true; // Strings are anagrams
    }
}




```



### Dry Run of the Code

Let’s analyze the function `areAnagrams` with an example to understand its working.

#### Input:
- `s1 = "geeks"`
- `s2 = "kseeg"`

#### Step-by-Step Execution:

1. **Length Check**:
   - `s1.length() = 5`, `s2.length() = 5`. Since the lengths are equal, continue.

2. **Initialize Frequency Array**:
   - `charCount = [0, 0, 0, ..., 0]` (size 26, all initialized to 0).

3. **Traverse Both Strings Simultaneously**:
   - For each index `i` in the strings:
     - Update the frequency array for characters in `s1` and `s2`.

| Iteration | `s1.charAt(i)` | `s2.charAt(i)` | `charCount` Updates                           |
|-----------|----------------|----------------|-----------------------------------------------|
| `i = 0`   | `'g'`          | `'k'`          | Increment at `'g'` (`+1` at index 6), Decrement at `'k'` (`-1` at index 10). |
| `i = 1`   | `'e'`          | `'s'`          | Increment at `'e'` (`+1` at index 4), Decrement at `'s'` (`-1` at index 18). |
| `i = 2`   | `'e'`          | `'e'`          | Increment and decrement at `'e'` (net change 0). |
| `i = 3`   | `'k'`          | `'e'`          | Increment at `'k'` (`+1` at index 10), Decrement at `'e'` (`-1` at index 4). |
| `i = 4`   | `'s'`          | `'g'`          | Increment at `'s'` (`+1` at index 18), Decrement at `'g'` (`-1` at index 6). |

   - After all iterations:
     ```
     charCount = [0, 0, 0, ..., 0]  // All values are 0
     ```

4. **Check All Counts are Zero**:
   - Traverse `charCount`. Since all counts are zero, the strings are anagrams.

5. **Return Result**:
   - Return `true`.

---

### Approach:

1. **Check Lengths**:
   - If the lengths of the strings are not equal, they cannot be anagrams.

2. **Frequency Array**:
   - Create an array of size 26 to store the frequency of each character.
   - Traverse both strings simultaneously:
     - Increment the count for the character in `s1`.
     - Decrement the count for the character in `s2`.

3. **Verify Zero Counts**:
   - After processing both strings, if all elements in the frequency array are zero, the strings are anagrams.

---

### Why This Works:
- By incrementing for `s1` and decrementing for `s2`, the frequency array effectively compares the counts of characters in both strings.
- If the strings are anagrams, the net change for each character will be zero.

---

### Complexity:
- **Time Complexity**: \(O(n)\), where \(n\) is the length of the strings.
  - Single traversal of both strings and a constant-time check of the frequency array.
- **Space Complexity**: \(O(1)\).
  - Fixed size array (26) is used for frequency counting.