# java
```java
class Solution {
    public String addBinary(String s1, String s2) {
        StringBuilder result = new StringBuilder();
        int i = s1.length() - 1; // Pointer for s1
        int j = s2.length() - 1; // Pointer for s2
        int carry = 0;           // Initialize carry
        
        // Traverse both strings from right to left
        while (i >= 0 || j >= 0 || carry > 0) {
            int bit1 = (i >= 0) ? s1.charAt(i--) - '0' : 0; // Get bit from s1 or 0
            int bit2 = (j >= 0) ? s2.charAt(j--) - '0' : 0; // Get bit from s2 or 0
            
            int sum = bit1 + bit2 + carry; // Add bits and carry
            result.append(sum % 2);       // Append the resulting bit (sum % 2)
            carry = sum / 2;              // Calculate new carry
        }
        
        // Reverse the result string
        result.reverse();
        
        // Remove leading zeros
        while (result.length() > 1 && result.charAt(0) == '0') {
            result.deleteCharAt(0);
        }
        
        return result.toString();
    }
}



```

Let's perform a **dry run** of the `addBinary` method with an example input to understand how it works step by step.

---

### Example Input:
```java
s1 = "1101";
s2 = "111";
```

---

### Initial Setup:
- `i = s1.length() - 1 = 3`
- `j = s2.length() - 1 = 2`
- `carry = 0`
- `result = ""` (empty string, will use `StringBuilder`)

---

### Step-by-Step Execution:

#### **1st Iteration**:
- **Bits at current positions**:
  - `bit1 = s1.charAt(3) - '0' = 1`
  - `bit2 = s2.charAt(2) - '0' = 1`
  - `carry = 0`
  
- **Sum**:
  - `sum = bit1 + bit2 + carry = 1 + 1 + 0 = 2`
  - Append `sum % 2 = 0` to `result` → `result = "0"`
  - Update `carry = sum / 2 = 1`

- **Update Pointers**:
  - `i = 2`, `j = 1`

---

#### **2nd Iteration**:
- **Bits at current positions**:
  - `bit1 = s1.charAt(2) - '0' = 0`
  - `bit2 = s2.charAt(1) - '0' = 1`
  - `carry = 1`
  
- **Sum**:
  - `sum = bit1 + bit2 + carry = 0 + 1 + 1 = 2`
  - Append `sum % 2 = 0` to `result` → `result = "00"`
  - Update `carry = sum / 2 = 1`

- **Update Pointers**:
  - `i = 1`, `j = 0`

---

#### **3rd Iteration**:
- **Bits at current positions**:
  - `bit1 = s1.charAt(1) - '0' = 1`
  - `bit2 = s2.charAt(0) - '0' = 1`
  - `carry = 1`
  
- **Sum**:
  - `sum = bit1 + bit2 + carry = 1 + 1 + 1 = 3`
  - Append `sum % 2 = 1` to `result` → `result = "001"`
  - Update `carry = sum / 2 = 1`

- **Update Pointers**:
  - `i = 0`, `j = -1`

---

#### **4th Iteration**:
- **Bits at current positions**:
  - `bit1 = s1.charAt(0) - '0' = 1`
  - `bit2 = 0` (since `j = -1`, out of bounds)
  - `carry = 1`
  
- **Sum**:
  - `sum = bit1 + bit2 + carry = 1 + 0 + 1 = 2`
  - Append `sum % 2 = 0` to `result` → `result = "0010"`
  - Update `carry = sum / 2 = 1`

- **Update Pointers**:
  - `i = -1`, `j = -1`

---

#### **5th Iteration**:
- **Bits at current positions**:
  - `bit1 = 0` (since `i = -1`, out of bounds)
  - `bit2 = 0` (since `j = -1`, out of bounds)
  - `carry = 1`
  
- **Sum**:
  - `sum = bit1 + bit2 + carry = 0 + 0 + 1 = 1`
  - Append `sum % 2 = 1` to `result` → `result = "00101"`
  - Update `carry = sum / 2 = 0`

- **Update Pointers**:
  - `i = -2`, `j = -2`

---

### Final Result:
- **Result Before Reversing**: `"00101"`
- **After Reversing**: `"10100"`

---

### Output:
```java
System.out.println(solution.addBinary("1101", "111")); // Output: "10100"
```

---

### Key Observations:
1. The algorithm handles mismatched string lengths naturally by treating out-of-bound bits as `0`.
2. The carry ensures correctness for cases where the sum exceeds 1.
3. Reversing at the end gives the correct result since the sum is calculated from the least significant bit (rightmost).