# Quick Power Fibonacci Sequence 
Calculate the $n$th term of Fibonacci Sequence, $1\le n\le 10^8$.

$F(n+1)=F(n)+F(n-1),F(0)=0,F(1)=1.$

We can convert the formula above into matrix form:

$$\begin{bmatrix}
    F(n+1) \\
    F(n)
\end{bmatrix}=\begin{bmatrix}
    1&1\\
    1&0
\end{bmatrix}\begin{bmatrix}
    F(n)\\
    F(n-1)
\end{bmatrix}$$

So we get:

$$\begin{bmatrix}
    F(n+1) \\
    F(n)
\end{bmatrix}=\begin{bmatrix}
    1&1\\
    1&0
\end{bmatrix}^n \begin{bmatrix}
    F(1)\\
    F(0)
\end{bmatrix}$$

So we only need to do quick power to the matrix, below is a C++ implement:

```c++
#include<iostream>
#include<vector>
#define MOD 1000000007
using namespace std;
typedef long long LL;
typedef vector<vector<LL>> matrix;
// multiply matrix a by b
matrix mm(matrix a,matrix b)
{
    int an=a.size(),am=a[0].size();
    int bn=b.size(),bm=b[0].size();
    matrix res;
    if(am!=bn) exit(1);
    for(int i=0;i<an;i++)
    {
        res.push_back(vector<LL>());//push back a empty LL vector
        for(int j=0;j<bm;j++)
        {
            LL tmp=0;
            for(int k=0;k<am;k++)
               tmp=(tmp+(a[i][k]*b[k][j])%MOD)%MOD;
            res[i].push_back(tmp);//push back a LL vector
        }
    }
    return res;
}
// quick power function:
matrix quick_pow(LL n)
{
    matrix A={{1,1},{1,0}};
    matrix res={{1,0},{0,1}};
    while(n)
    {
        if(n&1) res=mm(A,res);
        n>>=1;
        A=mm(A,A);
    }
    return res;
}


int main()
{
    matrix res={{1,0},{0,1}};
    LL n;
    cin>>n;
    res=quick_pow(n);
    printf("%d ",res[0][0]);
    return 0;
}
```
