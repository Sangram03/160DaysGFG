### Code Recap:
```java

class Solution {

    static void computeLPSArray(String s, int[] lps) {
        int len = 0, idx = 1;

        lps[0] = 0;

        while (idx < s.length()) {
            if (s.charAt(idx) == s.charAt(len)) {
                len++;
                lps[idx] = len;
                idx++;
            } else {

                if (len == 0) {
                    lps[idx] = 0;
                    idx++;
                } else {

                    len = lps[len - 1];
                }
            }
        }
    }

    static boolean KMPSearch(String txt, String pat, int[] lps, int rep) {
        int n = txt.length(), m = pat.length();
        int i = 0, j = 0;

        while (i < n * rep) {

            if (txt.charAt(i % n) == pat.charAt(j)) {
                i++;
                j++;

                if (j == m) {
                    return true;
                }
            } else {

                if (j != 0)
                    j = lps[j - 1];
                else
                    i++;
            }
        }
        return false;
    }

    static int minRepeats(String s1, String s2) {

        int n = s1.length();
        int m = s2.length();

        int[] lps = new int[m];
        computeLPSArray(s2, lps);

        int x = (m + n - 1) / n;

        if (KMPSearch(s1, s2, lps, x)) return x;

        if (KMPSearch(s1, s2, lps, x + 1)) return x + 1;

        return -1;
    }
};
```



Let’s dry run the given code with an example to understand how it works.

---

### Example
**Input**:  
`s1 = "abcd"`, `s2 = "cdabcdab"`

---

### Initial Setup:
1. `n = s1.length() = 4`  
   `m = s2.length() = 8`

2. Compute the LPS array for `s2 = "cdabcdab"`.

---

### Step 1: Compute the LPS Array
LPS (Longest Prefix Suffix) helps in optimizing the KMP pattern matching algorithm by storing information about matching prefixes and suffixes.

- `s2 = "cdabcdab"`
- `lps = [0, 0, 0, 1, 2, 3, 4, 0]`

**Explanation**:
- `lps[i]` represents the length of the longest proper prefix which is also a suffix in the substring `s2[0...i]`.

---

### Step 2: Calculate Minimum Repeats
1. Compute `x = (m + n - 1) / n = (8 + 4 - 1) / 4 = 2`  
   This means we initially test repeating `s1` **2 times**.

2. Check if `s2` can be found in `s1` repeated `x = 2` times using KMP search.

---

### Step 3: KMP Search for `x = 2`
We are searching for `s2 = "cdabcdab"` in `txt = "abcdabcd"` (repeated `s1` 2 times).

#### Matching Process:
- `txt = "abcdabcd"`, `pat = "cdabcdab"`.
- Initialize `i = 0`, `j = 0`.
- Iterate through `txt` until `i < n * rep = 8`.

1. **i = 0, j = 0**: `txt[0] = 'a'`, `pat[0] = 'c'` → Mismatch, increment `i = 1`.
2. **i = 1, j = 0**: `txt[1] = 'b'`, `pat[0] = 'c'` → Mismatch, increment `i = 2`.
3. **i = 2, j = 0**: `txt[2] = 'c'`, `pat[0] = 'c'` → Match, increment `i = 3`, `j = 1`.
4. **i = 3, j = 1**: `txt[3] = 'd'`, `pat[1] = 'd'` → Match, increment `i = 4`, `j = 2`.
5. **i = 4, j = 2**: `txt[4] = 'a'`, `pat[2] = 'a'` → Match, increment `i = 5`, `j = 3`.
6. **i = 5, j = 3**: `txt[5] = 'b'`, `pat[3] = 'b'` → Match, increment `i = 6`, `j = 4`.
7. **i = 6, j = 4**: `txt[6] = 'c'`, `pat[4] = 'c'` → Match, increment `i = 7`, `j = 5`.
8. **i = 7, j = 5**: `txt[7] = 'd'`, `pat[5] = 'd'` → Match, increment `i = 8`, `j = 6`.

- At this point, `i = 8` and `j < m`, meaning the pattern `s2` is **not fully matched**.

#### Result: KMP Search for `x = 2` returns `false`.

---

### Step 4: KMP Search for `x = 3`
Now, repeat `s1` 3 times and search for `s2` in `txt = "abcdabcdabcd"`.

#### Matching Process:
- `txt = "abcdabcdabcd"`, `pat = "cdabcdab"`.
- Initialize `i = 0`, `j = 0`.
- Iterate through `txt` until `i < n * rep = 12`.

1. Repeat steps 1–8 (as above). At `i = 8`, `j = 6`.
2. **i = 8, j = 6**: `txt[8] = 'a'`, `pat[6] = 'a'` → Match, increment `i = 9`, `j = 7`.
3. **i = 9, j = 7**: `txt[9] = 'b'`, `pat[7] = 'b'` → Match, increment `i = 10`, `j = 8`.

- At this point, `j = m = 8`, meaning the pattern `s2` is **fully matched**.

#### Result: KMP Search for `x = 3` returns `true`.

---

### Step 5: Return Result
- Since `x = 3` matches `s2`, return `x = 3`.

---

### Final Output
The minimum number of repeats required is **3**.