# [Count Words Obtained After Adding a Letter](https://leetcode.com/problems/count-words-obtained-after-adding-a-letter/description/)

## Approach (Using HashMap & HashSets)

- **Time Complexity:** $O(n + m)$
- **Space Complexity:** $O(m)$


```cpp
class Solution {
public:
    //O(26) => O(1)
    void match(vector<int>& f, unordered_map<string, int>& targets, unordered_set<string>& set, int &count){
        string s = "";
        for(int j = 0; j<26; j++){
            int t = f[j];
            while(t-- > 0){
                s += (char)(j + 'a');
            }
        }

        if(targets.find(s) != targets.end()){
            if(set.find(s) == set.end()){
                count += targets[s];
                set.insert(s);
            }
        }
    }

    int wordCount(vector<string>& startWords, vector<string>& targetWords) {
        int n = startWords.size(), m = targetWords.size();

        unordered_map<string, int> targets;
        //O(m)
        for(int i = 0; i<m; i++){
            vector<int> freq(26, 0);
            for(char ch: targetWords[i]){
                freq[ch-'a']++;
            }
            
            string s = "";
            for(int j = 0; j<26; j++){
                int f = freq[j];
                while(f-- > 0){
                    s += (char)(j + 'a');
                }
            }
            targets[s]++;
        }

        int count = 0;
        unordered_set<string> set;
        //O(n*26) => O(n)
        for(string word: startWords){
            vector<int> f(26, 0);
            for(char ch: word){
                f[ch-'a']++;
            }

            //O(26)
            for(char ch = 'a'; ch <='z'; ch++){
                if(f[ch-'a'] > 0){
                    continue;
                }

                f[ch-'a']++;
                //O(26)
                match(f, targets, set, count);
                f[ch-'a']--;

                if(set.size() == m){
                    return m;
                }
            }
        }

        return count;
    }
};  
```