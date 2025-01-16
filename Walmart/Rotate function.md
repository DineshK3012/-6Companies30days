# [Rotate Function](https://leetcode.com/problems/rotate-function/)

## Approach (Using Pattern)

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$


```java
class Solution {
    public int maxRotateFunction(int[] nums) {
        int f0 = 0;
        int sum = 0, n = nums.length;

        for(int i = 0; i<n; i++){
            sum += nums[i];
            f0 += i * nums[i];
        }

        int max = f0;
        int next_fn = 0;
        int prev_fn = f0;
        for(int i = n-1; i>=0; i--){
            int num = nums[i];
            next_fn = prev_fn + sum - (n * num);
            max = Math.max(max, next_fn);
            prev_fn = next_fn;
        }

        return max;
    }
}
```