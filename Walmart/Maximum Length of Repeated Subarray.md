# [Maximum Length of Repeated Subarray](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)

## Approach (Using DP Tabulation)
- The question is exactly to longest common substring.
- And Longest Common Substring is similar to Longest Common Subsequence(LCS) but without carry forward, that means while filling dp table in LCS, if the current characters are not equal, then we take the maximum of the previous one's.
- But thats not the case in this, if the character are not matched we just set it to 0. If it matches then we take the previous answer + 1.

---

- **Time Complexity:** $O(n*m)$
- **Space Complexity:** $O(n*m)$

```java
class Solution {
    public int findLength(int[] nums1, int[] nums2) {
        int max = 0;
        int n = nums1.length;
        int m = nums2.length;
        
        int dp[][] = new int[n+1][m+1];
        for(int i = 1; i<=n; i++){
            for(int j = 1; j<=m; j++){
                if(nums1[i-1] == nums2[j-1]){
                    dp[i][j] = 1 + dp[i-1][j-1];
                    max = Math.max(max, dp[i][j]);
                }
            }
        }

        return max;
    }
}
```