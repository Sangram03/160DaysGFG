# java
```java
class Solution {
    public ArrayList<ArrayList<String>> anagrams(String[] arr) {
        // Map to group anagrams
        LinkedHashMap<String, ArrayList<String>> map = new LinkedHashMap<>();

        // Iterate over each string in the input array
        for (String str : arr) {
            // Sort the characters of the string to create a key
            char[] charArray = str.toCharArray();
            Arrays.sort(charArray);
            String sortedKey = new String(charArray);

            // Add the string to the group corresponding to the sorted key
            map.putIfAbsent(sortedKey, new ArrayList<>());
            map.get(sortedKey).add(str);
        }

        // Prepare the result, maintaining the order of first appearance
        ArrayList<ArrayList<String>> result = new ArrayList<>();
        for (ArrayList<String> group : map.values()) {
            result.add(group);
        }

        return result;
    }
}




```



Let's perform a **dry run** of the provided code with the example input:

### Input:
```java
arr = ["act", "god", "cat", "dog", "tac"]
```

### Step-by-Step Execution:
#### Initial Setup:
1. `map`: Initialize an empty `LinkedHashMap`.
2. `result`: Initialize an empty `ArrayList<ArrayList<String>>`.

#### Iteration Over `arr`:

**Iteration 1** (`str = "act"`):
- Convert `str` to a character array: `charArray = ['a', 'c', 't']`.
- Sort `charArray`: `sortedKey = "act"`.
- Check `map`:
  - `sortedKey` ("act") is not present, so add it with a new list.
  - `map = {"act": ["act"]}`.

---

**Iteration 2** (`str = "god"`):
- Convert `str` to a character array: `charArray = ['g', 'o', 'd']`.
- Sort `charArray`: `sortedKey = "dgo"`.
- Check `map`:
  - `sortedKey` ("dgo") is not present, so add it with a new list.
  - `map = {"act": ["act"], "dgo": ["god"]}`.

---

**Iteration 3** (`str = "cat"`):
- Convert `str` to a character array: `charArray = ['c', 'a', 't']`.
- Sort `charArray`: `sortedKey = "act"`.
- Check `map`:
  - `sortedKey` ("act") is already present.
  - Add `str` ("cat") to the existing list for "act".
  - `map = {"act": ["act", "cat"], "dgo": ["god"]}`.

---

**Iteration 4** (`str = "dog"`):
- Convert `str` to a character array: `charArray = ['d', 'o', 'g']`.
- Sort `charArray`: `sortedKey = "dgo"`.
- Check `map`:
  - `sortedKey` ("dgo") is already present.
  - Add `str` ("dog") to the existing list for "dgo".
  - `map = {"act": ["act", "cat"], "dgo": ["god", "dog"]}`.

---

**Iteration 5** (`str = "tac"`):
- Convert `str` to a character array: `charArray = ['t', 'a', 'c']`.
- Sort `charArray`: `sortedKey = "act"`.
- Check `map`:
  - `sortedKey` ("act") is already present.
  - Add `str` ("tac") to the existing list for "act".
  - `map = {"act": ["act", "cat", "tac"], "dgo": ["god", "dog"]}`.

---

#### Build the Result:
- Iterate over the `values` of `map`:
  - Add `["act", "cat", "tac"]` to `result`.
  - Add `["god", "dog"]` to `result`.

---

### Final Output:
```java
result = [["act", "cat", "tac"], ["god", "dog"]]
```

### Dry Run Complete:
This output matches the expected result for the given input.

---

Let me know if you'd like to test with additional inputs or scenarios!
