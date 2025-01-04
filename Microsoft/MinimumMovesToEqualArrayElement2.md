# Minimum Moves To Equal Array Element II

## Approach 1: Sorting the array
Sort the array, find the median and find the sum absolute difference between the median and all elements in the array and return it.

- **Time Complexity:** $O(n*logn)$
- **Space Complexity:** $O(1)$

```java
class Solution {
    public int minMoves2(int[] nums) {
        int n =  nums.length;
        Arrays.sort(nums);
        
        int smallDiffElem = nums[(n-1)/2];
            
        int moves = 0;
        for(int i = 0; i<n; i++){
            moves += Math.abs(nums[i] - smallDiffElem);
        }
        
        return moves;
    }
}
```