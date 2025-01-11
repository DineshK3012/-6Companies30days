# [Find Subsequence of Length K with the Largest Sum](https://leetcode.com/problems/find-subsequence-of-length-k-with-the-largest-sum/)

## Approach (Using Min-heap):
- By creating a min heap of size K
- Iterate over all the numbers add them into the min heap, remove number from min-heap if its size becomes greater than k. Due to this the only elements which are in the subsequence with the largest sum remains in the min-heap
- And we can simply print them in the order

- **Time Complexity:** $O(n*logk)$
- **Space Complexity:** $O(k)$


```cpp
class Solution {
public:
    vector<int> maxSubsequence(vector<int>& nums, int k) {
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> min_heap;

        for(int i = 0; i<nums.size(); i++){
            min_heap.push({nums[i], i});

            if(min_heap.size() > k){
                min_heap.pop();
            }
        }

        map<int, int> m;
        while(!min_heap.empty()){
            m.insert({min_heap.top().second, min_heap.top().first});
            min_heap.pop();
        }

        vector<int> ans;
        for(auto& x: m){
            ans.push_back(x.second);
        }

        return ans;
    }
};
```