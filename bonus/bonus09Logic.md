### Code Recap:
```java

class Solution {
    int longestPrefixSuffix(String s) {
        int n = s.length();
        int[] lps = new int[n];
        
        // KMP pattern matching prefix function calculation
        int length = 0; // length of the previous longest prefix suffix
        int i = 1; // Start from the second character
        
        while (i < n) {
            if (s.charAt(i) == s.charAt(length)) {
                length++;
                lps[i] = length;
                i++;
            } else {
                if (length != 0) {
                    length = lps[length - 1]; // Try to find a shorter matching prefix
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
        
        // lps[n-1] will give us the longest prefix-suffix for the entire string
        return lps[n - 1];
    }
}
```


Here’s a dry run of the given `longestPrefixSuffix` function, which uses the KMP algorithm to calculate the longest proper prefix which is also a suffix for a given string.

Let's go step by step using an example string, `"abacab"`. The function uses an array `lps` to store the length of the longest proper prefix-suffix for each position in the string.

### Input:
```java
String s = "abacab";
```

### Step 1: Initialize
- `n = 6` (length of the string)
- `lps = [0, 0, 0, 0, 0, 0]` (Array to store the length of longest prefix-suffix at each position)
- `length = 0` (Length of the current longest proper prefix-suffix)
- `i = 1` (We start checking from the second character)

### Step 2: Begin the while loop (Start from `i = 1`):
- **Iteration 1 (`i = 1`)**:  
  - `s.charAt(1)` = `'b'`  
  - `s.charAt(0)` = `'a'`  
  - The characters don't match, so we check `length`. Since `length = 0`, set `lps[1] = 0` and increment `i`.
  - `lps = [0, 0, 0, 0, 0, 0]`
  - `i = 2`
  
- **Iteration 2 (`i = 2`)**:  
  - `s.charAt(2)` = `'a'`  
  - `s.charAt(0)` = `'a'`  
  - The characters match, so we increase `length` to 1 and set `lps[2] = 1`.
  - `lps = [0, 0, 1, 0, 0, 0]`
  - `i = 3`
  
- **Iteration 3 (`i = 3`)**:  
  - `s.charAt(3)` = `'c'`  
  - `s.charAt(1)` = `'b'`  
  - The characters don't match, so we check `length = 1`. We update `length = lps[length - 1] = lps[0] = 0`. This means we look for a shorter prefix.
  - Now `length = 0`, so `lps[3] = 0` and increment `i`.
  - `lps = [0, 0, 1, 0, 0, 0]`
  - `i = 4`
  
- **Iteration 4 (`i = 4`)**:  
  - `s.charAt(4)` = `'a'`  
  - `s.charAt(0)` = `'a'`  
  - The characters match, so we increase `length` to 1 and set `lps[4] = 1`.
  - `lps = [0, 0, 1, 0, 1, 0]`
  - `i = 5`
  
- **Iteration 5 (`i = 5`)**:  
  - `s.charAt(5)` = `'b'`  
  - `s.charAt(1)` = `'b'`  
  - The characters match, so we increase `length` to 2 and set `lps[5] = 2`.
  - `lps = [0, 0, 1, 0, 1, 2]`
  - `i = 6` (Exit loop since `i` equals `n`)

### Step 3: Final Result
- `lps[n - 1] = lps[5] = 2` (The longest prefix-suffix length for the string `"abacab"` is `2`)

### Explanation:
- The prefix `"ab"` (length 2) is also a suffix of the string `"abacab"`. This is why the longest prefix-suffix is `2`.
  
### Final Output:
```java
return lps[n - 1]; // Output is 2
```

### Dry Run Table

| i   | s[i]  | length (prefix-suffix length) | lps[]             | Explanation                                |
|-----|-------|-------------------------------|-------------------|--------------------------------------------|
| 1   | 'b'   | 0                             | [0, 0, 0, 0, 0, 0] | No match, so lps[1] = 0                    |
| 2   | 'a'   | 1                             | [0, 0, 1, 0, 0, 0] | Match, increase length to 1                |
| 3   | 'c'   | 0                             | [0, 0, 1, 0, 0, 0] | No match, set length to lps[0] = 0         |
| 4   | 'a'   | 1                             | [0, 0, 1, 0, 1, 0] | Match, increase length to 1                |
| 5   | 'b'   | 2                             | [0, 0, 1, 0, 1, 2] | Match, increase length to 2                |
| End |       | 2                             | [0, 0, 1, 0, 1, 2] | Finished processing, return lps[5] = 2     |

Thus, the function correctly returns `2` for the longest prefix-suffix in the string `"abacab"`.