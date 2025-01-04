# Who is the winnner?

## Approach (Using Queue)
Just follow the simulation or the process given in the problem description.

- **Time Complexity:** $O(n * k)$
- **Space Complexity:** $O(n)$


```java
class Solution {
    public int findTheWinner(int n, int k) {
        Queue<Integer> q = new LinkedList<>();
        
        for(int i = 1; i<=n; i++){
            q.add(i);
        }
        
        int counter = k;
        while(q.size() > 1){
            if(counter == 1){
                q.remove();
                counter = k;
                continue;
            }
            
            q.add(q.remove());
            counter --;
        }
        
        return q.remove();
    }
}
```