# Simple Dijkstra
Simple dijkstra could calculate the shortest path from the **starting point to every other point**. Below are the steps:
1. **Initialize $dist[1]=0, dist[i]=+\infty,i\gt 1$**. *$dist[i]$ represents the shortest path from the starting point $1$ to the point $i$.*
2. **Add point $1$ to set $S$**. *$S$ is a set of points that the shortest path have been confirmed*. Then repeat the following steps $n$ times:
   1. Find the mininum $dist[i]$ where $i$ is not in $S$.
   2. Add $i$ to set $S$.
   3. Go through every point $j$ that $i$ can reach in one step, update the shortest path of these points. *If dist[i]+w < dist[j], update dist[j]=dist[i]+w*.

# Optimized Dijkstra


# Bellman Ford


# Examples
## Simple Dijkstra
```c++
int g[N][N];  
int dist[N];  
bool st[N];   // st[i]==true means point i has been confirmed

int dijkstra()
{
    //Initialization
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;

    for (int i = 0; i < n - 1; i ++ )
    {
        //Find the minimun dist[t]
        int t = -1;     
        for (int j = 1; j <= n; j ++ )
            if (!st[j] && (t == -1 || dist[t] > dist[j]))
                t = j;
        //Update dist[j]
        for (int j = 1; j <= n; j ++ )
            dist[j] = min(dist[j], dist[t] + g[t][j]);
        
        //add t to S
        st[t] = true;
    }

    if (dist[n] == 0x3f3f3f3f) return -1;
    return dist[n];
}

```
## Bellman Ford

```c++
int n, m;       //n points, m edges
int dist[N];        // dist[x]: shortest path from point 1 to x

struct Edge     // edge a-->b
{
    int a, b, w;
}edges[M];


int bellman_ford()
{
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    //If we still have dist[b]>dist[a]+w in the nth  iteration
    // 如果第n次迭代仍然会松弛三角不等式，就说明存在一条长度是n+1的最短路径，由抽屉原理，路径中至少存在两个相同的点，说明图中存在负权回路。
    for (int i = 0; i < n; i ++ )
    {
        for (int j = 0; j < m; j ++ )
        {
            int a = edges[j].a, b = edges[j].b, w = edges[j].w;
            if (dist[b] > dist[a] + w)
                dist[b] = dist[a] + w;
        }
    }

    if (dist[n] > 0x3f3f3f3f / 2) return -1;
    return dist[n];
}

```



