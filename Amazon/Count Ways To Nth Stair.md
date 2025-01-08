# [Find the Number of Ways to Reach the Kth Stair](https://leetcode.com/problems/find-number-of-ways-to-reach-the-k-th-stair/description/)

## Approach (Using DP Memoization):
- The variable which are changing are i(current stair on which the person is), jump (the jump value which person can make), canJumpBack (denotes if the person can jumpback to i-1).
- Use HashMap instead of DP array because k can be upto $10^9$.
- Create key from the variable which are changing like "i_jump_canJumpBack".

- **Time Complexity:** $O(notExponential)$
- **Space Complexity:** $O(notExponential)$


```java
class Solution {
    private int helper(int i, int jump, int canJump, int k, HashMap<String, Integer> map){
        if(i > k + 1){
            return 0;
        }

        int ways = 0;
        if(i == k){
            ways++;
        }

        String key = i + "_" + jump + "_" + canJump;
        if(map.containsKey(key)){
            return map.get(key);
        }

        if(canJump == 1){
            ways += helper(i - 1, jump, 0, k, map);
        }

        ways += helper(i + (int)Math.pow(2, jump), jump + 1, 1, k, map);    
        map.put(key, ways);

        return ways;
    }

    public int waysToReachStair(int k) {
        HashMap<String, Integer> map = new HashMap<>();

        return helper(1, 0, 1, k, map);
    }
}
```