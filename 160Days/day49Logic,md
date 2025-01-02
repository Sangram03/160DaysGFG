# java
```java


class Solution {
    public int countSubarrays(int[] arr, int k) {
        // Initialize variables
        int count = 0;
        int sum = 0;

        // HashMap to store prefix sums and their frequencies
        HashMap<Integer, Integer> prefixSumMap = new HashMap<>();

        // Initialize the HashMap with a zero-sum prefix
        prefixSumMap.put(0, 1);

        // Iterate through the array
        for (int num : arr) {
            sum += num; // Update running sum

            // Check if (sum - k) exists in the map
            if (prefixSumMap.containsKey(sum - k)) {
                count += prefixSumMap.get(sum - k);
            }

            // Update the frequency of the current sum in the map
            prefixSumMap.put(sum, prefixSumMap.getOrDefault(sum, 0) + 1);
        }

        return count;
    }
}





```



To solve this problem, we can use the **Prefix Sum with HashMap** approach. This method efficiently computes the count of subarrays with the sum \( k \) in \( O(n) \) time complexity.

### Explanation
1. **Prefix Sum Concept**:
   - Maintain a running sum while iterating through the array.
   - For every element \( arr[i] \), calculate the cumulative sum \( sum \).
   - Check if \( sum - k \) exists in the hash map. If it exists, it indicates there are subarrays ending at index \( i \) that sum to \( k \).

2. **HashMap Usage**:
   - The hash map stores frequencies of the prefix sums encountered so far.
   - This allows for efficient checking and updating.

3. **Edge Cases**:
   - Handle cases where the subarray starts from the beginning of the array.
   - Handle negative numbers properly.

Let’s dry-run the given code to understand how it works step-by-step.  

### Input
```java
String[] arr = {"bat", "tab", "cat", "act", "tac"};
```

### Step-by-Step Execution

#### Initial Setup
1. Create a `LinkedHashMap` named `map` to group anagrams while preserving the insertion order:
   ```java
   LinkedHashMap<String, ArrayList<String>> map = new LinkedHashMap<>();
   ```
2. Initialize the result list at the end to store the groups:
   ```java
   ArrayList<ArrayList<String>> result = new ArrayList<>();
   ```

#### Iteration Over Strings in `arr`
##### Iteration 1: Process `"bat"`
1. Convert `"bat"` to a character array:  
   ```java
   char[] charArray = {'b', 'a', 't'};
   ```
2. Sort the array:  
   ```java
   charArray = {'a', 'b', 't'};
   ```
3. Create the sorted key:  
   ```java
   String sortedKey = "abt";
   ```
4. Check if `map` contains the key `"abt"`. It doesn’t, so create a new list and add `"bat"` to it:
   ```java
   map.put("abt", new ArrayList<>(Arrays.asList("bat")));
   ```
   **Map State**: `{ "abt": ["bat"] }`

##### Iteration 2: Process `"tab"`
1. Convert `"tab"` to a character array:  
   ```java
   char[] charArray = {'t', 'a', 'b'};
   ```
2. Sort the array:  
   ```java
   charArray = {'a', 'b', 't'};
   ```
3. Create the sorted key:  
   ```java
   String sortedKey = "abt";
   ```
4. Check if `map` contains the key `"abt"`. It does, so add `"tab"` to the existing list:
   ```java
   map.get("abt").add("tab");
   ```
   **Map State**: `{ "abt": ["bat", "tab"] }`

##### Iteration 3: Process `"cat"`
1. Convert `"cat"` to a character array:  
   ```java
   char[] charArray = {'c', 'a', 't'};
   ```
2. Sort the array:  
   ```java
   charArray = {'a', 'c', 't'};
   ```
3. Create the sorted key:  
   ```java
   String sortedKey = "act";
   ```
4. Check if `map` contains the key `"act"`. It doesn’t, so create a new list and add `"cat"` to it:
   ```java
   map.put("act", new ArrayList<>(Arrays.asList("cat")));
   ```
   **Map State**: `{ "abt": ["bat", "tab"], "act": ["cat"] }`

##### Iteration 4: Process `"act"`
1. Convert `"act"` to a character array:  
   ```java
   char[] charArray = {'a', 'c', 't'};
   ```
2. Sort the array:  
   ```java
   charArray = {'a', 'c', 't'};
   ```
3. Create the sorted key:  
   ```java
   String sortedKey = "act";
   ```
4. Check if `map` contains the key `"act"`. It does, so add `"act"` to the existing list:
   ```java
   map.get("act").add("act");
   ```
   **Map State**: `{ "abt": ["bat", "tab"], "act": ["cat", "act"] }`

##### Iteration 5: Process `"tac"`
1. Convert `"tac"` to a character array:  
   ```java
   char[] charArray = {'t', 'a', 'c'};
   ```
2. Sort the array:  
   ```java
   charArray = {'a', 'c', 't'};
   ```
3. Create the sorted key:  
   ```java
   String sortedKey = "act";
   ```
4. Check if `map` contains the key `"act"`. It does, so add `"tac"` to the existing list:
   ```java
   map.get("act").add("tac");
   ```
   **Map State**: `{ "abt": ["bat", "tab"], "act": ["cat", "act", "tac"] }`

#### Constructing the Result
1. Iterate over the values of `map` and add each group to `result`:
   ```java
   for (ArrayList<String> group : map.values()) {
       result.add(group);
   }
   ```
   **Result**:
   ```java
   [
       ["bat", "tab"],
       ["cat", "act", "tac"]
   ]
   ```

### Final Output
```java
[["bat", "tab"], ["cat", "act", "tac"]]
```