# Phone directory

## Approach (Brute Force)

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