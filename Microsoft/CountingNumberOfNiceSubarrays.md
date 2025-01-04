# Counting Number Of Nice Subarrays

## Approach 1 (using Sliding window):
Find the total subarrays with atmost K odd numbers and total subarray with atmost K - 1 odd numbers and return the difference between them.

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$

```java
class Solution {
    private int atmostKOdd(int nums[], int k){
        if(k < 0)
            return 0;

        int i = 0, j = 0, oddCount = 0, n = nums.length, count = 0;
        while(j < n){
            if(nums[j] % 2 != 0)
                oddCount++;

            while(i < j && oddCount > k){
                if(nums[i] % 2 != 0){
                    oddCount--;
                }

                i++;
            }

            if(oddCount <= k)
                count += (j - i + 1);

            j++;
        }

        return count;
    }

    public int numberOfSubarrays(int[] nums, int k) {
        return atmostKOdd(nums, k) - atmostKOdd(nums, k-1);
    }
}
```

## Approach 2 (Prefix Sum):
Use the prefix sum of element by doing % 2. 

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        int n = nums.length;
        HashMap<Integer, Integer> ps = new HashMap<>();
        ps.put(0, 1);

        int count = 0, ans = 0;
        for(int i = 0; i<n; i++){
            count += nums[i] % 2;

            if(ps.containsKey(count - k)){
                ans += ps.get((count - k));
            }

            ps.put(count, ps.getOrDefault(count, 0) + 1);
        }

        return ans;
    }
}
```