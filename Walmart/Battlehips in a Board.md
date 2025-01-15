# [Battlehips in a Board](https://leetcode.com/problems/battleships-in-a-board/description/)

## Approach
- Simple Traversal approach is used in the solution.
- Alternate approach can be using DFS/BFS to count number of connected Components (Similar to number of islands question)

---

- **Time Complexity:** $O(m*n)$
- **Space Complexity:** $O(1)$


```java
class Solution {
    public int countBattleships(char[][] board) {
        int count = 0;

        for(int i = 0; i<board.length; i++){
            for(int j = 0; j<board[0].length; j++){
                if(board[i][j] == '.')  continue;

                if(i == 0 && j == 0){
                    if(board[i][j] == 'X'){
                        count++;
                    }
                }else if(i == 0){
                    if(board[i][j-1] != 'X'){
                        count++;
                    }
                }else if(j == 0){
                    if(board[i-1][j] != 'X'){
                        count++;
                    }
                }else{
                    if(board[i-1][j] != 'X' && board[i][j-1] != 'X'){
                        count++;
                    }
                }
            }
        }

        return count;
    }
}
```