# [Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/description/)

## Approach (using map and priority queue(max-heap))
- Map to store the frequency of each string
- Priority queue is to create a min heap to store the string in increasing order of their frequency

- **Time Complexity:** $O(n + n*logk + k*logk) => O(n*logk)$
- **Space Complexity:** $O(n+k)$


```cpp
class Solution {
public:
    vector<string> topKFrequent(vector<string>& words, int k) {
        // Step 1: Count word frequencies
        unordered_map<string, int> map;
        for (string word : words) {
            map[word]++;
        }

        // Step 2: Create a min-heap based on custom comparator
        auto cmp = [](const pair<int, string>& a, const pair<int, string>& b) {
            if (a.first == b.first) {
                return a.second < b.second; // Lexicographical order if frequencies are equal
            }
            return a.first > b.first; // Higher frequencies come earlier
        };

        priority_queue<pair<int, string>, vector<pair<int, string>>, decltype(cmp)> pq(cmp);

        // Step 3: Push elements into the heap and maintain size `k`
        for (auto& m : map) {
            pq.push({m.second, m.first});
            if (pq.size() > k) {
                pq.pop();
            }
        }

        // Step 4: Extract elements from the heap and reverse the order
        vector<string> ans;
        while (!pq.empty()) {
            ans.push_back(pq.top().second);
            pq.pop();
        }

        reverse(ans.begin(), ans.end()); // Reverse because the heap gives smallest first

        return ans;
    }
};
```