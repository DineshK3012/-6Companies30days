# [K-diff Pairs in an Array](https://leetcode.com/problems/k-diff-pairs-in-an-array/)

## Approach (Using Map)
- Add all the elements in the map
- Now, traverse over every unique element and find the matching pair for it by adding or subtracting the given k from it
- If found increase the count
- And remove the element from the queue before moving on.

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$

```cpp
class Solution {
public:
    int findPairs(vector<int>& nums, int k) {
        unordered_map<int, int> map;
        for(int num: nums){
            map[num]++;
        }   

        int count = 0;
        unordered_set<int> set;
        for(int num: nums){
            if(set.count(num) > 0)
                continue;

            if(k == 0){
                count += (map[num] > 1) ? 1: 0;
                map.erase(num);
                continue;
            }

            if(map[num+k] > 0){
                count++;
            }

            if(map[num-k] > 0){
                count++;
            }

            set.insert(num);
            map.erase(num);
        }

        return count;
    }
};
```