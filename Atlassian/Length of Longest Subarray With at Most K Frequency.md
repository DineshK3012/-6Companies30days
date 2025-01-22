# [Length of Longest Subarray With at Most K Frequency](https://leetcode.com/problems/length-of-longest-subarray-with-at-most-k-frequency/description/)

## Approach (using Sliding Window & HashMap)

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$


```cpp
class Solution {
public:
    int maxSubarrayLength(vector<int>& nums, int k) {
        unordered_map<int, int> map;

        int i = 0, j = 0, ans = 0;
        while(j < nums.size()){
            map[nums[j]]++;

            while(i < j && map[nums[j]] > k){
                map[nums[i]]--;
                i++;
            }

            ans = max(ans, (j-i+1));
            j++;
        }

        return ans;
    }
};
```