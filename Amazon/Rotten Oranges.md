# Rotten Oranges

## Approach (Using Multisource BFS):
- First create a queue for the BFS traversal, add all those grid cells whose value is 2 (already rotten oranges) into the queue. 
- Now, apply BFS, while adding new oranges into the queue mark them as rotten (change there value to 2).
- After the BFS is finished, check if the grid has any fresh orange remaining if yes, then return -1, otherwise return the level in the BFS traversal.
  

- **Time Complexity:** $O(n*m)$
- **Space Complexity:** $O(n*m)$, used in queue

```cpp
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int n = grid.size(), m = grid[0].size();
        queue<pair<int, int>> q;

        int count = 0;
        for(int i = 0; i<n; i++){
            for(int j = 0; j<m; j++){
                if(grid[i][j] == 2){
                    q.push({i, j});
                }

                if(grid[i][j] == 1){
                    count++;
                }
            }
        }

        if(count == 0)  return 0;
        if(q.size() == 0)   return -1;

        int dx[] = {-1, 0, 0, 1};
        int dy[] = {0, -1, 1, 0};
        
        int l = 0;
        while(!q.empty()){
            int s = q.size();
            for(int i = 0; i<s; i++){
                pair<int, int> p = q.front();
                q.pop();

                for(int i = 0; i<4; i++){
                    int x = dx[i] + p.first;
                    int y = dy[i] + p.second;

                    if(x >= 0 && x < n && y >= 0 && y < m && grid[x][y] == 1){
                        q.push({x, y});
                        grid[x][y] = 2; //rotting the orange
                    }
                }
            }

            l++;
        }

        for(int i = 0; i<n; i++){
            for(int j = 0; j<m; j++){
                if(grid[i][j] == 1) return -1;
            }
        }

        return l-1;
    }
};
```