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

But for complete binary tree, we can use an array to store.

For all nodes we can mark them from $1$ to $n$ in level order, for node $i$, its left child is $2i$, right child is $2i+1$ and its parent is $i/2$. 

```c++
const int N = 1010;
int arr[N], inorder[N];
int n, idx=0;
void InorderBuild(int root)
{
    if(root > n) return;
    InorderBuild(root * 2);
    inorder[root] = arr[idx++];
    InorderBuild(root * 2 + 1);
}
```