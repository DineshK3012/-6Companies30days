# [Word Break](https://leetcode.com/problems/word-break/submissions/)

## Approach (Using DP Tabulation approach)
- Store all the words of dictionary into the hashset for faster check.
- Now, create a dp array of length of |s|, find the answer using dp.

---

- **Time Complexity:** $O(n^3)$,
- **Space Complexity:** $O(n + m)$, where n is the length of s and m is the number of words in the dictionary


```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> dict;
        for(string word: wordDict){
            dict.insert(word);
        }

        int n = s.length();
        vector<int> dp(n+1);
        dp[n] = 1;

        for(int i = n-1; i>=0; i--){
            string str = "";
            for(int j = i; j<n; j++){
                str += s[j];

                if(dict.find(str) != dict.end()){
                    dp[i] = dp[j+1];

                    if(dp[i] == 1)
                        break;
                }
            }
        }

        return dp[0];
    }
};
```