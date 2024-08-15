# Disjoint Set Union
Disjoint Set Union is a data structure used for sets management, nanifesting as a forest, and each tree represents a set. It has mainly two operations:
- Unify two sets.
- Find the set that a element belongs to.

```c++
int p[N]; //p[i] stores the ancestor index of vertex i

// return the ancestor node of vertex i
int find(int x)
{
    if (p[x] != x) p[x] = find(p[x]);
    return p[x];
}

// Initialization:
void init()
{
    for (int i = 1; i <= n; i ++ ) 
        p[i] = i;
}

// Unify the two sets where A and B belong to:
void unite(int a,int b)
{
    p[find(a)] = find(b);
}
 
```
