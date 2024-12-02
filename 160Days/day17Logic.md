# java
```java
class Solution {
    // Function to find the first non-repeating character in a string.
    static char nonRepeatingChar(String s) {
        // Step 1: Create an array to store character frequencies
        int[] freq = new int[26]; // For lowercase Latin letters
        
        // Step 2: Count the frequency of each character
        for (char c : s.toCharArray()) {
            freq[c - 'a']++;
        }

        // Step 3: Find the first non-repeating character
        for (char c : s.toCharArray()) {
            if (freq[c - 'a'] == 1) {
                return c; // Return the first non-repeating character
            }
        }

        // Step 4: If no non-repeating character, return '$'
        return '$';
    }
    
    // Test the function
    public static void main(String[] args) {
        System.out.println(nonRepeatingChar("geeksforgeeks")); // Output: 'f'
        System.out.println(nonRepeatingChar("racecar"));       // Output: 'e'
        System.out.println(nonRepeatingChar("aabbccc"));       // Output: '$'
    }
}




```


Let's do a **dry run** of the code for the input `"geeksforgeeks"` to understand its working step by step.

---

### Input: `"geeksforgeeks"`

#### Step 1: Frequency Count
- Initialize an array `freq[26]` with all values set to 0.

Traverse the string and count the frequency of each character:
- `'g'`: `freq['g' - 'a'] = freq[6]++` → `freq[6] = 1`
- `'e'`: `freq['e' - 'a'] = freq[4]++` → `freq[4] = 1`
- `'e'`: `freq[4]++` → `freq[4] = 2`
- `'k'`: `freq['k' - 'a'] = freq[10]++` → `freq[10] = 1`
- `'s'`: `freq['s' - 'a'] = freq[18]++` → `freq[18] = 1`
- `'f'`: `freq['f' - 'a'] = freq[5]++` → `freq[5] = 1`
- `'o'`: `freq['o' - 'a'] = freq[14]++` → `freq[14] = 1`
- `'r'`: `freq['r' - 'a'] = freq[17]++` → `freq[17] = 1`
- `'g'`: `freq[6]++` → `freq[6] = 2`
- `'e'`: `freq[4]++` → `freq[4] = 3`
- `'e'`: `freq[4]++` → `freq[4] = 4`
- `'k'`: `freq[10]++` → `freq[10] = 2`
- `'s'`: `freq[18]++` → `freq[18] = 2`

Final `freq` array (only non-zero values):
- `freq[4] = 4` (`'e'`)
- `freq[5] = 1` (`'f'`)
- `freq[6] = 2` (`'g'`)
- `freq[10] = 2` (`'k'`)
- `freq[14] = 1` (`'o'`)
- `freq[17] = 1` (`'r'`)
- `freq[18] = 2` (`'s'`)

---

#### Step 2: Find First Non-Repeating Character
- Traverse the string again and check `freq` for each character:
  - `'g'`: `freq[6] = 2` → Repeated
  - `'e'`: `freq[4] = 4` → Repeated
  - `'e'`: `freq[4] = 4` → Repeated
  - `'k'`: `freq[10] = 2` → Repeated
  - `'s'`: `freq[18] = 2` → Repeated
  - `'f'`: `freq[5] = 1` → Non-repeating!

Return `'f'`.

---

### Output: `'f'`

---

### Dry Run for `"racecar"`

#### Step 1: Frequency Count
- `'r'`: `freq[17] = 1`
- `'a'`: `freq[0] = 1`
- `'c'`: `freq[2] = 1`
- `'e'`: `freq[4] = 1`
- `'c'`: `freq[2] = 2`
- `'a'`: `freq[0] = 2`
- `'r'`: `freq[17] = 2`

Final `freq` array:
- `freq[0] = 2` (`'a'`)
- `freq[2] = 2` (`'c'`)
- `freq[4] = 1` (`'e'`)
- `freq[17] = 2` (`'r'`)

---

#### Step 2: Find First Non-Repeating Character
- `'r'`: `freq[17] = 2` → Repeated
- `'a'`: `freq[0] = 2` → Repeated
- `'c'`: `freq[2] = 2` → Repeated
- `'e'`: `freq[4] = 1` → Non-repeating!

Return `'e'`.

---

### Dry Run for `"aabbccc"`

#### Step 1: Frequency Count
- `'a'`: `freq[0] = 2`
- `'b'`: `freq[1] = 2`
- `'c'`: `freq[2] = 3`

---

#### Step 2: Find First Non-Repeating Character
- `'a'`: `freq[0] = 2` → Repeated
- `'b'`: `freq[1] = 2` → Repeated
- `'c'`: `freq[2] = 3` → Repeated

No non-repeating character found. Return `'$'`.

---

### Outputs:
1. `"geeksforgeeks"` → `'f'`
2. `"racecar"` → `'e'`
3. `"aabbccc"` → `'$'`