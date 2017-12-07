# Postorder

## Recursive Method

### Complexity

- Time : O(n)
- Space : O(h) if considering function call stack else O(1)

### Code

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
private:
    void traverse(vector<int>& postorder, TreeNode* root) {
        if (!root) return;
        traverse(postorder, root->left);
        traverse(postorder, root->right);
        postorder.push_back(root->val);
    }
    
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> postorder;
        traverse(postorder, root);
        return postorder;
    }
};
```



## Iterative Method using Two Stack

### Complexity

- Time : O(n)
- Space : O(n)

### Code

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> postorder;
        if (!root) return postorder;
        stack<TreeNode*> s1;
        stack<TreeNode*> s2;      
        s1.push(root);
        while (!s1.empty()) {
            TreeNode* current = s1.top();
            s2.push(current);
            s1.pop();
            if (current->left)
                s1.push(current->left);
            if (current->right)
                s1.push(current->right);
        }
        
        while (!s2.empty()) {
            postorder.push_back(s2.top()->val);
            s2.pop();
        }
        return postorder;
    }
};
```



## Related Problem

- [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal)