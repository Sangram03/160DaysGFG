### **Approach**

To solve this problem, we aim to form two numbers using all the digits in the array such that the sum of these two numbers is minimized. Here's the step-by-step approach:

1. **Sort the Array:**  
   - By sorting the array, we can distribute smaller digits to both numbers first, ensuring a minimized sum.

2. **Distribute Digits:**  
   - Use a toggle mechanism to alternate appending digits between the two numbers (`num1` and `num2`). This ensures the digits are balanced between the two numbers.

3. **Handle Leading Zeros:**  
   - Ensure no number has leading zeros. Skip appending `0` to an empty string unless the number itself is zero.

4. **Add the Two Numbers:**  
   - Use a helper function (`findSum`) to compute the sum of the two numbers represented as strings to avoid integer overflow issues.

5. **Return the Result:**  
   - Return the computed sum as a string, ensuring no leading zeros.

---




### **Code:**
```java

class Solution {
    public String minSum(int[] arr) {
        Arrays.sort(arr);
        StringBuilder num1 = new StringBuilder();
        StringBuilder num2 = new StringBuilder();
        boolean toggle = true;

        for (int num : arr) {
            if (toggle) {
                if (!(num == 0 && num1.length() == 0)) {
                    num1.append(num);
                }
            } else {
                if (!(num == 0 && num2.length() == 0)) {
                    num2.append(num);
                }
            }
            toggle = !toggle;
        }

        if (num1.length() == 0) num1.append("0");
        if (num2.length() == 0) num2.append("0");

        return findSum(num1.toString(), num2.toString());
    }

    private String findSum(String str1, String str2) {
        int n1 = str1.length(), n2 = str2.length();
        int carry = 0;
        StringBuilder result = new StringBuilder();

        for (int i = 0; i < Math.max(n1, n2) || carry > 0; i++) {
            int digit1 = i < n1 ? str1.charAt(n1 - i - 1) - '0' : 0;
            int digit2 = i < n2 ? str2.charAt(n2 - i - 1) - '0' : 0;
            int sum = digit1 + digit2 + carry;
            result.append(sum % 10);
            carry = sum / 10;
        }

        return result.reverse().toString();
    }
}
```


### **Dry Run**

#### Input:  
`arr[] = [6, 8, 4, 5, 2, 3]`

#### Execution Steps:
1. **Sort the Array:**  
   After sorting, `arr = [2, 3, 4, 5, 6, 8]`.

2. **Distribute Digits Between `num1` and `num2`:**
   - Initialize `num1 = ""`, `num2 = ""`, and `toggle = true`.
   - Iterating through `arr`:
     - `2`: Append to `num1` → `num1 = "2"`.
     - `3`: Append to `num2` → `num2 = "3"`.
     - `4`: Append to `num1` → `num1 = "24"`.
     - `5`: Append to `num2` → `num2 = "35"`.
     - `6`: Append to `num1` → `num1 = "246"`.
     - `8`: Append to `num2` → `num2 = "358"`.

3. **Sum the Two Numbers (`findSum`):**
   - Inputs: `str1 = "246"`, `str2 = "358"`.
   - Reverse strings: `str1 = "642"`, `str2 = "853"`.
   - Perform digit-wise addition with carry:
     - `6 + 8 = 14` → Append `4`, Carry `1`.
     - `4 + 5 + 1 = 10` → Append `0`, Carry `1`.
     - `2 + 3 + 1 = 6` → Append `6`, Carry `0`.
   - Result (reversed): `"604"` → Final result: `"604"`.

#### Output:  
`"604"`

---

### **Explanation of Example Outputs**

1. **Example 1:**  
   Input: `arr = [6, 8, 4, 5, 2, 3]`  
   Output: `"604"`  
   Explanation: Numbers formed are `246` and `358`. Their sum is `604`.

2. **Example 2:**  
   Input: `arr = [5, 3, 0, 7, 4]`  
   Output: `"82"`  
   Explanation: Numbers formed are `35` and `47`. Their sum is `82`.

3. **Example 3:**  
   Input: `arr = [9, 4]`  
   Output: `"13"`  
   Explanation: Numbers formed are `9` and `4`. Their sum is `13`.