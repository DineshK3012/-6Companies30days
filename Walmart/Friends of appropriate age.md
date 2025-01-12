# [Friends of Appropriate Ages](https://leetcode.com/problems/friends-of-appropriate-ages/description/)

## Approach (using Sorting and Binary Search)
- Sort the array first 
- And for each person, we calculate the expected range, and use binary search to find the number of elements in ages[] that sit in that range. 
- Note that, age[B] > 100 && age[A] < 100 is an useless condition which is fully convered by the second one.

---

- **Time Complexity:** $O(n*logn)$
- **Space Complexity:** $O(1)$

```cpp
class Solution {
public:
    int numFriendRequests(vector<int>& ages) {
        int n = ages.size();
        sort(ages.begin(), ages.end());

        int count = 0;
        for(int i = 0; i<n; i++){
            int l = (ages[i]*0.5 + 7);
            int r = ages[i];

            auto left = upper_bound(ages.begin(), ages.end(), l);
            auto right = lower_bound(ages.begin(), ages.end(), r+1);
            int d = (right - left - 1);

            count += max(d, 0);
        }                        

        return count;           
    }
};
```