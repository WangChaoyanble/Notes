# Complete Binary Search Tree
A BST(Binary Search Tree) is a tree that for all nodes, all values of the left subtree are less than the node's, and all values of the right subtree are greater than the node's.

Build a complete BST:
```c++
//For array arr[l:r] sorted ascend, find the root node index.
int findpivot(int l,int r)
{
    int N=r-l+1;
    int pivot;
    int Exp=log(N+1)/log(2);
    int left=N-(pow(2,Exp)-1);
    int LeftTreeNum=left-pow(2,Exp-1);
    if(LeftTreeNum>=0) pivot=pow(2,Exp)-1+l;
    else pivot=pow(2,Exp)-1+LeftTreeNum+l;
    return pivot;
}

vector<int> arr;
//Recursively construct the Binary Search Tree
TreeNode * buildTree(int l,int r)
{
    if(l>r) return NULL;
    
    int pivot=findpivot(l,r);
    TreeNode *p=new TreeNode(arr[pivot]);
    p->left=buildTree(l,pivot-1);
    p->right=buildTree(pivot+1,r);
    return p;
}
```