# [Map of Highest Peak](https://leetcode.com/problems/map-of-highest-peak/)

## Approach (Using Multisource BFS):
- Add all the cells with water into the queue
- Now Apply BFS on the queue and update the distances of land cells from the water cells.

---

- **Time Complexity:** $O(n*m)$
- **Space Complexity:** $O(n*m)$


```cpp
class Solution {
public:
    vector<vector<int>> highestPeak(vector<vector<int>>& isWater) {
        int n = isWater.size(), m = isWater[0].size();
        vector<vector<int>> height(n, vector<int>(m, -1));
        queue<pair<int, int>> q;
        
        for(int i = 0; i<n; i++){
            for(int j = 0; j<m; j++){
                if(isWater[i][j] == 1){
                    q.push({i, j});
                    height[i][j] = 0;
                }
            }
        }

        vector<vector<int>> dir = {{0, -1}, {0, 1}, {-1, 0}, {1, 0}};

        while(!q.empty()){
            int s = q.size();
            for(int i = 0; i<s; i++){
                auto [x, y] = q.front();
                q.pop();

                //visiting the neighbors
                for(vector<int> d: dir){
                    int newX = x + d[0];
                    int newY = y + d[1];

                    if(newX >= 0 && newX < n && newY >= 0 && newY < m && height[newX][newY] == -1){
                        height[newX][newY] = height[x][y] + 1;

                        q.push({newX, newY});
                    }
                }
            }
        }

        return height;
    }
};
```