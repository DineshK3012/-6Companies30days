# [Query Kth smallest Trimmed Number]()

## Approach (using sorting)
- Radix sort

- **Time Complexity:** $O()$
- **Space Complexity:** $O()$


```cpp
class Solution {
public:
    vector<int> smallestTrimmedNumbers(vector<string>& nums, vector<vector<int>>& queries) {
        vector<int> ans(queries.size());
        int n = nums.size();
        int maxLength = nums[0].size();

        // Preprocess sorted results for each possible trimmed length
        vector<vector<pair<string, int>>> sortedByTrim(maxLength + 1, vector<pair<string, int>>());
        for (int trimLength = 1; trimLength <= maxLength; trimLength++) {
            vector<pair<string, int>> trimmed(n);
            for (int i = 0; i < n; i++) {
                string trimmedString = nums[i].substr(maxLength - trimLength);
                trimmed[i] = {trimmedString, i};
            }
            sort(trimmed.begin(), trimmed.end());
            sortedByTrim[trimLength] = trimmed;
        }

        // Process each query
        for (int i = 0; i < queries.size(); i++) {
            int k = queries[i][0];
            int trimLength = queries[i][1];
            ans[i] = sortedByTrim[trimLength][k - 1].second;
        }

        return ans;
    }
};
```