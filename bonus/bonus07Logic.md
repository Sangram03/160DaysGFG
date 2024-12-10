class Solution {

    public boolean sentencePalindrome(String s) {
        // Step 1: Process the string to remove non-alphanumeric characters and convert to lowercase
        StringBuilder processedString = new StringBuilder();
        
        // Traverse the input string
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            // If the character is alphanumeric, add it to the processed string in lowercase
            if (Character.isLetterOrDigit(c)) {
                processedString.append(Character.toLowerCase(c));
            }
        }

        // Step 2: Check if the processed string is a palindrome
        int left = 0;
        int right = processedString.length() - 1;
        
        while (left < right) {
            if (processedString.charAt(left) != processedString.charAt(right)) {
                return false; // Return false if characters don't match
            }
            left++;
            right--;
        }

        return true; // Return true if it's a palindrome
    }
}
