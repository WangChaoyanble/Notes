# Other Formulas
## $QQ^T=I$
Columns of $Q$ are unit orthogonal vectors like: 

```math
Q=\begin{bmatrix}q_1&q_2&...&q_n\end{bmatrix}
```
$q_i^Tq_j=1$ if $i=j$, else $q_i^Tq_j=0$. Then we have: $Q^T=Q^{-1}$.

Proof:

$$Q^T=\begin{bmatrix}q_1^T\\q_2^T\\...\\q_n^T\end{bmatrix}$$

Then: 

$$Q^TQ=\begin{bmatrix}q_1^T\\q_2^T\\...\\q_n^T\end{bmatrix}\cdot\begin{bmatrix}q_1&q_2&...&q_n\end{bmatrix}=\begin{bmatrix}
q_1 \cdot q_1 & q_1 \cdot q_2 & \cdots & q_1 \cdot q_n \\
q_2 \cdot q_1 & q_2 \cdot q_2 & \cdots & q_2 \cdot q_n \\
\vdots & \vdots & \ddots & \vdots \\
q_n \cdot q_1 & q_n \cdot q_2 & \cdots & q_n \cdot q_n
\end{bmatrix}=I$$

## $A(A^TA)^{-1}A^T$

Projection matrix: $P=A(A^TA)^{-1}A^T$

Left multiply $x$ by $P$ so that we project $x$ to the column space of $A$: $Px$

Especially when $A$ is a vector $a$ we have $P=\frac{aa^T}{a^Ta}$, then $Px=\frac{aa^T}{a^Ta}x=\frac{a(a^Tx)}{a^Ta}=\frac{a^Tx}{a^Ta}a$