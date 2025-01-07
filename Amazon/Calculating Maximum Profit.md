# [Best Time To Buy And Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

## Approach (Using Dynamic Programming)
Using the dp tabulation approach to solve the problem

- **Time Complexity:** $O(n*k)$
- **Space Complexity:** $O(n*k)$


```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> dp(n+1, vector<int>(2*k+1, 0));
        for(int i = n-1; i>=0; i--){
            for(int t = 2*k-1; t >= 0; t--){
                //not buying or selling the stock
                int ans1 = dp[i+1][t];

                //buying/selling
                int ans2 = (t % 2 == 0 ? -prices[i]: prices[i]) + dp[i+1][t+1];

                dp[i][t] = max(ans1, ans2);
            }
        }

        return dp[0][0];
    }
};
```