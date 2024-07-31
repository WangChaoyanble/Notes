# KMP Algorithm

$next[i]=j$ means that a substring(*not starting with the first char*) ends with the ith char match a prefix of the whole string. $j$ is the maximum length of that substring.

How to calculate array $next[]$：


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