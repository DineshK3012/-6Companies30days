# [Verify Preorder Serialization Of a Binary Tree](https://leetcode.com/problems/verify-preorder-serialization-of-a-binary-tree/)

## Approach 1 (Recursion):

- **Time Complexity:** $O(n)$, where n is number of nodes
- **Space Complexity:** $O(n)$, for storing nodes after splitting


```java
class Solution {
    public boolean checkSubtree(String[] nodes, int[] counter){
        if(counter[0] >= nodes.length){
            return false;
        }

        if(nodes[counter[0]].equals("#")){
            return true;
        }

        counter[0]++;
        boolean left = checkSubtree(nodes, counter);
        if(!left){
            return false;
        }

        counter[0]++;
        boolean right = checkSubtree(nodes, counter);
       
        return right;
    }

    public boolean isValidSerialization(String preorder) {
        String[] nodes = preorder.split(",");

        int[] counter = new int[1];
        boolean res = checkSubtree(nodes, counter);
        System.out.println(res + " " + counter[0]);
        return res && (counter[0] == nodes.length-1);
    }
}
```

--- 

## Approach 2 (Using vacancy variable):
- Create a variable to store the vacancy/seats for nodes which have to come.
- When we encounter a nodes which is not null, then increase the vacancy by 1 {since, -1 + 2 => -1 because it is traversed already, +2 for its left and right child}
- Ff at any time vacancy becomes smaller than or equal to 0(and more node remaining), then simply return 0.
- At the end if vacancy becomes 0, then return else false
  
---

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$, for storing nodes after splitting


```java
class Solution {
    public boolean isValidSerialization(String preorder) {
        String[] nodes = preorder.split(",");

        int vacancy = 1;
        for(String s: nodes){
            if(vacancy == 0){
                return false;
            }

            if(s.equals("#")){
                vacancy--;
            }else{
                vacancy++;
            }
        }

        return vacancy == 0;
    }
}
```