The given code calculates the **maximum profit** that can be obtained from a stock by buying and selling once. The idea is to track the **minimum price** encountered so far, and at each step, calculate the potential **profit** if the stock were sold at the current price. Let’s perform a **dry run** for the code.

---

### Example Input:
```java
prices = {7, 1, 5, 3, 6, 4}
```

---

### Initial Values:
- `minPrice = Integer.MAX_VALUE` (initially set to a very large value to ensure any price will be smaller).
- `maxProfit = 0` (initialize to 0, because initially no profit has been made).

---

### Step-by-Step Execution:

#### **Iteration 1: `price = 7`**
- **Update `minPrice`**: `minPrice = Math.min(Integer.MAX_VALUE, 7) = 7`.
- **Calculate profit**: `profit = 7 - 7 = 0`.
- **Update `maxProfit`**: `maxProfit = Math.max(0, 0) = 0`.
- Updated state:  
  ```plaintext
  minPrice = 7, maxProfit = 0
  ```

---

#### **Iteration 2: `price = 1`**
- **Update `minPrice`**: `minPrice = Math.min(7, 1) = 1`.
- **Calculate profit**: `profit = 1 - 1 = 0`.
- **Update `maxProfit`**: `maxProfit = Math.max(0, 0) = 0`.
- Updated state:  
  ```plaintext
  minPrice = 1, maxProfit = 0
  ```

---

#### **Iteration 3: `price = 5`**
- **Update `minPrice`**: `minPrice = Math.min(1, 5) = 1`.
- **Calculate profit**: `profit = 5 - 1 = 4`.
- **Update `maxProfit`**: `maxProfit = Math.max(0, 4) = 4`.
- Updated state:  
  ```plaintext
  minPrice = 1, maxProfit = 4
  ```

---

#### **Iteration 4: `price = 3`**
- **Update `minPrice`**: `minPrice = Math.min(1, 3) = 1`.
- **Calculate profit**: `profit = 3 - 1 = 2`.
- **Update `maxProfit`**: `maxProfit = Math.max(4, 2) = 4`.
- Updated state:  
  ```plaintext
  minPrice = 1, maxProfit = 4
  ```

---

#### **Iteration 5: `price = 6`**
- **Update `minPrice`**: `minPrice = Math.min(1, 6) = 1`.
- **Calculate profit**: `profit = 6 - 1 = 5`.
- **Update `maxProfit`**: `maxProfit = Math.max(4, 5) = 5`.
- Updated state:  
  ```plaintext
  minPrice = 1, maxProfit = 5
  ```

---

#### **Iteration 6: `price = 4`**
- **Update `minPrice`**: `minPrice = Math.min(1, 4) = 1`.
- **Calculate profit**: `profit = 4 - 1 = 3`.
- **Update `maxProfit`**: `maxProfit = Math.max(5, 3) = 5`.
- Updated state:  
  ```plaintext
  minPrice = 1, maxProfit = 5
  ```

---

### Final Output:
```java
maxProfit = 5
```

---

### Dry Run Summary:

#### Input:
```plaintext
prices = {7, 1, 5, 3, 6, 4}
```

#### Iterations:
| Price \(i\) | `minPrice` | Profit | `maxProfit` |
|-------------|------------|--------|-------------|
| 7           | 7          | 0      | 0           |
| 1           | 1          | 0      | 0           |
| 5           | 1          | 4      | 4           |
| 3           | 1          | 2      | 4           |
| 6           | 1          | 5      | 5           |
| 4           | 1          | 3      | 5           |

---

### Complexity Analysis:

1. **Time Complexity:**
   - The algorithm iterates through the `prices` array once: \( O(n) \).

2. **Space Complexity:**
   - Uses a fixed number of variables (`minPrice`, `maxProfit`): \( O(1) \).

---

### Key Points:
- The algorithm efficiently tracks the minimum price encountered and calculates the maximum profit possible in a single pass through the array.
- It doesn't require sorting or additional data structures, making it optimal for this problem.