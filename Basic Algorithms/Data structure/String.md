# KMP Algorithm

$next[i]=j$ means that a substring(*not starting with the first char*) ends with the ith char match a prefix of the whole string. $j$ is the maximum length of that substring.

How to calculate array $next[]$：

We assume a array $arr[]$ and $next[i]=j$, for $next[i+1]$, we have two scenarios：
- If $arr[i+1]==arr[j+1]$, then $next[i+1]=j+1$
- If $arr[i+1]!=arr[j+1]$, if $arr[i+1]==arr[arr[j]+1]$, $next[i+1]=next[j]+1$, or $arr[i+1]=0$

```c++
// s[] is long tring (length n)，p[] is pattern string (length m), ne[] is the next array

//Claculate the next array：
for (int i = 2, j = 0; i <= m; i ++ )
{
    while (j && p[i] != p[j + 1]) j = ne[j];
    if (p[i] == p[j + 1]) j ++ ;
    ne[i] = j;
}

// match
for (int i = 1, j = 0; i <= n; i ++ )
{
    while (j && s[i] != p[j + 1]) j = ne[j];
    if (s[i] == p[j + 1]) j ++ ;
    if (j == m)
    {
        j = ne[j];
        // 
    }
}

```