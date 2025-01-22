# [Find the City With the Smallest Number of Neighbors at a Threshold](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/)

## Approach (Using Floyd Warshall Algorithm)

- **Time Complexity:** $O(n^3)$
- **Space Complexity:** $O(n^2)$

```java
//Floyd Warshall Algorithm
class Solution {
    public int findTheCity(int n, int[][] edges, int distanceThreshold) {
        int max = (int)1e9;

        int matrix[][] = new int[n][n];

        //changing the unreachable nodes value to a bit value
        for(int i = 0; i<n; i++){
            for(int j = 0; j<n; j++){
                matrix[i][j] = max;
            }
        }

        for(int i = 0; i<edges.length; i++){
            int u = edges[i][0], v = edges[i][1], w = edges[i][2];
            matrix[u][v] = w;
            matrix[v][u] = w;
        }
        
        for(int k = 0; k<n; k++){
            for(int i = 0; i<n; i++){
                for(int j = 0; j<n; j++){
                    if(i == j)
                        continue;

                    matrix[i][j] = Math.min(matrix[i][j], matrix[i][k] + matrix[k][j]);
                }
            }
        }

        int ans = -1, cities = n;
        for(int i = 0; i<n; i++){
            int x = 0;
            for(int j = 0; j<n; j++){
                if(i == j)
                    continue;

                if(matrix[i][j] <= distanceThreshold){
                    x++;
                }
            }

            if(cities >= x){
                cities = x;
                ans = i;
            }
        }

        return ans;
    }
}
```