# Wiggle Sort

## Approach 1: Sorting the array

- **Time Complexity:** $O(nlogn)$
- **Space Complexity:** $O(n)$

```cpp
class Solution {
public:
    void wiggleSort(vector<int>& nums) {
        vector<int> copy;
        for (int num : nums) {
            copy.push_back(num);
        }

        sort(copy.begin(), copy.end());
        int i = copy.size() - 1;
        for (int k = 1; k < nums.size(); k += 2) {
            nums[k] = copy[i--];
        }

        for (int k = 0; k < nums.size(); k += 2) {
            nums[k] = copy[i--];
        }

    }
};
```


## Approach 2: Counting Sort / Frequncy Array
Use the frequency array to get the sorted numbers because the maximum value of an element is upto 5000 only

- **Time Complexity:** $O(n + 5001) => O(n)$, for storing the frequencies of elements
- **Space Complexity:** $O(5001) => O(1)$, constant space


```cpp
class Solution {
public:
    void wiggleSort(vector<int>& nums) {
        vector<int> f(5001, 0);
        for (int num : nums) {
            f[num]++;
        }

        int n = nums.size();
        int i = 5000;
        int k = 1;
        while(k < n){
            if(f[i] == 0){
                i--;
                continue;
            }

            nums[k] = i;
            f[i]--;
            k += 2;
        }

        k = 0;
        while(k < n){
            if(f[i] == 0){
                i--;
                continue;
            }

            nums[k] = i;
            f[i]--;
            k += 2;
        }
    }
};
```