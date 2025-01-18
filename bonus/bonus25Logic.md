Here's a solution for converting a Roman numeral string to its integer equivalent in Java:

### Code:

```java
class Solution {
    // Finds decimal value of a given roman numeral
    public int romanToDecimal(String s) {
        // code here
        int[] values = new int[128];
        values['I'] = 1;
        values['V'] = 5;
        values['X'] = 10;
        values['L'] = 50;
        values['C'] = 100;
        values['D'] = 500;
        values['M'] = 1000;
        int result = 0;
        int n = s.length();
        
        for (int i = 0; i < n; i++) {
            int currentValues;
            currentValues = values[s.charAt(i)];
            if (i < n - 1 && currentValues < values[s.charAt(i + 1)]) {
                result -= currentValues;
            }else {
                result += currentValues;
            }
        }
        return result;
    }
}
```

### Explanation:
1. **Mapping Roman Numerals to Integers**:
   - We use an array `values` where each character from 'A' to 'Z' maps to an integer. Only the relevant Roman numeral characters ('I', 'V', 'X', 'L', 'C', 'D', 'M') are assigned values.

2. **Iterate from Right to Left**:
   - Starting from the rightmost character, we evaluate the value of the current Roman numeral.
   - If the current numeral's value is less than the previous numeral (e.g., 'I' before 'V' in "IV"), it is subtracted from the result.
   - Otherwise, it is added to the result.

3. **Update Previous Value**:
   - The `prevValue` variable keeps track of the last processed Roman numeral's value to handle the subtraction logic.

### Complexity:
- **Time Complexity**: \(O(n)\), where \(n\) is the length of the string. We process each character once.
- **Space Complexity**: \(O(1)\), as we use a fixed-size array for the mapping.

### Example Usage:
```java
public class Main {
    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.romanToDecimal("IX")); // Output: 9
        System.out.println(solution.romanToDecimal("XL")); // Output: 40
        System.out.println(solution.romanToDecimal("MCMIV")); // Output: 1904
    }
}
```

This code adheres to the constraints and ensures correct conversion of Roman numerals to integers.