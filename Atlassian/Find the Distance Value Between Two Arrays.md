# [Find the Distance Value Between Two Arrays](https://leetcode.com/problems/find-the-distance-value-between-two-arrays/description/)

## Approach (Using binary search)
- Sort the arr2.
- Now iterate over all the element e of arr1.
- Find lower and upper limit -> $(e-d) <= x <= (e+4)$. Now, revert it i.e., we have to find x such that $x < (4-e)$ and $x > d+e$ 
- Use binary search to find the count of such number of elements. If the count of such element is equal to the size of the arr2. Then increase answer by 1. 

---

- **Time Complexity:** $O(m*logm + n * logm)$
- **Space Complexity:** $O(1)$


```cpp
class Solution {
public:
    int findTheDistanceValue(vector<int>& arr1, vector<int>& arr2, int d) {
        sort(arr2.begin(), arr2.end());

        int ans = 0;
        for(int num: arr1){
            int l = num - d;
            int r = num + d;
            // cout<<num<<" "<<l<<" "<<r<<endl;

            auto index1 = lower_bound(arr2.begin(), arr2.end(), l);
            auto index2 = upper_bound(arr2.begin(), arr2.end(), r);

            int count = index1 - arr2.begin() + arr2.end() - index2;
            // cout<<count<<" "<<(index1-arr2.begin())<<" "<<(index2 - arr2.begin())<<endl;
            if(count == arr2.size()){
                ans++;
            }
        }

        return ans;
    }
};
```