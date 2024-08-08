# Symmetric Binary Tree
Given a binary tree T, determine if it is symmetric.

When the following conditions are met, we can determine that two subtrees are symmetric:
- The root values of the two subtree are equal
- The left subtree of the first subtree symmetry with the right subtree of the other.
- The right subtree of the first subtree symmetry with the left subtree of the other.

```c
 bool isSymmetric(TreeNode* root) {
        return !root || dfs(root->left, root->right);
    }

    bool dfs(TreeNode*p, TreeNode*q)
    {
        if (!p || !q) return !p && !q;
        return p->val == q->val && dfs(p->left, q->right) && dfs(p->right, q->left);
    }
```