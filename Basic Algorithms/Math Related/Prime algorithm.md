# Prime Number Algorithm

## Primality Testing

### Trial Division Algorithm
If $n$ is not a prime, it must can be decomposed to 2 factors that between $2$ and $n-1$, and one of the factors lies within the interval $[2,\sqrt{n}]$.
```c++
bool is_prime(int x)
{
    if (x<2) return false;
    for(int i=2;i<=x/i;i++)
        if(x%i==0) return false;
    return true;
}
```

### Factor prime number
We can also use this method to find the prime factors of number $n$:
```C++
void divide(int x)
{
    for(int i=2;i<=x/i;i++) //One of the factors lies within the interval [2,sqrt(n)]
        if(x%i==0)
        {
            int cnt=0;
            while(x%i==0) x=x/i,cnt++;
            cout<<i<<" "<<cnt<<endl;
        }
    if(x>1) cout<<x<<" "<<1<<endl;
}
```

## Solve for prime numbers
Given integer $N$, find all prime numbers that is less than $N$.

### The Sieve of Eratosthenes
To filter all prime numbers between $2$ and $N$, we just need to interate the interval $[2,N]$, remove the multiples of each number.

The rest are all prime numbers, below is a C++ implementation:

```c++
int primes[N],cnt;// Store all primes
int st[N];//If st[i] is true, i is not a prime

void get_primes(int N)
{
    cnt=0;
    for(int i=2;i<=N;i++)
    {
        if(st[i]) continue;
        primes[cnt++]=i;
        for(int j=2*i;j<=N;j=j*2)
            st[j]=true;
    }
}
```

### Euler's Sieve
In the algorithm above, when iterating and meet a prime number $x$, then the multiples of x are not primes.

But we will also meet repeated sieves.

Each composite number have a minimal prime factor, if the number is sieved only once by it's minimal prime factor, there would be no more repeated sieves.

```c
int primes[N], cnt;     // primes[] stores the primes
bool st[N];         // st[x] represents whether x is sieved

void get_primes(int n)
{
    for (int i = 2; i <= n; i ++ )
    {
        // if i is not sieved, store it in the primes[]
        if (!st[i]) primes[cnt ++ ] = i;
        // Seive all multiples of i
        for (int j = 0; primes[j] <= n / i; j ++ )
        {
            st[primes[j] * i] = true;
            if (i % primes[j] == 0) break;
        }
    }
}
```
