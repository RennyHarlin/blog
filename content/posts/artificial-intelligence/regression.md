---
date: '2026-01-25T17:47:48+05:30'
draft: false
title: 'Linear Regression'
math: true
category: ['Machine Learning']
---

This is one of machine learning's lightly interpreted algorithms out there. Often always taught using abstractions that kills the beauty of this interesting algorithm. 

Let's look at this algorithm from the ground up.

First for any supervised machine learning, we need a dataset. Let's construct a simple one.

$$
(x_1, y_1), (x_2, y_2), (x_3, y_3)...(x_n, y_n)
$$

Here, $x_i$ is the input to the algorithm and $y_i$ is the output from the algorithm. Practically, the input $x_i$ can of arbitrary dimension belonging to $\mathbb{R}^m$, where m is the number of independent features in the input. But, for simplicity we are going to work with $x_i$ belonging to $\mathbb{R}^1$.

Our goal is to find a best fit line that best represents the training dataset, and use it to infer the value of $y_i$ from the testing dataset.

The line equation for our training dataset comes out to be $\hat{y_i} = mx_i + c$

Now, the error for $ith$ sample is $(y_i - \hat{y_i})^2$.

> We are considering squared error instead of the absolute error, because it makes the process of differentiation to minimize the error a whole lot easier. If you think about it the expression $|y_i - \hat{y_i}|$ does not have a derivative defined at $y_i - \hat{y_i} = 0$. So, squared errors are generally preferred.

So, our objective function for the entire training dataset becomes,

$$
\hat{e} = \sum_{i=1}^n(y_i - (mx_i + b))^2
$$
$$
\min_{m, b} \hat{e}
$$

On setting the gradients with respect to m and b to 0,

$$
\frac{\partial{\hat{e}}}{\partial{m}} = 0 
$$
$$
\sum_{i=1}^nx_i(y_i - (mx_i + b)) = 0 
$$

$$
\boxed{
\sum_{i=1}^nx_iy_i - m\sum_{i=1}^nx_i^2 + b 
\sum_{i=1}^nx_i = 0 }
$$

$$
\frac{\partial{\hat{e}}}{\partial{b}} = 0
$$
$$
\sum_{i=1}^n(y_i - (mx_i + b)) = 0
$$

$$
\boxed{
\sum_{i=1}^ny_i = m\sum_{i=1}^nx_i + nb
}
$$

Now, divide both equations $(1)$ and $(2)$ by n,

$$
\frac{1}{n}\sum_{i=1}^nx_iy_i - m (\frac{1}{n}\sum_{i=1}^nx_i^2) + b(\frac{1}{n}\sum_{i=1}^nx_i) = 0
$$

$$
\overline{x_iy_i} - m\overline{x_i^2} + b\overline{x_i} = 0 \tag{1}
$$

$$
\frac{1}{n}\sum_{i=1}^ny_i = m(\frac{1}{n}\sum_{i=1}^nx_i) + b
$$
$$
\overline{y_i} = m\overline{x_i} + b
$$
$$
b = \overline{y_i} - m\overline{x_i} \tag{2}
$$

On substituting $(2)$ in $(1)$,

$$
\overline{x_iy_i} - m\overline{x_i^2} + (\overline{y_i} - m\overline{x_i})\overline{x_i} = 0 
$$
$$
\overline{x_i y_i} - \overline{x_i},\overline{y_i} = m\left(\overline{x_i^2} - \overline{x_i}^2\right)
$$

So, finally after so much math we have,

$$
\boxed{
    m = \frac{\overline{x_i y_i} - \overline{x_i} \ \overline{y_i}}{\left(\overline{x_i^2} - \overline{x_i}^2\right)}
} \tag{3}
$$

$$
\boxed{
    b = \overline{y_i} - m\overline{x_i} \tag{4}
}
$$

Eqns 3 and 4 give us closed form solution of linear regression.

Interestingly, if we have a look at equation 3 carefully, it can be broken down in to:
$$
\boxed{
    m = \frac{Cov(X, Y)}{Var(x)}
}
$$

This is no coincidence, the slope is large when:
1. X and Y vary in the same direction (large covariance)
2. The spread of X around the mean is small (small variance)

Now, this same idea can be used for multiple linear regression. In multiple linear regression, our input $x_i$ belong to $\mathbb{R}^n$. Therefore, our linear regressor will no longer be a line but a hyperplane of dimension $n$.

So, our best fit hyper plane equation is given by,

$$
y = b + m_1x_1 + m_2x_2 + m_3x_3 + ... + m_nx_n
$$

In matrix notation, the above equation can be written as,

$$
AM = y
$$

where M is a vector of weights and the bias term, A is the matrix of inputs along with an extra column of 1's to accomodate the bias term, and y is the output vector.

I'm not going to overwhelm this blog even further with more math, but if the squared error is computed and the objective function is minimized with respect to M.

The final solution we get is:
$$
\boxed{
    M = (A^TA)^{-1}A^Ty
}
$$

$$
\boxed{
    \hat{y} = A(A^TA)^{-1}A^Ty
}
$$

If you have studied linear algebra, you will immediately realize that $(A^TA)^{-1}A^T$ is the pseudo inverse of $A$, and the $\hat{y}$ is the projection of $y$ onto the column space of $A$.

We started with the claim that the optimal solution for the weights and bias in linear regression are those that minimize the squared error. But, the solution also helped us deduce a conclusion that $\hat{y}$ always lies in the column space of the input or feature matrix. 

That's the beauty of linear regression, it connects linear algebra, statistics and optimization in to one nicely packed algorithm, and that's why today this exact algorithm is the pillar of modern machine learning and deep learning.














