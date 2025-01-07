# [Brackets In Matrix Chain Multiplication](https://www.geeksforgeeks.org/problems/brackets-in-matrix-chain-multiplication1024/1)

## Approach (Using Dynamic Programming)
Using memoization approach, creating an dp array of pair(string, int) of dimension `n*n`.

- **Time Complexity:** $O(n^3)$
- **Space Complexity:** $O(n^2)$, ignoring the stack space


```cpp
class Solution {
  public:
    pair<string, int> helper(int i, int j, vector<int>& arr, vector<vector<pair<string, int>>>& dp){
        if(i + 1 == j){
            string s = "";
            s += 'A' + i;
            
            return {s, 0};
        }
        
        if(dp[i][j].second != -1)  return dp[i][j];
        
        int ans = INT_MAX;
        string s = "";
        
        for(int k = i+1; k < j; k++){
            auto p1 = helper(i, k, arr, dp);
            auto p2 = helper(k, j, arr, dp);
            
            int x = arr[i]*arr[k]*arr[j] + p1.second + p2.second;
            string st = "(" + p1.first + p2.first + ")";
            if(x < ans){
                ans = x;
                s = st;
            }
        }
        
        return dp[i][j] = {s, ans};
    }
  
    string matrixChainOrder(vector<int> &arr) {
        int n = arr.size();
        vector<vector<pair<string, int>>> dp(n, vector<pair<string, int>>(n, {"", -1}));
        
        auto p = helper(0, n-1, arr, dp);
        // cout<<p.first<<endl;
        
        return p.first;
    }
};
```