# Successor of A Binary Tree Node
Given a binary tree node: 

```c++
struct TreeNode {
    int val;
    TreeNode *left,*right,*father;
    TreeNode(int x) : val(x), left(NULL), right(NULL), father(NULL) {}
};

```
Find the in-order traversal successor of the node.

- If the node has right child, then its successor is the first node of the in-order traversal of its right subtree
- If the node has no right child, we need to find **its nearest predecessor node that contains the node as left subtree**(The node is the last one of in-order as the left subtree of the predecessor). And that predecessor node is the one we want.

```c++
 TreeNode* inorderSuccessor(TreeNode* p) 
 {
    if (p->right) 
    {
        p = p->right;
        while (p->left) p = p->left;
        return p;
    }

    while (p->father && p == p->father->right) p = p->father;
    return p->father;
}
```