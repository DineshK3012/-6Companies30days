# [Largest Divisible Subset](https://leetcode.com/problems/largest-divisible-subset/description/)

## Approach (Using DP)
- Using the same approach as Longest Increasing Subsequence using dp.

- **Time Complexity:** $O(n^2)$
- **Space Complexity:** $O(n)$


```cpp
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        vector<int> dp(n, 1);
        vector<int> prev(n, -1);
        int mx = 1, maxIndex = 0;

        for(int i = 1; i<n; i++){
            int j = i-1;
            while(j >= 0){
                if(nums[i] % nums[j] == 0){
                    if(dp[i] < 1 + dp[j]){
                        dp[i] = 1 + dp[j];
                        prev[i] = j;
                    }
                }
                j--;
            }

            if(dp[i] > mx){
                mx = dp[i];
                maxIndex = i;
            }
        }   

        vector<int> ans(mx);
        int i = mx-1;
        int y = maxIndex;
        while(prev[y] != -1){
            ans[i] = nums[y];
            i--;
            y = prev[y];
        }
        ans[0] = nums[y];
        return ans;
    }
};
```