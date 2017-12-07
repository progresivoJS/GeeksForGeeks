# Preorder

## Recursive Method

### Complexity

- Time : O(n)
- Space : O(h) if considering function stack else O(1).

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
	void traverse(vector<int>& preorder, TreeNode* root) {
		if (!root) return;
		preorder.push_back(root->val);
		traverse(preorder, root->left);
		traverse(preorder, root->right);
	}

public:
    vector<int> preorderTraversal(TreeNode* root) {
    	vector<int> preorder;
        traverse(preorder, root);
        return preorder;
    }
};
```

## Iterative Method

### Time and Space Complexity

- TIme : O(n)
- Space : O(h)

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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> preorder;
        if (!root) return preorder;
        stack<TreeNode*> s;
        s.push(root);
        while (!s.empty()) {
            TreeNode* current = s.top();
            s.pop();
            preorder.push_back(current->val);
            if (current->right)
                s.push(current->right);
            if (current->left)
                s.push(current->left);
        }
        return preorder;
    }
};
```

## Related Problem

- [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal)