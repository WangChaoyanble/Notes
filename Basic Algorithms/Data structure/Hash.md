# Hash functions

We have data stored in such form: $(key,value)$, the $key$ is identical and can mark the correspond $value$.

Hash functions could quickly compute the address that the value is stored:
$$addr=Hash(key)$$
So that we can often get the value with the key in $O(1)$ time complexity.

## Linear Probing
A simple hash functino could be $hash(key)=key \% SIZE$, $SIZE$ is the capacity of the storage.

We assume that $SIZE=10$, and some key-values: $(1,100),(2,98),(3,16),(4,10),(13,34)$, with the hash function above, their addresses are as follows: $1,2,3,4,3$.

We could see conflicts. So we use linear probing to solve that: **Search the next empty location in the array by looking into the next cell until we find an empty cell.**

The $(13,34)$ conflicts so we search the next empty space is 5, their address are $1,2,3,4,5$.

Implement the function in C++, below shows how to search, insert and delete values:

```c++
#include<iostream>
#define SIZE 20

struct Data 
{
   int value;
   int key;
};

Data *hashArray[SIZE];

int hash(int key)
{
   return key % SIZE;
}
//Search
Data * search(int key)
{
    int index=hash(key);
    while(hashArray[index]!=NULL)
    {
        if(hashArray[index]->key==key)
            return hashArray[index];

        index++;
        index=index%SIZE;//Wrap around the table
    }

    return NULL;
}

bool insert(int key,int value)
{
    int index=hash(key);
    int flag=index;
    while(hashArray[index]!=NULL)
    {
        index++;
        index%=SIZE;
        if(index==flag) return false;
    }

    hashArray[index]=new Data;
    hashArray[index]->key=key;
    hashArray[index]->value=value;
    return true;

}

bool delete_(int key)
{
    int index=hash(key);
    int flag=index;
    while(hashArray[index]->key!=key)
    {
        index++;
        index%=SIZE;
        if(index==flag) return false;
    }
    delete hashArray[index];

    return true;
    
}
int main()
{
    insert(10, 20);
    insert(30, 10);
    Data *d=search(10);
    std::cout<<d->value<<std::endl;
    d=search(30);
    std::cout<<d->value<<std::endl;
    std::cout<<search(11)<<std::endl;
    delete_(30);
    std::cout<<search(30);

    return 0;
}
```

**References:**

[Hash Table Data structure
](https://www.tutorialspoint.com/data_structures_algorithms/hash_data_structure.html)