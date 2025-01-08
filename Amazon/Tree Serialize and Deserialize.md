# [Serialize And Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

## Approach (Using LevelWise Traversal):
- In serializing, find the levelwise traversal using BFS traversal of the tree and convert it into the string and return it.
- While deserializing, convert to string into the levelwise traversal and then convert it back into the Binary tree using the BFS traversal

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$


```java
class Codec {
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if(root == null)
            return "";

        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        List<List<Integer>> t = new ArrayList<>();

        while(!q.isEmpty()){
            int s = q.size();
            List<Integer> temp = new ArrayList<>();
            for(int i = 0; i<s; i++){
                TreeNode n = q.remove();
                temp.add(n.val);

                if(n.val == -1001){
                    continue;
                }

                if(n.left != null){
                    q.add(n.left);
                }else{
                    q.add(new TreeNode(-1001));
                }

                if(n.right != null){
                    q.add(n.right);
                }else{
                    q.add(new TreeNode(-1001));
                }
            }

            t.add(temp);
        }

        StringBuilder str = new StringBuilder();
        for(List<Integer> l: t){
            str.append(l).append("_");
        }

        return str.toString();
    }

    private List<Integer> stringToList(String traverse) {
        List<Integer> list = new ArrayList<>();

        traverse = traverse.substring(1, traverse.length() - 1); // Remove square brackets
        if (!traverse.isEmpty()) {
            String[] elem = traverse.split(", ");
            for (String e : elem) {
                list.add(Integer.parseInt(e));
            }
        }

        return list;
    }

    private List<List<Integer>> getBFSTraversal(String data){
        data = data.substring(0, data.length() - 1);

        List<List<Integer>> t = new ArrayList<>();
        String[] lists = data.split("_");

        for(String list: lists){
            t.add(stringToList(list));
        }

        return t;
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.length() == 0) {
            return null;
        }
        List<List<Integer>> t = getBFSTraversal(data);

        //converting the level-wise traversal to binary tree
        Queue<TreeNode> q = new LinkedList<>();
        TreeNode root = new TreeNode(t.get(0).get(0));
        q.add(root);
        int l = 1;
        while(!q.isEmpty()){
            int s = q.size();
            int j = 0;
            for(int i = 0; i<s; i++){
                TreeNode n = q.remove();

                if(t.get(l).get(j) != -1001){
                    n.left = new TreeNode(t.get(l).get(j));
                    q.add(n.left);
                }
                j++;

                if(t.get(l).get(j) != -1001){
                    n.right = new TreeNode(t.get(l).get(j));
                    q.add(n.right);
                }
                j++;
            }
            l++;
        }

        return root;
    }
}
```