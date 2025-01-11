# [Amount of Time for Binary Tree to Be Infected](https://leetcode.com/problems/amount-of-time-for-binary-tree-to-be-infected/description/)

## Approach (Using BFS & DFS):
- First apply dfs to traverse over all the nodes, to find the parent of each node and to find the node for the start. 
- Now, apply BFS on the given start node and return the number of levels we go after applying the BFS.

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$

```cpp
class Solution {
public:
    void dfs(TreeNode* node, unordered_map<int, TreeNode*>& parents, unordered_map<int, TreeNode*>& nodes) {
        nodes[node->val] = node; // Map the value to the node

        if (node->left) {
            parents[node->left->val] = node; // Map child to parent
            dfs(node->left, parents, nodes);
        }

        if (node->right) {
            parents[node->right->val] = node; // Map child to parent
            dfs(node->right, parents, nodes);
        }
    }

    int amountOfTime(TreeNode* root, int start) {
        if (!root) return 0; // Handle empty tree

        unordered_map<int, TreeNode*> parents;
        unordered_map<int, TreeNode*> nodes;

        // Populate parents and nodes maps
        dfs(root, parents, nodes);

        unordered_set<int> set; // Keep track of infected nodes
        queue<TreeNode*> q;

        // Initialize BFS
        q.push(nodes[start]);
        set.insert(nodes[start]->val);

        int l = 0;
        while (!q.empty()) {
            int s = q.size();
            for (int i = 0; i < s; i++) {
                TreeNode* temp = q.front();
                q.pop();

                // Check parent node
                if (parents.count(temp->val) == 1 && set.count(parents[temp->val]->val) == 0) {
                    q.push(parents[temp->val]);
                    set.insert(parents[temp->val]->val);
                }

                // Check left child
                if (temp->left && set.count(temp->left->val) == 0) {
                    q.push(temp->left);
                    set.insert(temp->left->val);
                }

                // Check right child
                if (temp->right && set.count(temp->right->val) == 0) {
                    q.push(temp->right);
                    set.insert(temp->right->val);
                }
            }

            l++;
        }

        return l - 1; // Adjust for extra increment
    }
};
```