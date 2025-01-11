# [Get Equal Substrings Within Budget](https://leetcode.com/problems/get-equal-substrings-within-budget/)

## Approach (Using Sliding Window)

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$

```cpp
class Solution {
public:
    int equalSubstring(string s, string t, int maxCost) {
        int i = 0, j = 0, cost = 0, ans = 0;
        while(j < s.length()){
            cost += abs((int)(s[j] - t[j]));

            while(cost > maxCost){
                cost -= abs((int)(s[i] - t[i]));
                i++;
            }

            ans = max(ans, (j - i + 1));
            j++;
        }

        return ans;
    }
};
```