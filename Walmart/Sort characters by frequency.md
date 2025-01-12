# [Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)

## Approach (Using Map and PriorityQueue)
- Map to store the frequency of every character
- Priority queue to create max heap, to sort the character in descending order of their frequency

- **Time Complexity:** $O(n + 128*log(128)) => O(n)$
- **Space Complexity:** $O(128) => O(1)$ 


```cpp
class Solution {
public:
    string frequencySort(string s) {
        map<char, int> mp;
        for(char ch: s){
            mp[ch]++;
        }

        priority_queue<pair<int, char>, vector<pair<int, char>>, less<pair<int, char>>> pq;
        for(auto m: mp){
            pq.push({m.second, m.first});
        }

        string ans;
        while(!pq.empty()){
            auto p = pq.top();
            pq.pop();

            ans.append(p.first, p.second);
        }

        return ans;
    }
};
```