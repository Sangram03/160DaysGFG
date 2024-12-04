# java
```java


class Solution {
    // Function to check if two strings are rotations of each other or not.
    public static boolean areRotations(String s1, String s2) {
        // Check if lengths are equal
        if (s1.length() != s2.length()) {
            return false;
        }
        // Concatenate s1 with itself
        String combined = s1 + s1;
        // Use KMP for substring search
        return kmpSearch(combined, s2);
    }

    // KMP substring search function
    private static boolean kmpSearch(String text, String pattern) {
        int[] lps = computeLPSArray(pattern);
        int i = 0, j = 0; // i for text, j for pattern
        
        while (i < text.length()) {
            if (text.charAt(i) == pattern.charAt(j)) {
                i++;
                j++;
                if (j == pattern.length()) {
                    return true; // Found a match
                }
            } else {
                if (j > 0) {
                    j = lps[j - 1]; // Use LPS to skip unnecessary comparisons
                } else {
                    i++;
                }
            }
        }
        return false; // No match found
    }

    // Function to compute the LPS (Longest Prefix Suffix) array for KMP
    private static int[] computeLPSArray(String pattern) {
        int[] lps = new int[pattern.length()];
        int len = 0, i = 1;

        while (i < pattern.length()) {
            if (pattern.charAt(i) == pattern.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len > 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
        return lps;
    }

    public static void main(String[] args) {
        // Test cases
        System.out.println(areRotations("abcd", "cdab")); // Output: true
        System.out.println(areRotations("aab", "aba"));   // Output: true
        System.out.println(areRotations("abcd", "acbd")); // Output: false
    }
}



```


Let’s perform a **dry run** for the given code with the example test cases to understand its behavior:

---

### Test Case 1: `areRotations("abcd", "cdab")`

1. **Check lengths**:
   - `s1.length() = 4`, `s2.length() = 4` → Lengths are equal, proceed.

2. **Concatenate `s1`**:
   - `combined = "abcd" + "abcd" = "abcdabcd"`

3. **Call `kmpSearch("abcdabcd", "cdab")`**:
   - **Compute LPS array for `"cdab"`**:
     - `lps = [0, 0, 0, 0]` (No repeated prefix-suffix patterns).
   - **KMP Matching**:
     - `i = 0, j = 0`: No match.
     - `i = 1, j = 0`: No match.
     - `i = 2, j = 0`: Match (`combined[2] == pattern[0]`), increment `i` and `j`.
     - `i = 3, j = 1`: Match (`combined[3] == pattern[1]`), increment `i` and `j`.
     - `i = 4, j = 2`: Match (`combined[4] == pattern[2]`), increment `i` and `j`.
     - `i = 5, j = 3`: Match (`combined[5] == pattern[3]`), `j == pattern.length()` → Match found, return `true`.

**Result**: `true`

---

### Test Case 2: `areRotations("aab", "aba")`

1. **Check lengths**:
   - `s1.length() = 3`, `s2.length() = 3` → Lengths are equal, proceed.

2. **Concatenate `s1`**:
   - `combined = "aab" + "aab" = "aabaab"`

3. **Call `kmpSearch("aabaab", "aba")`**:
   - **Compute LPS array for `"aba"`**:
     - `lps = [0, 0, 1]` (last character repeats the first).
   - **KMP Matching**:
     - `i = 0, j = 0`: Match (`combined[0] == pattern[0]`), increment `i` and `j`.
     - `i = 1, j = 1`: No match, use `lps` → `j = lps[j - 1] = 0`.
     - `i = 2, j = 0`: Match (`combined[2] == pattern[0]`), increment `i` and `j`.
     - `i = 3, j = 1`: Match (`combined[3] == pattern[1]`), increment `i` and `j`.
     - `i = 4, j = 2`: Match (`combined[4] == pattern[2]`), `j == pattern.length()` → Match found, return `true`.

**Result**: `true`

---

### Test Case 3: `areRotations("abcd", "acbd")`

1. **Check lengths**:
   - `s1.length() = 4`, `s2.length() = 4` → Lengths are equal, proceed.

2. **Concatenate `s1`**:
   - `combined = "abcd" + "abcd" = "abcdabcd"`

3. **Call `kmpSearch("abcdabcd", "acbd")`**:
   - **Compute LPS array for `"acbd"`**:
     - `lps = [0, 0, 0, 0]` (No repeated prefix-suffix patterns).
   - **KMP Matching**:
     - `i = 0, j = 0`: Match (`combined[0] == pattern[0]`), increment `i` and `j`.
     - `i = 1, j = 1`: No match, use `lps` → `j = 0`.
     - Continue comparison; no match found after checking all positions in `combined`.

**Result**: `false`

---

### Final Output
```plaintext
true
true
false
```