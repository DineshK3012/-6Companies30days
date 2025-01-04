# Russian Doll Envelopes

## Approach (Dynamic Programming)
Using Optimized Longest Increasing Subsequence. First sort the envelopes in increasing order of width and decreasing order of height. Then, find the LIS of the heights of the envelopes.

- **Time Complexity:** $O(n*logn)$
- **Space Complexity:** $O(n)$


```cpp
class Solution {
public:
    int maxEnvelopes(vector<vector<int>>& env) {
        sort(env.begin(), env.end(), [](auto &a, auto &b){
            return a[0] == b[0] ? a[1] > b[1] : a[0] < b[0];
        });

        vector<int> ans;
        ans.push_back(env[0][1]);

        for(int i = 1; i<env.size(); i++){
            if(env[i][1] > ans.back()){
                ans.push_back(env[i][1]);
            }else{
                int index = lower_bound(ans.begin(), ans.end(), env[i][1]) - ans.begin();
                ans[index] = env[i][1];
            }
        }

        return ans.size();
    }
};
```