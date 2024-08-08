# Balanced Binary Tree
Determine whether binary tree root is a balanced binary tree or not.

```c++
class Solution {
public:
    Solution():result(true){}
    bool isBalanced(TreeNode* root) 
    {
        CalculateHeight(root);
        return result;
    }
    bool result;//storing the result true or false

    //Calculate the height of tree root
    int CalculateHeight(TreeNode *root)
    {
        if(!root) return 0;
        int left=CalculateHeight(root->left);
        int right=CalculateHeight(root->right);
        if(abs(left-right)>1) result=false;//if the height difference is greater than 1, result is false.
        return max(left,right)+1;
    }
};
```