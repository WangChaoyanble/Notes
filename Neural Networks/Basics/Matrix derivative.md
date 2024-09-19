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
$f(\pmb{x}),\pmb{x}=[x_1,x_2,\cdots,x_n]^T$ :

$$\begin{align*} \mathbb{d}f(\pmb{x}) &=\frac{\partial f}{\partial x_1}\mathbb{d}x_1+\frac{\partial f}{\partial x_2}\mathbb{d}x_2 + \cdots+\frac{\partial f}{\partial x_n}\mathbb{d}x_n\\\\ &= (\frac{\partial f}{\partial x_1},\frac{\partial f}{\partial x_2},\cdots,\frac{\partial f}{\partial x_n}) \begin{bmatrix} \mathbb{d}x_1 \\ \mathbb{d}x_2\\ \vdots \\ \mathbb{d}x_n \end{bmatrix} \end{align*}$$

 
 $f(\pmb{X}),\pmb{X}_{m\times n}=(x_{ij})_{i=1,j=1}^{m,n}$ :

$$\begin{align*} \mathbb{d}f(\pmb{X}) &=\frac{\partial f}{\partial x_{11}}\mathbb{d}x_{11}+\frac{\partial f}{\partial x_{12}}\mathbb{d}x_{12} + \cdots+\frac{\partial f}{\partial x_{1n}}\mathbb{d}x_{1n}\\ &+\frac{\partial f}{\partial x_{21}}\mathbb{d}x_{21}+\frac{\partial f}{\partial x_{22}}\mathbb{d}x_{22} + \cdots+\frac{\partial f}{\partial x_{2n}}\mathbb{d}x_{2n}\\ &+\cdots\\ &+\frac{\partial f}{\partial x_{m1}}\mathbb{d}x_{m1}+\frac{\partial f}{\partial x_{m2}}\mathbb{d}x_{m2} + \cdots+\frac{\partial f}{\partial x_{mn}}\mathbb{d}x_{mn} \end{align*}$$

 $\pmb{F}(\pmb{X}),\pmb{F}_{p\times q}=(f_{ij})_{i=1,j=1}^{p,q},\pmb{X}_{m \times n}=(x_{ij})_{i=1,j=1}^{m,n}$ :

$$\begin{align*} \mathbb{d}\pmb{F}_{p \times q}(\pmb{X}) &= \begin{bmatrix} \mathbb{d}f_{11}(\pmb{X})& \mathbb{d}f_{12}(\pmb{X}) & \cdots & \mathbb{d}f_{1q}(\pmb{X}) \\ \mathbb{d}f_{21}(\pmb{X})& \mathbb{d}f_{22}(\pmb{X}) & \cdots & \mathbb{d}f_{2q}(\pmb{X}) \\ \vdots&\vdots&\vdots&\vdots \\ \mathbb{d}f_{p1}(\pmb{X})& \mathbb{d}f_{p2}(\pmb{X}) & \cdots & \mathbb{d}f_{pq}(\pmb{X}) \end{bmatrix}_{p \times q} \end{align*}$$