# [Construct Longest New String](https://leetcode.com/problems/construct-the-longest-new-string/description/)

## Approach (Using Greedy approach)

- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$


```cpp
class Solution {
public:
    int longestString(int x, int y, int z) {
        if(x == y){
            return 2*(z + x + y); 
        }else if(x > y){
            return 2 *(z + 2 * y + 1);
        }else{
            return 2*(z + 2 *x + 1);
        }
    }
};
```