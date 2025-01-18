# [Assign Cookies](https://leetcode.com/problems/assign-cookies/)

## Approach (Greedy approach):
- Sort both the g and s array in decreasing order.
- Now take two pointer i and j, i points to g and j point to s.
- Now run a loop directly, till any one of them exceeds its respective array length.
- If the s[j] >= g[i], that means I can assign this cookie to that children, so increase count by one.
- If s[j] < g[i], that means no cookie can be assigned to this boy, hence increase i by one and move to next child.

---

- **Time Complexity:** $O(n*logn + m*logn + m + n)$
- **Space Complexity:** $O(1)$


```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end(), greater<>());
        sort(s.begin(), s.end(), greater<>());

        int i = 0, j = 0;
        int count = 0;
        while(i < g.size() && j < s.size()){
            if(s[j] >= g[i]){
                j++;
                count++;
            }

            i++;
        }

        return count;
    }
};
```