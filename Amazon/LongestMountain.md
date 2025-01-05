# Longest Mountain in Array

## Approach 1 (By Pre-Calculating):
Just Precalculate the maximum of elements in increasing consecutively from left to right and right to left

- **Time Complexity:** $O(2*n) => O(n)$
- **Space Complexity:** $O(n)$
  

```cpp
class Solution {
public:
    int longestMountain(vector<int>& arr) {
        int n = arr.size();
        vector<int> f(n, 1);

        for(int i = 1; i<n; i++){
            if(arr[i] > arr[i-1]){
                f[i] += f[i-1];
            }
        }

        int prev = 1, ans = 0;
        for(int i = n-2; i > 0; i--){
            if(arr[i] > arr[i+1]){
                prev++;
            }else{
                prev = 1;
            }

            if(!(prev == 1 || f[i] == 1))
                ans = max(ans, prev + f[i] - 1);
        }
        
        return ans;
    }
};
```

---

## Approach 2 (Single pass):
Just simulating the process of trekking the mountain. Important point to note here is another mountain only starts after the first one ends.

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$
  

```cpp
class Solution {
public:
    int longestMountain(vector<int>& arr) {
        int n = arr.size();
        int i = 0, ans = 0;

        while(i < n){
            int base = i;
            //walk up 
            while(i+1 < n && arr[i] < arr[i+1]){
                i++;
            }

            if(i == base){
                i++;
                continue;
            }

            int peak = i;
            //walk down
            while(i + 1 < n && arr[i] > arr[i+1]){
                i++;
            }

            if(i == peak){
                i++;
                continue;
            }

            ans = max(ans, i - base + 1);
        }

        return ans;
    }
};
```
