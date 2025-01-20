# [Throne Inheritance](https://leetcode.com/problems/throne-inheritance/description/)

## Approach (Using Trees)
- Creating a Family tree.
- Returning Pre-order traversal of the tree for the inheritance order.

---

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$


```java
class TreeNode{
    String name;
    ArrayList<TreeNode> children;
    boolean isAlive;

    public TreeNode(String personName){
        this.name = personName;
        children = new ArrayList<>();
        isAlive = true;
    }
}

class ThroneInheritance {
    HashMap<String, TreeNode> map;
    TreeNode root;

    public ThroneInheritance(String kingName) {
        root = new TreeNode(kingName);
        map = new HashMap<>();
        map.put(kingName, root);
    }
    
    public void birth(String parentName, String childName) {
        TreeNode parent = map.get(parentName);
        map.putIfAbsent(childName, new TreeNode(childName));
        TreeNode child = map.get(childName);

        parent.children.add(child);
    }
    
    public void death(String name) {
        map.get(name).isAlive = false;
    }

    private void preOrder(TreeNode root, List<String> ans){
        if(root.isAlive){
            ans.add(root.name);
        }

        for(TreeNode child: root.children){
            preOrder(child, ans);
        }
    }
    
    public List<String> getInheritanceOrder() {
        List<String> ans = new ArrayList<>();
        preOrder(root, ans);

        return ans;
    }
}

/**
 * Your ThroneInheritance object will be instantiated and called as such:
 * ThroneInheritance obj = new ThroneInheritance(kingName);
 * obj.birth(parentName,childName);
 * obj.death(name);
 * List<String> param_3 = obj.getInheritanceOrder();
 */
```