# Matix derivative

## Vector variables
**This notes discribes the following case:**

$x$ is a vector variable while $f(x)$ is a constant like: $f(x), x=[x_1,x_2,...x_n]^T$

**Gradient vertor form:**
$$\nabla_x f(x)=\frac{\partial f(x)}{\partial x}=[\frac{\partial f}{\partial x_1},\frac{\partial f}{\partial x_2},... ,\frac{\partial f}{\partial x_n}]^T$$

**Several priciples:**
- $\frac{\partial x^Ta}{\partial x}=\frac{\partial x^Ta}{\partial x}=a$
- $\frac{\partial x^Tx}{\partial x}=2x$
- $\frac{\partial x^TAx}{\partial x}=Ax+A^Tx$
- $\frac{\partial a^Txx^Tb}{\partial x}=ab^Tx+ba^Tx$



## Matrix variables

Matrix variavle $\textbf{A} \in R^{m \times n}$ , scalar function $f(\textbf{A})$

- $\frac{\partial(a^TXb)}{\partial X}=ab^T$
- $\frac{\partial(a^TX^Tb)}{\partial X}=ba^T$
- $\frac{\partial(a^TXX^Tb)}{\partial X}=ba^TX+ab^TX$
- $\frac{\partial(a^TX^TXb)}{\partial X}=Xba^T+Xab^T$

## Differentiation of Matrices
### Real-valued scalar functions with vector variables

$f(\pmb{x}),\pmb{x}=[x_1,x_2,\cdots,x_n]^T$ :

$$\begin{align*} \mathbb{d}f(\pmb{x}) &=\frac{\partial f}{\partial x_1}\mathbb{d}x_1+\frac{\partial f}{\partial x_2}\mathbb{d}x_2 + \cdots+\frac{\partial f}{\partial x_n}\mathbb{d}x_n\\\\ &= (\frac{\partial f}{\partial x_1},\frac{\partial f}{\partial x_2},\cdots,\frac{\partial f}{\partial x_n}) \begin{bmatrix} \mathbb{d}x_1 \\ \mathbb{d}x_2\\ \vdots \\ \mathbb{d}x_n \end{bmatrix} \end{align*}$$

### Real-valued scalar functions of matrix variables

  $f(\pmb{X}),\pmb{X}_{m\times n}=(x_{ij})_{i=1,j=1}^{m,n}$ :

$$\begin{align*} \mathbb{d}f(\pmb{X}) &=\frac{\partial f}{\partial x_{11}}\mathbb{d}x_{11}+\frac{\partial f}{\partial x_{12}}\mathbb{d}x_{12} + \cdots+\frac{\partial f}{\partial x_{1n}}\mathbb{d}x_{1n}\\ &+\frac{\partial f}{\partial x_{21}}\mathbb{d}x_{21}+\frac{\partial f}{\partial x_{22}}\mathbb{d}x_{22} + \cdots+\frac{\partial f}{\partial x_{2n}}\mathbb{d}x_{2n}\\ &+\cdots\\ &+\frac{\partial f}{\partial x_{m1}}\mathbb{d}x_{m1}+\frac{\partial f}{\partial x_{m2}}\mathbb{d}x_{m2} + \cdots+\frac{\partial f}{\partial x_{mn}}\mathbb{d}x_{mn} \end{align*}$$

### Real Matrix Functions of Matrix Variables

 $\pmb{F}(\pmb{X}),\pmb{F}_{p\times q}=(f_{ij})_{i=1,j=1}^{p,q},\pmb{X}_{m \times n}=(x_{ij})_{i=1,j=1}^{m,n}$ :

$$\begin{align*} \mathbb{d}\pmb{F}_{p \times q}(\pmb{X}) &= \begin{bmatrix} \mathbb{d}f_{11}(\pmb{X})& \mathbb{d}f_{12}(\pmb{X}) & \cdots & \mathbb{d}f_{1q}(\pmb{X}) \\ \mathbb{d}f_{21}(\pmb{X})& \mathbb{d}f_{22}(\pmb{X}) & \cdots & \mathbb{d}f_{2q}(\pmb{X}) \\ \vdots&\vdots&\vdots&\vdots \\ \mathbb{d}f_{p1}(\pmb{X})& \mathbb{d}f_{p2}(\pmb{X}) & \cdots & \mathbb{d}f_{pq}(\pmb{X}) \end{bmatrix}_{p \times q} \end{align*}$$

Some principals：

- $\mathbb{d}\pmb{A}_{m \times n} = \pmb{0}_{m \times n}$
- $\mathbb{d}(c_1\pmb{F}(\pmb{X})+c_2\pmb{G}(\pmb{X})) = c_1\mathbb{d}\pmb{F}(\pmb{X})+c_2\mathbb{d}\pmb{G}(\pmb{X})$
- $\mathbb{d}(\pmb{F}(\pmb{X})\pmb{G}(\pmb{X}))=\mathbb{d}(\pmb{F}(\pmb{X}))\pmb{G}(\pmb{X}) + \pmb{F}(\pmb{X})\mathbb{d}\pmb{G}(\pmb{X})$ 
- $\mathbb{d}\pmb{F}^T_{p \times q}(\pmb{X})= (\mathbb{d}\pmb{F}_{p \times q}(\pmb{X}))^T$ 

Trace form $df(\pmb{X})$ can be derived with following steps:



$$\begin{align*} \mathbb{d}\pmb{X}_{m \times n} &= \begin{bmatrix} \mathbb{d}x_{11}& \mathbb{d}x_{12} & \cdots & \mathbb{d}x_{1n} \\ \mathbb{d}x_{21}& \mathbb{d}x_{22} & \cdots & \mathbb{d}x_{2n} \\ \vdots&\vdots&\vdots&\vdots \\ \mathbb{d}x_{m1}& \mathbb{d}x_{m2} & \cdots & \mathbb{d}x_{mn} \\ \end{bmatrix}_{m \times n} \end{align*}$$



According to the formula above, we can get: 

$$\begin{align*} \mathbb{d}f(\pmb{X}) &=\mathbb{tr}(\frac{\partial f(\pmb{X})}{\partial\pmb{X}^T} \mathbb{d}\pmb{X})\end{align*}$$

When $\pmb{X}$ degrades to a vector, the formula above is still correct.

Some principals of differentiation:

- $\mathbb{d}(\pmb{A}\pmb{X}\pmb{B})=\pmb{A}\mathbb{d}(\pmb{X})\pmb{B}$ , $\pmb{A}_{p \times m},\pmb{B}_{n \times q}$ are scalar matrices.
- 