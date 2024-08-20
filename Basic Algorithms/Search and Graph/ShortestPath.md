# Simple Dijkstra
Simple dijkstra could calculate the shortest path from the **starting point to every other point**. Below are the steps:
1. **Initialize $dist[1]=0, dist[i]=+\infty,i\gt 1$**. *$dist[i]$ represents the shortest path from the starting point $1$ to the point $i$.*
2. **Add point $1$ to set $S$**. *$S$ is a set of points that the shortest path have been confirmed*. Then repeat the following steps $n-1$ times:
   1. Find the mininum $dist[t]$ where $t$ is not in $S$.
   2. Add $t$ to set $S$.
   3. Go through every point $j$ that $t$ can reach in one step, update the shortest path of these points. *If dist[t]+w < dist[j], update dist[j]=dist[t]+w*.
```c++
int g[N][N];  
int dist[N];  
bool st[N];   // st[i]==true means point i has been confirmed

int dijkstra()
{
    //Initialization
    memset(dist, INF, sizeof dist);
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

    if (dist[n] == INF) return -1;
    return dist[n];
}

```


# Bellman Ford
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
    //If we still have dist[b]>dist[a]+w in the nth iteration, it indicates that there exists a shortest path with a length of n+1，suggesting the existence of a negative-weight cycle in the graph.
   
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

# Floyd Algorithm
The core point of Floyd Algorithm is dynamic programming:

Assume that $dp[k][i][j]$ is the shortest distance from $i$ to $j$ throught only the first $k$ edges. So the state transition function:

$dp[k][i][j]=min(dp[k-1][i][j],dp[k-1][i][k]+dp[k-1][k][j])$.

So we can go through every $k$ and calculate the corresponding shortest path $i$ to $j$, so the total time complexity is $O(n^3)$.

As we don't need to record the history shortest path, so we can strip off the first dimension. So the equation is like:

$dp[i][j]=min(dp[i][j],dp[i][k]+dp[k][j])$.


```c++
//Initialization:d[i][j] represents the shortest distance from a to b
void init()
{
    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= n; j ++ )
            if (i == j) d[i][j] = 0;
            else d[i][j] = INF;
}
    

// After the algorithm，d[a][b] is the shortest distance from a to b
void floyd()
{
    for (int k = 1; k <= n; k ++ )
        for (int i = 1; i <= n; i ++ )
            for (int j = 1; j <= n; j ++ )
                d[i][j] = min(d[i][j], d[i][k] + d[k][j]);
}

```

# Conclusion










