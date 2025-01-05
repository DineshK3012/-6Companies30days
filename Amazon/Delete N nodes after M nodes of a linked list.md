# Delete N nodes after M nodes of a linked list

## Approach:
Just simulating the process

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$

```cpp
class Solution {
  public:
    Node* linkdelete(Node* head, int n, int m) {
        if (!head) return NULL; // Handle empty list

        Node* current = head;

        while (current) {
            // Skip `m` nodes
            int skip = m;
            while (current && skip > 1) {
                current = current->next;
                skip--;
            }

            // If we've reached the end of the list, break
            if (!current) break;
            
            // cout<<current->data;

            // Start deleting `n` nodes
            Node* temp = current->next;
            int deleteCount = n;
            while (temp && deleteCount > 0) {
                Node* toDelete = temp;
                temp = temp->next;
                delete toDelete; // Free memory for the deleted node
                deleteCount--;
            }

            // Link the remaining list
            current->next = temp;
            current = temp; // Move to the next segment
        }

        return head;
    }
};
```