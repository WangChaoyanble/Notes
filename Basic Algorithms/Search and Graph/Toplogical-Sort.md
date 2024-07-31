# Toplogical Sorting

A static linked list version of toplogical sorting:
```c++

#include <iostream>
#include <cstring>
using namespace std;
const int N=100010;
int h[N],e[N],ne[N],idx=0;//Linked lists

int n,m;// n/m is the number of the points/edges
int q[N],d[N];//q is used as a queue and d[i] is the indegree of point i 
void add(int a,int b) //add edge a --> b
{
    ne[idx]=h[a];
    e[idx]=b;
    h[a]=idx++;

    d[b]++;
}

bool topsort()
{
     int hh=0,tt=-1;
    for(int i=1;i<=n;i++)
     if(!d[i]) 
     q[++tt]=i;//add zero-indegree point to the queue
    while(hh<=tt)
    {
        int t=q[hh++];
        for(int i=h[t];i!=-1;i=ne[i])
        {
            int j=e[i];
            d[j]--;//delete edge t --> j
            if(d[j]==0)//add j to the queue if j's indegree is 0
            q[++tt]=j;
        }
    }
    return tt==n-1; //if all points are in the queue, return true
}

int main() 
{
    cin>>n>>m;
    memset(h,-1,sizeof(h));//Init the headnode
    for(int i=0;i<m;i++)
    {
        int a,b;
        scanf("%d%d",&a,&b);
        add(a,b);
        
    }
     if(topsort()) 
    {
        for(int i=0;i<n;i++)
        printf("%d ",q[i]);
        puts("");
    }
    else
    puts("-1");


    return 0;
}

```