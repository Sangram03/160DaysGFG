# java
```java

class Solution {
    public static int minChar(String s) {
        // Create the concatenated string: s + '#' + reverse(s)
        String reversed = new StringBuilder(s).reverse().toString();
        String temp = s + "#" + reversed;

        // Compute the LPS (longest prefix suffix) array
        int lps[] = computeLPS(temp);

        // Minimum characters to add at the front
        return s.length() - lps[temp.length() - 1];
    }

    private static int[] computeLPS(String pattern) {
        int n = pattern.length();
        int[] lps = new int[n];
        int length = 0;
        int i = 1;

        while (i < n) {
            if (pattern.charAt(i) == pattern.charAt(length)) {
                length++;
                lps[i] = length;
                i++;
            } else {
                if (length != 0) {
                    length = lps[length - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }

        return lps;
    }
}





```


### Dry Run of the Code

#### Input:
`s = "abc"`

---

#### Step-by-Step Execution:

1. **Reverse the String**:
   - `reversed = "cba"`

2. **Create Concatenated String**:
   - `temp = "abc#cba"`

3. **Compute LPS Array for `temp`**:

   - **Initialization**:
     - `n = temp.length() = 7`
     - `lps = [0, 0, 0, 0, 0, 0, 0]` (initial LPS array)
     - `length = 0`, `i = 1`

   - **Iteration**:
     
     **i = 1**:
     - Compare `temp[1]` (`b`) and `temp[length]` (`a`). They do not match.
     - Since `length == 0`, set `lps[1] = 0` and increment `i`.

     **i = 2**:
     - Compare `temp[2]` (`c`) and `temp[length]` (`a`). They do not match.
     - Since `length == 0`, set `lps[2] = 0` and increment `i`.

     **i = 3**:
     - Compare `temp[3]` (`#`) and `temp[length]` (`a`). They do not match.
     - Since `length == 0`, set `lps[3] = 0` and increment `i`.

     **i = 4**:
     - Compare `temp[4]` (`c`) and `temp[length]` (`a`). They do not match.
     - Since `length == 0`, set `lps[4] = 0` and increment `i`.

     **i = 5**:
     - Compare `temp[5]` (`b`) and `temp[length]` (`a`). They do not match.
     - Since `length == 0`, set `lps[5] = 0` and increment `i`.

     **i = 6**:
     - Compare `temp[6]` (`a`) and `temp[length]` (`a`). They match.
     - Increment `length` to 1, set `lps[6] = 1`, and increment `i`.

   - Final `lps` array: `[0, 0, 0, 0, 0, 0, 1]`

4. **Compute Minimum Characters to Add**:
   - `lps[temp.length() - 1] = lps[6] = 1`
   - Minimum characters to add = `s.length() - lps[temp.length() - 1] = 3 - 1 = 2`

---

### Output:
- **Result**: `2`

---

### Explanation:
To make `"abc"` a palindrome, we need to add two characters (`"cb"`) at the front to form `"cbabc"`.