# Image Smoother

## Approach
Just find the average of all the neighbouring cells for every cell including it, and place it in the output.

- **Time Complexity:** $O(n * m * 9)$
- **Space Complexity:** $O(n*m)$


```java
class Solution {
    int[] dx = {-1, -1, -1, 0, 0, 1, 1, 1, 0};
    int[] dy = {-1, 0, 1, -1, 1, -1, 0, 1, 0};

    private void smooth(int i, int j, int n, int m, int[][] img, int[][] output){
        int sum = 0;
        int count = 0;
        for(int k = 0; k<9; k++){
            int x = i + dx[k];
            int y = j + dy[k];

            if(x >= 0 && x < n && y >= 0 && y < m){
                sum += img[x][y];
                count++;
            }
        }

        output[i][j] = sum/count;
    }

    public int[][] imageSmoother(int[][] img) {
        int n = img.length, m = img[0].length;
        int[][] output = new int[n][m];

        for(int i = 0; i<n; i++){
            for(int j = 0; j<m; j++){
                smooth(i, j, n, m, img, output);
            }
        }

        return output;
    }
}
```