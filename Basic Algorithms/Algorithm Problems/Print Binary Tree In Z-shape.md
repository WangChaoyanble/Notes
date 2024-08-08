# Print Binary Tree In Z-shape

Print the odd layer from the left to the right and the even layer from the right to the left.

```c
vector<vector<int>> printFromTopToBottom(TreeNode* root) {
        vector<vector<int>> res;
        if(!root) return res;
        queue<TreeNode*> q;
        q.push(root); int i = 1;
        while(q.size())
        {
            int len = q.size();
            vector<int> lev;
            for(int j = 0; j < len; j++)    /
            {
                auto t = q.front();
                q.pop();
                lev.push_back(t->val);
               
                if(t->left) q.push(t->left);
                if(t->right) q.push(t->right);                      
            }
            if(i % 2 == 0) reverse(lev.begin(),lev.end());   
            res.push_back(lev);  i++;
        }
        return res;
    }

```