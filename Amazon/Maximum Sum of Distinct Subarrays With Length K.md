# Maximum Sum of Distinct Subarrays With Length K

## Approach :
Using sliding window approach

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$
  

```java
class Solution {
    public long maximumSubarraySum(int[] nums, int k) {
        HashSet<Integer> set = new HashSet<>();
        int i = 0, j = 0, n = nums.length;
        long ans = 0;
        long curr = 0;
        while(j < n){
            curr += nums[j];

            while((j-i+1) > k || set.contains(nums[j])){
                curr -= nums[i];
                set.remove(nums[i]);
                i++;
            }

            if((j-i+1) == k){
                ans = Math.max(ans, curr);
            }

            set.add(nums[j]);
            j++;
        }

        return ans;
    }
}
```