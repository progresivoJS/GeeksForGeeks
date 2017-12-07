# Connect nodes at same level using constant extra space

## Using O(n) Space

### Complexity

- Time : O(n)
- Space : O(n)

### Code

```c++
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        if (!root) return;
        queue<TreeLinkNode*> q;
        q.push(root);
        while (!q.empty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeLinkNode* node = q.front();
                q.pop();
                if (i != size - 1) {
                    node->next = q.front();
                }
                
                if (node->left)
                    q.push(node->left);
                if (node->right)
                    q.push(node->right);
            }
        }
    }
};
```



## Using Contant Space

### Complexity

- Time : O(n)
- Space : O(1)

### Code

```c++
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        TreeLinkNode* queue = root;
        TreeLinkNode* level = new TreeLinkNode(0);
        while (queue) {
            TreeLinkNode* current = level;
            while (queue) {
                if (queue->left) {
                    current->next = queue->left;
                    current = current->next;
                }
                if (queue->right) {
                    current->next = queue->right;
                    current = current->next;
                }
                queue = queue->next;
            }
            queue = level->next;
            level->next = nullptr;
        }
        delete level;
    }
};
```



## Related Problem

- [Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii) 