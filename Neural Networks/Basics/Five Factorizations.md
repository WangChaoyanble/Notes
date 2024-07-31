# Five Factorizations
- $A=CR$, Columns in C are the independent columns in A,R is reduced echelon form of A.

- $A=LU$, $L$ is lower triangular and $U$ is upper triangular.
- $A=QR$, $Q$ is orthogonal matrix and $R$ is upper triangular matrix.
- $S=Q\Lambda Q^T$, $S$ is symmetric matrix, columns of $Q$ is the orthogonal eigenvectors of $S$, elements of diagonal matrix $\Lambda$ is the corresponding eigenvalues.
- $A=U\Sigma V^T$, $U$ and $V$ is orthogonal matrix,  $\Sigma$ is diagonal matrix.

## $A=CR$
![alt text](../../assets/MarkdownImg/image-3.png)

 $C$ consists of independent columns of A, columns of R can rebuild the matrix $C$ as shown above. Below is another version:
 
![alt text](../../assets/MarkdownImg/image-4.png)

## $A=LU$

## $A=QR$

## $S=Q\Lambda Q^T$

## $A=U\Sigma V^T$


### Change of basis
Orthonormal basis of vector $x$ is $I(n×n)$, another basis is $W(n×n)$.

We have $x=Wc$, $c$ is the new coordinate of $x$ under new basis $W$

Especially when $W$ is orthonormal basis we have $W^TW=I$, so the equation becomes like: $c=W^{-1}x=W^Tx$.

We can easily get the new coordinate.


**Refernces**

[The Art of Linear Algebra](https://github.com/kenjihiranabe/The-Art-of-Linear-Algebra)


