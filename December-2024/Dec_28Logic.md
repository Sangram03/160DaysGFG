### **Approach to Find All Triplets with Zero Sum**

The goal is to find all triplets in an array such that the sum of the elements in the triplet equals zero. We'll ensure the triplets are unique and in sorted order \(i < j < k\).

---

### **Naive Approach**:
1. Use three nested loops to check every possible combination of triplets.
2. For each triplet, check if their sum equals zero. If yes, add the triplet indices to the result.

---

### **Optimal Approach (Two Pointers Method)**:
A more efficient approach involves sorting the array and using the two-pointer technique to reduce complexity.

---

### **Steps for Two-Pointer Approach**:

1. **Sort the Array**:
   - Sort the array in ascending order. This ensures we can systematically find triplets using two pointers.

2. **Iterate Through the Array**:
   - For each element \(arr[i]\), fix it as the first element of the triplet.
   - Use two pointers:
     - `left` starting at \(i+1\) (next element after \(arr[i]\)).
     - `right` starting at the end of the array.
   - Calculate the sum of the triplet:
     - If the sum is zero, add the triplet to the result list.
     - If the sum is less than zero, increment `left` to increase the sum.
     - If the sum is greater than zero, decrement `right` to decrease the sum.

3. **Handle Duplicates**:
   - Skip duplicate elements while iterating to ensure unique triplets.

4. **Return the Result**:
   - Return the list of all triplets.

---

### **Complexity**:
- **Time Complexity**: \(O(n^2)\)  
  - Sorting the array takes \(O(n \log n)\), and the two-pointer traversal for each element is \(O(n)\), making it \(O(n^2)\) in total.
- **Space Complexity**: \(O(1)\)  
  - Apart from the result list, no extra space is used.

---

### **Code Implementation**:

```java

class Solution {
    public List<List<Integer>> findTriplets(int[] arr) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(arr); // Step 1: Sort the array
        int n = arr.length;

        for (int i = 0; i < n - 2; i++) {
            // Skip duplicate elements for the first element
            if (i > 0 && arr[i] == arr[i - 1]) continue;

            int left = i + 1, right = n - 1;
            while (left < right) {
                int sum = arr[i] + arr[left] + arr[right];

                if (sum == 0) {
                    res.add(Arrays.asList(i, left, right));
                    left++;
                    right--;

                    // Skip duplicates for second and third elements
                    while (left < right && arr[left] == arr[left - 1]) left++;
                    while (left < right && arr[right] == arr[right + 1]) right--;
                } else if (sum < 0) {
                    left++; // Increase the sum
                } else {
                    right--; // Decrease the sum
                }
            }
        }

        return res;
    }
}
```

---

### **Dry Run**

#### Input:
```java
arr = [0, -1, 2, -3, 1];
```

---

#### Sorted Array:
```java
arr = [-3, -1, 0, 1, 2];
```

---

#### Execution:

1. **i = 0** (\(arr[i] = -3\)):
   - \(left = 1\), \(right = 4\):
     - \(sum = -3 + (-1) + 2 = -2\) (\(sum < 0\)), move \(left = 2\).
   - \(left = 2\), \(right = 4\):
     - \(sum = -3 + 0 + 2 = -1\) (\(sum < 0\)), move \(left = 3\).
   - \(left = 3\), \(right = 4\):
     - \(sum = -3 + 1 + 2 = 0\) (\(sum = 0\)), add triplet: \([-3, 1, 2]\).
     - Move \(left = 4\), \(right = 3\) (terminate loop).

2. **i = 1** (\(arr[i] = -1\)):
   - \(left = 2\), \(right = 4\):
     - \(sum = -1 + 0 + 2 = 1\) (\(sum > 0\)), move \(right = 3\).
   - \(left = 2\), \(right = 3\):
     - \(sum = -1 + 0 + 1 = 0\) (\(sum = 0\)), add triplet: \([-1, 0, 1]\).
     - Move \(left = 3\), \(right = 2\) (terminate loop).

3. **i = 2** (\(arr[i] = 0\)):
   - \(left = 3\), \(right = 4\):
     - \(sum = 0 + 1 + 2 = 3\) (\(sum > 0\)), move \(right = 3\) (terminate loop).

---

### **Output**:
```java
[[-3, 1, 2], [-1, 0, 1]]


```



### Approach 2


```java

class Solution {
    public List<List<Integer>> findTriplets(int[] arr) {
        List<List<Integer>> res = new ArrayList<>();
        int n = arr.length;

        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (arr[i] + arr[j] + arr[k] == 0) {
                        res.add(Arrays.asList(i, j, k));
                    }
                }
            }
        }

        return res;
    }
}
```




### **Dry Run of the Code**

#### **Input**:
```java
arr = [0, -1, 2, -3, 1];
```

#### **Execution**:

**Step 1**: Initialize `res = []` to store the results.  
Set `n = 5` (length of `arr`).

---

#### Outer Loop (`i = 0`):
- **`arr[i] = 0`**

---

##### Inner Loop (`j = 1`):
- **`arr[j] = -1`**

---

###### Nested Loop (`k = 2`):
- **`arr[k] = 2`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = 0 + (-1) + 2 = 1\) (not zero, skip).

---

###### Nested Loop (`k = 3`):
- **`arr[k] = -3`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = 0 + (-1) + (-3) = -4\) (not zero, skip).

---

###### Nested Loop (`k = 4`):
- **`arr[k] = 1`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = 0 + (-1) + 1 = 0\) (valid triplet).  
  - Add **\([0, 1, 4]\)** to `res`.

---

##### Inner Loop (`j = 2`):
- **`arr[j] = 2`**

---

###### Nested Loop (`k = 3`):
- **`arr[k] = -3`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = 0 + 2 + (-3) = -1\) (not zero, skip).

---

###### Nested Loop (`k = 4`):
- **`arr[k] = 1`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = 0 + 2 + 1 = 3\) (not zero, skip).

---

##### Inner Loop (`j = 3`):
- **`arr[j] = -3`**

---

###### Nested Loop (`k = 4`):
- **`arr[k] = 1`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = 0 + (-3) + 1 = -2\) (not zero, skip).

---

#### Outer Loop (`i = 1`):
- **`arr[i] = -1`**

---

##### Inner Loop (`j = 2`):
- **`arr[j] = 2`**

---

###### Nested Loop (`k = 3`):
- **`arr[k] = -3`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = -1 + 2 + (-3) = -2\) (not zero, skip).

---

###### Nested Loop (`k = 4`):
- **`arr[k] = 1`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = -1 + 2 + 1 = 2\) (not zero, skip).

---

##### Inner Loop (`j = 3`):
- **`arr[j] = -3`**

---

###### Nested Loop (`k = 4`):
- **`arr[k] = 1`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = -1 + (-3) + 1 = -3\) (not zero, skip).

---

#### Outer Loop (`i = 2`):
- **`arr[i] = 2`**

---

##### Inner Loop (`j = 3`):
- **`arr[j] = -3`**

---

###### Nested Loop (`k = 4`):
- **`arr[k] = 1`**  
  - **Sum**: \(arr[i] + arr[j] + arr[k] = 2 + (-3) + 1 = 0\) (valid triplet).  
  - Add **\([2, 3, 4]\)** to `res`.

---

#### Outer Loop (`i = 3`):
- The inner loop does not execute as \(j = 4\) is out of bounds.

---

#### Outer Loop (`i = 4`):
- The inner loop does not execute as \(j = 5\) is out of bounds.

---

#### **Final Result**:
`res = [[0, 1, 4], [2, 3, 4]]`

---

### **Output**:
```java
[[0, 1, 4], [2, 3, 4]]
```