# java
```java

class Solution {
    ArrayList<Integer> search(String pat, String txt) {
        ArrayList<Integer> result = new ArrayList<>();
        int m = pat.length(); // Length of the pattern
        int n = txt.length(); // Length of the text
        int base = 256; // Number of characters in the input alphabet
        int mod = 101; // A prime number to avoid overflow in hash computation

        if (m > n) return result; // If pattern length is greater than text length

        // Compute the hash value of the pattern and the first window of text
        int patHash = 0, txtHash = 0, h = 1;

        // The value of h would be "pow(base, m-1) % mod"
        for (int i = 0; i < m - 1; i++) {
            h = (h * base) % mod;
        }

        // Calculate initial hash values for pattern and first window of text
        for (int i = 0; i < m; i++) {
            patHash = (base * patHash + pat.charAt(i)) % mod;
            txtHash = (base * txtHash + txt.charAt(i)) % mod;
        }

        // Slide the pattern over the text
        for (int i = 0; i <= n - m; i++) {
            // Check if the hash values match
            if (patHash == txtHash) {
                // Verify the actual strings to avoid false positives due to hash collision
                if (txt.substring(i, i + m).equals(pat)) {
                    result.add(i); // Add 0-based index
                }
            }

            // Compute the hash value for the next window of text
            if (i < n - m) {
                txtHash = (base * (txtHash - txt.charAt(i) * h) + txt.charAt(i + m)) % mod;

                // If we get a negative hash, convert it to positive
                if (txtHash < 0) {
                    txtHash += mod;
                }
            }
        }

        return result;
    }

    // Test the function
    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.search("geek", "geeksforgeeks")); // Output: [0, 8]
        System.out.println(sol.search("aaa", "aaaaaa"));         // Output: [0, 1, 2, 3]
        System.out.println(sol.search("xyz", "abcdef"));         // Output: []
    }
}




```



Let’s walk through a dry run of your Rabin-Karp implementation for clarity. We'll use the test case:

**Input:**  
`pat = "geek"`  
`txt = "geeksforgeeks"`

---

### **Step-by-Step Execution**
#### Initialization:
- `m = 4` (length of pattern)  
- `n = 13` (length of text)  
- `base = 256`  
- `mod = 101`  
- `h = (base^(m-1)) % mod = (256^3) % 101 = 5` (calculated iteratively)

#### Compute Initial Hash Values:
- Compute the hash of `pat`:
  - `patHash = (256 * 0 + 'g') % 101 = 2`
  - `patHash = (256 * 2 + 'e') % 101 = 10`
  - `patHash = (256 * 10 + 'e') % 101 = 39`
  - `patHash = (256 * 39 + 'k') % 101 = 43`

- Compute the hash of the first window of `txt` (`"geek"`):
  - `txtHash = (256 * 0 + 'g') % 101 = 2`
  - `txtHash = (256 * 2 + 'e') % 101 = 10`
  - `txtHash = (256 * 10 + 'e') % 101 = 39`
  - `txtHash = (256 * 39 + 'k') % 101 = 43`

---

### **Sliding Window Matching**

1. **Window 1: `"geek"` (Indices 0 to 3)**
   - `patHash == txtHash` (43 == 43).  
   - Verify the substring: `"geek" == "geek"`. Match found! Add index `0` to `result`.

2. **Window 2: `"eeks"` (Indices 1 to 4)**
   - Update `txtHash`:
     - `txtHash = (256 * (43 - 'g' * 5) + 's') % 101`
     - `txtHash = (256 * (43 - 530) + 115) % 101 = 50`
   - `patHash != txtHash` (43 != 50). No match.

3. **Window 3: `"eksf"` (Indices 2 to 5)**
   - Update `txtHash`:
     - `txtHash = (256 * (50 - 'e' * 5) + 'f') % 101`
     - `txtHash = (256 * (50 - 505) + 102) % 101 = 31`
   - `patHash != txtHash` (43 != 31). No match.

4. **Continue Sliding...**

   Similarly, the algorithm slides the pattern across the text. Matches are found only when `txtHash` matches `patHash` **and** substring verification passes.

---

### **Final Match**

1. **Window 9: `"geek"` (Indices 8 to 11)**
   - Update `txtHash`:
     - `txtHash = (256 * (14 - 's' * 5) + 'k') % 101 = 43`
   - `patHash == txtHash` (43 == 43).  
   - Verify substring: `"geek" == "geek"`. Match found! Add index `8` to `result`.

---

### **Output**

The algorithm completes its iterations and returns:

**Output:** `[0, 8]`

---

### **Key Points**
1. **Efficiency:** The rolling hash avoids recomputing hash values for overlapping substrings.
2. **Collision Handling:** Hash matches are verified with actual substring comparisons.
3. **Complexity:** 
   - Preprocessing: \(O(m)\) (hash computation).  
   - Matching: \(O(n)\) (sliding the pattern).

Let me know if you want to walk through additional test cases!