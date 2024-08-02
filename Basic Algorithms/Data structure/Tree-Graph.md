# Binary Tree
## Level traveral
```c++
void LevelOrder(TreeNode *T)
{
    queue<TreeNode *> q;
    q.push(T);
    while(q.empty())
    {
        TreeNode t=q.front();
        q.pop();
        //visit(t);
        if(t->left) q.push(t->left);
        if(t->right) q.push(t-right);
    }
}
```

## Binary Tree non-recursive traversal
### In-order and pre-order
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