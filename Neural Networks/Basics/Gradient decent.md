One variable gradient decent:

$$x_{new}=x_{old}-\alpha \nabla_xf(x_{old})$$  
($\alpha$ is the learning rate)

And it's the same with the above when $x$ is a column vector, but the $\nabla_xf(x)$ becomes like $[\frac{\partial f}{\partial x_1},\frac{\partial f}{\partial x_2},... ,\frac{\partial f}{\partial x_n}]^T$.

With gradient decent we can find the $x$ that minimize $f(x)$. 

Example of muti-varible linear regression:

Consider the following equation:
$$f(x)=a_0+a_1x_1+...+a_{n-1}x_{n-1}=[a_0,a_1,...,a_{n-1}][x_0,x_1,x_2,...,x_{n-1}]^T=a^Tx,x_0=1$$

There are $m$ observations: 
$$X=\begin{bmatrix}
    x_0^{(1)}&x_1^{(1)}&...&x_{n-1}^{(1)}\\
     x_0^{(2)}&x_1^{(2)}&...&x_{n-1}^{(2)}\\
     ...&...&...&...\\
    x_0^{(m)}&x_1^{(m)}&...&x_{n-1}^{(m)}
    
\end{bmatrix},y'=[y_0,y_1,...,y_{n-1}]^T$$
We are minimizing: $g(a)=||Xa-y'||^2$

$$\begin{align}
    g(a)&=(Xa-y')^T(Xa-y')\\
    &=(a^TX^T-y'^T)(Xa-y')\\
    &=a^TX^TXa-y'^TXa-a^TX^Ty'+y'^Ty\\
\end{align}$$

There are two ways that we can solve:
- Gradient descent:

    Gradient: $\nabla_ag(a)=2X^TXa-2X^Ty'$

    So that we can use gradient descent:
    $$a_{new}=a_{old}-\alpha \nabla_ag(a_{old})$$

- Solve the equation:
  
  $Xa$ could be considered as the column space of $X$, so when $Xa-y'$ is orthogonal to the column space of $X$ that we get the minimum of $g(a)$, so we have the equation below:
  $$X^T(Xa-y')=0$$ 

  So: $a=(X^TX)^{-1}X^Ty'$


Below is a python code implementing gradient descent:
```python
import numpy as np
# Gradient descent
def compute_gradient(X,y,theta):
    
    return 2*(X.T@X@theta-X.T@y)

def compute_cost(X,y,theta):
    
    return np.mean(np.square(X@theta-y))

def linear_regression(X,y,alpha):
    err=1e-9
    theta=np.zeros((X.shape[1],1))
    
    while(compute_cost(X,y,theta)>err):
        theta=theta-alpha*compute_gradient(X,y,theta)
        
    return theta

# Solve equation
def regression(X,y):
    return np.linalg.inv(X.T@X)@X.T@y

X=np.array([[1,2,3],[1,5,6]])
y=np.array([[1.],[2.]])
alpha=0.001

print(linear_regression(X,y,alpha))
print(regression(X,y))


   


```