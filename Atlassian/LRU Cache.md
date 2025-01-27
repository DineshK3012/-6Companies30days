# [LRU Cache](https://leetcode.com/problems/lru-cache/)

## Approach (Using Doubly LinkedList & HahsMap):
- Doubly linkedlist to use as a queue.
- Why queue? To remove the least recently used which is the first element of queue
- Why DLL? If the element is get accessed in between, we have to remove it from the queue and add it at the last of the queue because it is accessed recently, to do this efficiently we are using dll.
- 

---

- **Time Complexity:**
  - get() Operation:
    - HashMap Lookup: $O(1)$    
    - DLL Update (remove + add): $O(1)$
    - Total: $O(1)$

  - put() Operation:
    - HashMap Lookup/Insertion: $O(1)$
    - DLL Operations (remove + add): $O(1)$
    - In case of eviction, removal from both the HashMap and DLL is also O(1).
    - Total: $O(1)$

  - Thus, both get() and put() operations run in $O(1)$ time.

- **Space Complexity:**
  - Space for HashMap:
    - Stores at most n entries (one per key in the cache).
    - Space: $O(n)$
  
  - Space for DLL:
    - Stores at most n nodes (one for each key in the cache).
    - Each node stores 2 pointers (prev and next) and the key-value pair.
    - Space: $O(n)$
  
  - Total space complexity: $O(n)$, where n is the cache capacity.


```java
class LRUCache {
    class DLLNode {
        int key, val;
        DLLNode prev, next;

        public DLLNode(int k, int v) {
            key = k;
            val = v;
        }
    }

    class DLL {
        DLLNode head, tail;

        public DLL() {
            head = tail = null;
        }

        public void add(DLLNode node) {
            if (head == null) {
                head = tail = node;
            } else {
                tail.next = node;
                node.prev = tail;
                tail = node;
            }
        }

        public void remove(DLLNode node) {
            if (node == head && node == tail) { // Only one node
                head = tail = null;
            } else if (node == head) { // Remove head
                head = head.next;
                head.prev = null;
            } else if (node == tail) { // Remove tail
                tail = tail.prev;
                tail.next = null;
            } else { // Remove middle node
                DLLNode prev = node.prev;
                DLLNode next = node.next;
                if(prev != null)
                    prev.next = next;

                if(next != null)
                    next.prev = prev;
            }
            node.prev = node.next = null; // Clean up
        }
    }

    int count;
    int max;
    HashMap<Integer, DLLNode> map;
    DLL dll;

    public LRUCache(int capacity) {
        dll = new DLL();
        count = 0;
        max = capacity;
        map = new HashMap<>();
    }
    
    public int get(int key) {
        if(map.containsKey(key)){
            DLLNode node = map.get(key);
            dll.remove(node);
            dll.add(node); 

            return node.val;
        }

        return -1;
    }
    
    public void put(int key, int value) {
        if(map.containsKey(key)){
            DLLNode node = map.get(key);

            dll.remove(node);
            node.val = value;
            dll.add(node);
        }else{
            DLLNode nn = new DLLNode(key, value);
            map.put(key, nn);

            dll.add(nn);
            count++;
        }

        if(count > max){
            DLLNode lru = dll.head;
            map.remove(lru.key);
            dll.remove(lru);
            count--;
        }
    }
}
```