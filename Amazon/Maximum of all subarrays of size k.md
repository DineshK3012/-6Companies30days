# Maximum of all subarrays of size k

## Approach 1 (Using Ordered Map):

- **Time Complexity:** $O(n*logk)$
- **Space Complexity:** $O(n-k) + O(k) => O(n)$, `O(n-k)` to store the answer and `O(k)` for the map
  

```cpp
class Solution {
public:
    // Function to find maximum of each subarray of size k.
    vector<int> maxOfSubarrays(vector<int>& arr, int k) {
        map<int, int> mp; // Maintains a sorted map of values and their counts
        vector<int> ans;

        // Initialize the map with the first window
        for (int i = 0; i < k; i++) {
            mp[arr[i]]++;
        }

        // Add the maximum of the first window
        ans.push_back(prev(mp.end())->first);

        // Slide the window across the array
        for (int i = k; i < arr.size(); i++) {
            // Remove the element going out of the window
            mp[arr[i - k]]--;
            if (mp[arr[i - k]] == 0) {
                mp.erase(arr[i - k]); // Erase if count becomes zero
            }

            // Add the new element coming into the window
            mp[arr[i]]++;

            // Add the maximum of the current window
            ans.push_back(prev(mp.end())->first);
        }

        return ans;
    }
};
```

## Approach 2 (Deque):

- **Maintaining the Maximum:** When adding a new element to the deque, any indices of elements smaller than the current element are removed from the back of the deque. This ensures that the largest element's index is always at the front.
- **Sliding the Window:** When the window slides, if the index at the front of the deque falls out of the current window, it is removed. This ensures that only indices within the current window are stored in the deque.
- **Accessing the Maximum:** The index at the front of the deque corresponds to the largest element in the current window. Accessing this element is `𝑂(1)`

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(k)$
  

```cpp
class Solution {
public:
    // Function to find maximum of each subarray of size k.
    vector<int> maxOfSubarrays(vector<int>& arr, int k) {
        deque<int> dq;
        vector<int> ans;

        // Initialize the map with the first window
        for (int i = 0; i < k; i++) {
            while(!dq.empty() && arr[dq.back()] <= arr[i]){
                dq.pop_back();
            }
            
            dq.push_back(i);
        }

        // Add the maximum of the first window
        ans.push_back(arr[dq.front()]);

        // Slide the window across the array
        for (int i = k; i < arr.size(); i++) {
            // Remove elements outside the current window
            if (!dq.empty() && dq.front() == i - k) {
                dq.pop_front();
            }
            
            while(!dq.empty() && arr[dq.back()] <= arr[i]){
                dq.pop_back();
            }
            
            dq.push_back(i);
            ans.push_back(arr[dq.front()]);
        }

        return ans;
    }
};
```