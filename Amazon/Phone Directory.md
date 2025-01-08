# [Phone directory](https://www.geeksforgeeks.org/problems/phone-directory4628/1)

## Approach 1 (Brute Force)

- **Time Complexity:** $O(|s|*n*max|s|)$
- **Space Complexity:** $O(n)$, ignoring the output space

```cpp
class Solution {
public:
    vector<vector<string>> displayContacts(int n, string contact[], string s) {
        int m = s.length();
        vector<vector<string>> ans(m);
        sort(contact, contact + n);

        for (int i = 0; i < m; i++) {
            set<string> temp;
            for(int x = 0; x<n; x++){
                string c = contact[x];    
                bool isPrefix = true;
                if(c.length() <= i)
                    continue;
                
                for (int j = 0; j <= i; j++) { // Check for index bounds of c
                    if (s[j] != c[j]) { 
                        isPrefix = false;
                        break;
                    }
                }

                if (isPrefix) {
                    temp.insert(c);
                }
            }   
            
            vector<string> t;
            if(temp.size() == 0){
                t.push_back("0");
            }else{
                t.assign(temp.begin(), temp.end());
            }
            ans[i] = t;
        }

        return ans;
    }
};
```

--- 

## Approach 2 (Using Trie)

- **Time Complexity:** $O(m*n*logn + m*n*L)$, where `m` is `|S|` and `L` is `max|contact[i]|`
- **Space Complexity:** $O(n * L)$, used in creating trie, ignoring the output space

```cpp
class Solution {
private:
    struct TrieNode{
        unordered_map<char, TrieNode*> child;
        vector<string> list;
    };
    
    TrieNode* root;
    
    void insert(string s){
        TrieNode* t = root;
        for(char c: s){
            if(t->child[c] == NULL){
                t->child[c] = new TrieNode();
            }
            
            t = t->child[c];
            t->list.push_back(s);
        }
    }
    
    vector<string> getWords(string prefix){
        TrieNode* t = root;
        vector<string> empty;
        for(char c: prefix){
            if(t->child[c] == NULL){
                return empty;
            }
            
            t = t->child[c];
        }
        
        return t->list;
    }
    
public:
    vector<vector<string>> displayContacts(int n, string contact[], string s) {
        root = new TrieNode();
        for (int i = 0; i < n; i++) {
            insert(contact[i]);
        }
        
        vector<vector<string>> ans(s.length()); // Initialize ans with s.length() empty vectors
        for (int i = 0; i < s.length(); i++) {
            vector<string> list = getWords(s.substr(0, i + 1));
            sort(list.begin(), list.end());
            list.erase(unique(list.begin(), list.end()), list.end());
            
            if (list.size() == 0) {
                list.push_back("0");
            }
            
            ans[i] = list; // Assign list directly to ans[i]
        }
        
        return ans;
    }

};
```