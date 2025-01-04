# Count Number Of Incremovable Subarray I

- **Time Complexity:** $O(n^2)$
- **Space Complexity:** $O(1)$

```java
class Solution {
    public int incremovableSubarrayCount(int[] nums) {
        int ans = 0;
        int n = nums.length;

        int left = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {
            int right = Integer.MAX_VALUE;
            for (int j = n-1; j >= i; j--) {
                ans++;
                if(left >= nums[j] || nums[j] >= right){
                    break;
                }

                right = nums[j];
            }

            if(left >= nums[i])
                break;

            left = nums[i];
        }
        return ans;
    }
}

```