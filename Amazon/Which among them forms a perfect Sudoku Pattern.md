# Valid Sudoku

## Approach:
Create a frequency array of size 9 and check for rows, columns and sub-boxes one after other for their validity.

- **Time Complexity:** $O(1)$, because board length is only 9
- **Space Complexity:** $O(1)$

```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        //checking rows
        for(int i = 0; i<9; i++){
            int freq[10] = {0};
            for(int j = 0; j<9; j++){
                if(board[i][j] == '.')  continue;

                if(freq[board[i][j] - '0'] > 0)   return false;
                freq[board[i][j] - '0']++;
            }
        }
        
        //checking columns
        for(int i = 0; i<9; i++){
            int freq[10] = {0};
            for(int j = 0; j<9; j++){
                if(board[j][i] == '.')  continue;

                if(freq[board[j][i] - '0'] > 0)   return false;
                freq[board[j][i] - '0']++;
            }
        }

        //checking sub boxes;
        for(int i = 0; i<9; i+=3){
            for(int j = 0; j<9; j+=3){
                //checking the sub-box
                int freq[10] = {0};
                for(int x = 0; x < 3; x++){
                    int newX = x + i;
                    for(int y = 0; y < 3; y++){
                        int newY = y + j;
                        if(board[newX][newY] == '.')  continue;

                        if(freq[board[newX][newY] - '0'] > 0)   return false;
                        freq[board[newX][newY] - '0']++;
                    }
                }
            }
        }

        return true;
    }
};
```