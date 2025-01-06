# Nuts And Bolts Problem

## Approach (Using sorting):
Sort both the nuts and bolts array. (No need for a custom comparator because the given ordering is already in ASCII order)

- **Time Complexity:** $O(nlogn)$
- **Space Complexity:** $O(logn)$
  

```cpp
class Solution {
  public:
    void matchPairs(int n, char nuts[], char bolts[]) {
        sort(nuts, nuts + n);
        sort(bolts, bolts + n);
    }
};
```