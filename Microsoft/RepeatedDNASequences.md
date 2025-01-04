# Repeated DNA Sequences

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$

```cpp
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        unordered_set<string> ans, set;
        for (int i = 0; i + 10 <= s.size(); i++) {
            string substr = s.substr(i, 10);
            if (set.count(substr)) {
                ans.insert(substr);
            }
            set.insert(substr);
        }

        return {ans.begin(), ans.end()};
    }
};

```