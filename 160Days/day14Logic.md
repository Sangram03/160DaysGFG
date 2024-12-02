# java
```java
class Solution {
    public int myAtoi(String s) {
        // Constants for 32-bit signed integer range
        int INT_MAX = Integer.MAX_VALUE; // 2^31 - 1
        int INT_MIN = Integer.MIN_VALUE; // -2^31
        
        // Step 1: Handle empty string
        if (s == null || s.length() == 0) {
            return 0;
        }
        
        // Step 2: Skip leading whitespaces
        int i = 0;
        int n = s.length();
        while (i < n && s.charAt(i) == ' ') {
            i++;
        }
        
        // If we have reached the end of the string
        if (i == n) {
            return 0;
        }
        
        // Step 3: Check for sign
        int sign = 1;
        if (s.charAt(i) == '+') {
            i++;
        } else if (s.charAt(i) == '-') {
            sign = -1;
            i++;
        }
        
        // Step 4: Convert digits to integer
        int num = 0;
        while (i < n && Character.isDigit(s.charAt(i))) {
            int digit = s.charAt(i) - '0'; // Convert char to digit
            
            // Step 5: Handle overflow
            if (num > (INT_MAX - digit) / 10) {
                return (sign == 1) ? INT_MAX : INT_MIN;
            }
            
            num = num * 10 + digit;
            i++;
        }
        
        // Step 6: Return the result with the sign
        return num * sign;
    }
}

```


### Approach

This implementation of `myAtoi` follows a step-by-step approach to convert the input string into an integer while ensuring it adheres to the constraints and handles edge cases. Here's the breakdown:

1. **Skip Leading Whitespaces**:
   - Use a loop to ignore any whitespace characters until a valid character is found.
   
2. **Check for Sign**:
   - Determine if the number is positive or negative by checking for `+` or `-`.
   - If no sign is found, assume the number is positive.

3. **Read Digits and Construct the Number**:
   - Process each character if it's a digit.
   - Convert the character to its integer value (`char - '0'`) and append it to the result.

4. **Handle Overflow**:
   - Before adding a new digit, check if the result will exceed the 32-bit signed integer range.
   - Return `INT_MAX` or `INT_MIN` as appropriate if overflow is detected.

5. **Stop at Non-Digit Characters**:
   - Terminate the loop when a non-digit character is encountered.

6. **Return the Result**:
   - Combine the constructed number with its sign and return it.

---

### Dry Run

#### Example 1: `"   -42"`

1. **Input**: `"   -42"`
2. **Step 1: Skip Whitespaces**:
   - Initial pointer `i = 0`.
   - Skip leading spaces, pointer moves to `i = 3`.
3. **Step 2: Check for Sign**:
   - `s.charAt(3) == '-'`, so `sign = -1`, and pointer moves to `i = 4`.
4. **Step 3: Convert Digits**:
   - `s.charAt(4) == '4'`: `digit = 4`, `num = 0 * 10 + 4 = 4`.
   - `s.charAt(5) == '2'`: `digit = 2`, `num = 4 * 10 + 2 = 42`.
   - Next character is out of bounds or non-digit.
5. **Step 4: Apply Sign**:
   - `num = 42 * -1 = -42`.
6. **Output**: `-42`.

---

#### Example 2: `"4193 with words"`

1. **Input**: `"4193 with words"`
2. **Step 1: Skip Whitespaces**:
   - No leading spaces, pointer remains at `i = 0`.
3. **Step 2: Check for Sign**:
   - No sign, default `sign = 1`.
4. **Step 3: Convert Digits**:
   - `s.charAt(0) == '4'`: `digit = 4`, `num = 0 * 10 + 4 = 4`.
   - `s.charAt(1) == '1'`: `digit = 1`, `num = 4 * 10 + 1 = 41`.
   - `s.charAt(2) == '9'`: `digit = 9`, `num = 41 * 10 + 9 = 419`.
   - `s.charAt(3) == '3'`: `digit = 3`, `num = 419 * 10 + 3 = 4193`.
   - Next character is a non-digit.
5. **Step 4: Apply Sign**:
   - `num = 4193 * 1 = 4193`.
6. **Output**: `4193`.

---

#### Example 3: `"   -91283472332"`

1. **Input**: `"   -91283472332"`
2. **Step 1: Skip Whitespaces**:
   - Skip leading spaces, pointer moves to `i = 3`.
3. **Step 2: Check for Sign**:
   - `s.charAt(3) == '-'`, so `sign = -1`, pointer moves to `i = 4`.
4. **Step 3: Convert Digits**:
   - Process digits until overflow occurs:
     - `num = 9`, `num = 91`, `num = 912`, ... exceeds `(INT_MAX - digit) / 10`.
   - Return `INT_MIN = -2147483648` due to overflow.
5. **Output**: `-2147483648`.

---

### Complexity Analysis

1. **Time Complexity**:
   - \(O(n)\), where \(n\) is the length of the input string.
   - Each character is processed once.

2. **Space Complexity**:
   - \(O(1)\), as no additional data structures are used.

This approach efficiently handles all edge cases like leading/trailing spaces, overflow, non-digit characters, and signs.