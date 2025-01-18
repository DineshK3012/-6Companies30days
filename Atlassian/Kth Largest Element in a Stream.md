# [Kth Largest Element in a Stream]()

## Approach (Using min-heap)
- Maintain a min-heap of of only K elements.
- If the size exceeds k then remove the top element from the heap.
- If you want to the kth largest element then return the top element.

---

- **Time Complexity:** $O(n*logk)$
- **Space Complexity:** $O(k)$


```cpp
class KthLargest {
priority_queue<int, vector<int>, greater<>> pq;
int limit;

public:
    KthLargest(int k, vector<int>& nums) {
        limit = k;

        for(int num: nums){
            pq.push(num);

            if(pq.size() > limit){
                pq.pop();
            }
        }
    }
    
    int add(int val) {
        pq.push(val);

        if(pq.size() > limit){
            pq.pop();
        }

        return pq.top();
    }
};
```