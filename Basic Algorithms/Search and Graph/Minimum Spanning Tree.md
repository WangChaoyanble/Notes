# Minimum Spanning Tree
## Prim's Algorithm
- Initialize the MST set($st[]$) as empty, and set $dist[]$ $+\infin$.*(dist[i] is the minimum distance to the current MST)*
- Loop the steps below until all points are added to the MST set.
  - Find the minimum $dist[i]$ where point $i$ is not in the MST set.
  - Add point $i$ to the set.
  - Update other $dist[]$ with point $i$.



Time complexity: $O(m^2+n)$

```c++
int n;      // number of vertices
int g[N][N];        // Adjacency matrix
int dist[N];        // the distance from the points to the current MST
bool st[N];     // Whether each vertex is in the MST

int prim()
{
    memset(dist, 0x3f, sizeof dist);

    int res = 0;// return the sum of the MST's weight
    for (int i = 0; i < n; i ++ )
    {
        int t = -1;
        
        for (int j = 1; j <= n; j ++ )//find the minimum dist[] that is not in the MST set.
            if (!st[j] && (t == -1 || dist[t] > dist[j]))
                t = j;

        if (i && dist[t] == INF) return INF;//

        if (i) res += dist[t];//add the point to the set.
        st[t] = true;
        //update dist[] with the point.
        for (int j = 1; j <= n; j ++ ) dist[j] = min(dist[j], g[t][j]);
    }

    return res;
}

```

## Kruskal's Algorithm

```c++

int n, m;       // n is number of vertices，m is number of edges
int p[N];       

struct Edge     
{
    int a, b, w;

    bool operator< (const Edge &W)const
    {
        return w < W.w;
    }
}edges[M];

int find(int x)     
{
    if (p[x] != x) p[x] = find(p[x]);
    return p[x];
}

int kruskal()
{
    sort(edges, edges + m);

    for (int i = 1; i <= n; i ++ ) p[i] = i;    // Initialization

    int res = 0, cnt = 0;
    for (int i = 0; i < m; i ++ )
    {
        int a = edges[i].a, b = edges[i].b, w = edges[i].w;

        a = find(a), b = find(b);
        if (a != b)     // Unify the two blocks
        {
            p[a] = b;
            res += w;
            cnt ++ ;
        }
    }

    if (cnt < n - 1) return INF;
    return res;
}

```