# Logistic Regression

## Description
Logistic regression is used for binary classification.

The usual hypothesis is: $h_\theta(x)=g(\theta^Tx)$ , $\theta=[\theta_0,\theta_1,...,\theta_n]^T$ , $x=[1,a_1,a_2,...,a_n]^T$ , $g(x)=\frac{1}{1+e^{-x}}$ .

Function $h_\theta(x)$ denotes the probability that $x$ is classified as positive class( $y=1$ ). 

In logistic regression, when $h_\theta(x)>=0.5$ , we predict $y=1$ , when $h_\theta(x)<0.5$ , $y=0$ .

## Loss Function
The loss function is:

$Cost(h_\theta(x),y)=-ylog(h_\theta(x))-(1-y)log(1-h_\theta(x))$

So that the cost function:

$J(\theta)=\frac{1}{m}\sum_{i=1}^mCost(h_\theta(x_i),y_i)$ 

$m$ is the number of samples for training.

We denote: 

${X}=[x_1 \space x_2... \space x_m]^T$

$y=[y_1,y_2,...,y_m]^T$

So we have: $H(X)=g(X\theta)$ , function $g$ is applied to every element of $X\theta$ .

$Cost(H(X),y)=$

