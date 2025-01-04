# Count Number Of Incremovable Subarray I

## Approach (Bitmasking):
Finding all the subsequence of the string, and checking which of them are palindrome or not and store the palindromic ones in the map or something. And find the pair of two palindrome whose AND is zero and the product of length of maximum.

- **Time Complexity:** $O(2^n)$
- **Space Complexity:** $O(2^n)$

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