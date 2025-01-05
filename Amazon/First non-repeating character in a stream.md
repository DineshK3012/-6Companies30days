# First non-repeating character in a stream

## Approach:
Make an array of size 26 to store the frequency of all the characters in the string, traverse the string first time to calculate the frequency, second time to find the first character which comes only one time.

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(26) => O(1)$
  

```java
class Solution {
    public int firstUniqChar(String s) {
        int freq[] = new int[26];
        for(char ch: s.toCharArray()){
            freq[ch - 'a']++;
        }

        for(int i = 0; i<s.length(); i++){
            if(freq[s.charAt(i) - 'a'] == 1){
                return i;
            }
        }

        return -1;
    }
}
```