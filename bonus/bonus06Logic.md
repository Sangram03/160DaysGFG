

### Code Recap:
```java

class Solution {
    public List<String> camelCase(String[] arr, String pat) {
        List<String> result = new ArrayList<>();
        
        for (String word : arr) {
            StringBuilder uppercaseSeq = new StringBuilder();

            // Extract uppercase letters from the word
            for (char ch : word.toCharArray()) {
                if (Character.isUpperCase(ch)) {
                    uppercaseSeq.append(ch);
                }
            }

            // Check if the pattern is a prefix of the uppercase sequence
            if (uppercaseSeq.toString().startsWith(pat)) {
                result.add(word);
            }
        }

        return result;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        
        // Example 1
        String[] arr1 = {"WelcomeGeek", "WelcomeToGeeksForGeeks", "GeeksForGeeks"};
        String pat1 = "WTG";
        System.out.println(sol.camelCase(arr1, pat1)); // Output: ["WelcomeToGeeksForGeeks"]

        // Example 2
        String[] arr2 = {"Hi", "Hello", "HelloWorld", "HiTech", "HiGeek", "HiTechWorld", "HiTechCity", "HiTechLab"};
        String pat2 = "HA";
        System.out.println(sol.camelCase(arr2, pat2)); // Output: []
    }
}

```



Let's perform a dry run of the given code step-by-step with the two provided examples.

### Example 1:
```java
String[] arr1 = {"WelcomeGeek", "WelcomeToGeeksForGeeks", "GeeksForGeeks"};
String pat1 = "WTG";
```

#### Iteration 1 (Word: "WelcomeGeek")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "WelcomeGeek":
   - 'W' is uppercase, so `uppercaseSeq` becomes "W".
   - 'G' is uppercase, so `uppercaseSeq` becomes "WG".
3. The `uppercaseSeq` for "WelcomeGeek" is "WG".
4. Check if the pattern `"WTG"` is a prefix of `"WG"`. It is not, so this word is not added to the result.

#### Iteration 2 (Word: "WelcomeToGeeksForGeeks")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "WelcomeToGeeksForGeeks":
   - 'W' is uppercase, so `uppercaseSeq` becomes "W".
   - 'T' is uppercase, so `uppercaseSeq` becomes "WT".
   - 'G' is uppercase, so `uppercaseSeq` becomes "WTG".
3. The `uppercaseSeq` for "WelcomeToGeeksForGeeks" is "WTG".
4. Check if the pattern `"WTG"` is a prefix of `"WTG"`. It is a match, so this word is added to the result.

#### Iteration 3 (Word: "GeeksForGeeks")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "GeeksForGeeks":
   - 'G' is uppercase, so `uppercaseSeq` becomes "G".
   - 'F' is uppercase, so `uppercaseSeq` becomes "GF".
   - 'G' is uppercase, so `uppercaseSeq` becomes "GFG".
3. The `uppercaseSeq` for "GeeksForGeeks" is "GFG".
4. Check if the pattern `"WTG"` is a prefix of `"GFG"`. It is not, so this word is not added to the result.

**Output for Example 1**: `["WelcomeToGeeksForGeeks"]`

### Example 2:
```java
String[] arr2 = {"Hi", "Hello", "HelloWorld", "HiTech", "HiGeek", "HiTechWorld", "HiTechCity", "HiTechLab"};
String pat2 = "HA";
```

#### Iteration 1 (Word: "Hi")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "Hi":
   - 'H' is uppercase, so `uppercaseSeq` becomes "H".
3. The `uppercaseSeq` for "Hi" is "H".
4. Check if the pattern `"HA"` is a prefix of `"H"`. It is not, so this word is not added to the result.

#### Iteration 2 (Word: "Hello")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "Hello":
   - 'H' is uppercase, so `uppercaseSeq` becomes "H".
3. The `uppercaseSeq` for "Hello" is "H".
4. Check if the pattern `"HA"` is a prefix of `"H"`. It is not, so this word is not added to the result.

#### Iteration 3 (Word: "HelloWorld")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "HelloWorld":
   - 'H' is uppercase, so `uppercaseSeq` becomes "H".
   - 'W' is uppercase, so `uppercaseSeq` becomes "HW".
3. The `uppercaseSeq` for "HelloWorld" is "HW".
4. Check if the pattern `"HA"` is a prefix of `"HW"`. It is not, so this word is not added to the result.

#### Iteration 4 (Word: "HiTech")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "HiTech":
   - 'H' is uppercase, so `uppercaseSeq` becomes "H".
   - 'T' is uppercase, so `uppercaseSeq` becomes "HT".
3. The `uppercaseSeq` for "HiTech" is "HT".
4. Check if the pattern `"HA"` is a prefix of `"HT"`. It is not, so this word is not added to the result.

#### Iteration 5 (Word: "HiGeek")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "HiGeek":
   - 'H' is uppercase, so `uppercaseSeq` becomes "H".
   - 'G' is uppercase, so `uppercaseSeq` becomes "HG".
3. The `uppercaseSeq` for "HiGeek" is "HG".
4. Check if the pattern `"HA"` is a prefix of `"HG"`. It is not, so this word is not added to the result.

#### Iteration 6 (Word: "HiTechWorld")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "HiTechWorld":
   - 'H' is uppercase, so `uppercaseSeq` becomes "H".
   - 'T' is uppercase, so `uppercaseSeq` becomes "HT".
   - 'W' is uppercase, so `uppercaseSeq` becomes "HTW".
3. The `uppercaseSeq` for "HiTechWorld" is "HTW".
4. Check if the pattern `"HA"` is a prefix of `"HTW"`. It is not, so this word is not added to the result.

#### Iteration 7 (Word: "HiTechCity")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "HiTechCity":
   - 'H' is uppercase, so `uppercaseSeq` becomes "H".
   - 'T' is uppercase, so `uppercaseSeq` becomes "HT".
   - 'C' is uppercase, so `uppercaseSeq` becomes "HTC".
3. The `uppercaseSeq` for "HiTechCity" is "HTC".
4. Check if the pattern `"HA"` is a prefix of `"HTC"`. It is not, so this word is not added to the result.

#### Iteration 8 (Word: "HiTechLab")
1. `uppercaseSeq` is initialized as an empty `StringBuilder`.
2. Loop through each character of "HiTechLab":
   - 'H' is uppercase, so `uppercaseSeq` becomes "H".
   - 'T' is uppercase, so `uppercaseSeq` becomes "HT".
   - 'L' is uppercase, so `uppercaseSeq` becomes "HTL".
3. The `uppercaseSeq` for "HiTechLab" is "HTL".
4. Check if the pattern `"HA"` is a prefix of `"HTL"`. It is not, so this word is not added to the result.

**Output for Example 2**: `[]`

### Summary
- The first example returns `["WelcomeToGeeksForGeeks"]` because it is the only word that starts with the uppercase sequence `"WTG"`.
- The second example returns an empty list `[]` because no word starts with the uppercase sequence `"HA"`.