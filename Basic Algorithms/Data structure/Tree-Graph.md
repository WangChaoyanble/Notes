# Binary Tree
## Level Traveral
```c++
void LevelOrder(TreeNode *T)
{
    queue<TreeNode *> q;
    q.push(T);
    while(!q.empty())
    {
        TreeNode *t=q.front();
        q.pop();
        //visit(t);
        if(t->left) q.push(t->left);
        if(t->right) q.push(t->right);
    }
}
```

## Binary Tree Non-recursive Traversal
### In-order and Pre-order
```c++
void InOrder(TreeNode* T)
{
    stack<TreeNode *> s;
    TreeNode* p=T;
    while(p||!s.empty())
    {
        if(p)
        {   
            //visit(p), pre-order traverse
            s.push(p);
            p=p->left;
        }
        else
        {
            p=s.top();
            s.pop();
            //visit(p),in-order traverse
            p=p->right;
        }
    }
    printf("\n");
}

```
### Post-order
```c++
void PostOrder(TreeNode *T)
{
	stack<TreeNode *>s;
    TreeNode *p=T;
	TreeNode *r=NULL;
	while(p||!s.empty())
    {
		if(p)
        {				//Get to the far left
			s.push(p);
			p=p->left;
		}
		else
        {				//Go right
			p=s.top();
			if(p->right&&p->right!=r)//If lchild exists and is not visited.
            {	
				p=p->right;	//Turn right
			}
			else
            {				
				s.pop();
				//printf("%d ",p->val);
				r=p;			//record recent-visited node 
				p=NULL;			//reset p
			}
		}
	}
    
}

```
## Construct A Binary Tree
### From Postorder and Inorder
```c++
int inorder[N];
int preorder[N];
TreeNode * buildTree(int l1,int r1,int l2,int r2)//l1,r1 preorder,l2,r2 inorder
{
    if(l1>r1) return NULL;

    TreeNode *root=new TreeNode(preorder[l1]);

    int i=l2;
    for(;i<=r2;i++)
        if(preorder[l1]==inorder[i]) break;
    
    TreeNode *left=buildTree(l1+1,l1+i-l2,l2,i-1);
    TreeNode *right=buildTree(l1+i-l2+1,r1,i+1,r2);
    root->left=left;
    root->right=right;
    return root;
    
}
```
## Threaded Binary Tree
In a binary tree with n nodes, there are n+1 null pointer, so these can be used for pointing the predecessor or successor of the node.

If a node don't has left child, the left child pointer points to it's predecessor. And so the right pointer points to the successor.
### Create Threaded Binary Tree
```c++
struct ThreadNode{
    int val;
    ThreadNode *left,*right;
    int ltag,rtag;
    ThreadNode(int x):val(x),left(NULL),right(NULL),ltag(0),rtag(0){}
}

//Construct thread tree
ThreadNode *P=NULL;//used for storing predecessor
void InThread(ThreadNode *T) //T is the current visiting node and P is the recent visited node.
{
    if(T)
    {
        InThread(T->left);
        if(!T->left)
        {
            T->left=P;
            T->ltag=1;
        }
        if(P&&!P->right)
        {
            P->right=T;
            P->rtag=1;
        }
        P=T;
        InThread(T->right);
    }
}

void CreateInThread(ThreadNode *T)
{
    ThreadNode *pre=NULL;
    if(T)
    {
        InThread(T,pre);  //With this function, pre points to the last in-order node.So we need to process below:
        pre->right=NULL;
        pre->rtag=1;
    }
}

```
### Traverse Threaded Binary Tree
Find the first in-order node of threaded tree T:
```c++
ThreadNode * FirstNode(ThreadNode *T)
{
    if(!T) return NULL;
    while(!T->ltag) T=T->left;
    return T;
}
```
Find the in-order succussor of threaded tree T:
```c++
ThreadNode *NextNode(ThreadNode *T)
{
    if(T->rtag) return T->right;
    else return FirstNode(T);
}
```
In-order traversal of threaded tree:
```c++
void ThreadInOrder(ThreadNode *T)
{
    for(ThreadNode *p=FirstNode(T);p!=NULL;p=NextNode(p))
        printf("%d ",p->val);
}
```