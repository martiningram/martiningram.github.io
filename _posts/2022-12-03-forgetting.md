---
layout: post
title: How to forget in an online linear regression
---

{% include mathjax.html %}

Recently, I [tweeted](https://twitter.com/xenophar/status/1595410322508189696) the following:

> Online linear regression is a cool special case of Kalman Filtering. Does anyone know how to _delete_ an observation? I'm interested in fitting a rolling window and it would be more efficient to do one update and one deletion rather than refitting each time...

I got some useful suggestions, and I think many of them would have led to a solution. However, the one that was easiest for me to try and worked was basically suggested by [ponzu](https://twitter.com/Gakki43094467), who wrote:

> use Woodbury equality and add is u while del is -u

Now, I actually didn't completely work out what he meant, but the term "Woodbury" set me on a path that worked out, so I thought I'd share that in case it's useful for others.

#### How to update

An online linear regression is basically just a sequence of multivariate normal updates. To be clear, let's consider a single data point, made up of the row vector $\mathbf{x}$ of covariates and the observation $y$. Let's further say that our current estimate of our parameters $\theta$ is given by the distribution

$$
\theta \sim \mathcal{N}(\mu, \Sigma).
$$

Then we can write that

$$
y = \mathbf{x}^T \theta + \epsilon,
$$

where

$$
\epsilon \sim \mathcal{N}(0, \sigma^2),
$$

the observation noise.

To me, the easiest way to derive the updating rule is to consider the joint distribution of $\theta$ and $y$. Because they are jointly normal, we can derive it using just means and covariances. I'll spare the details, but here's the result:

$$
\left[\begin{array}{c}  \theta \\ y  \end{array}\right] \sim
  \mathcal{N}\left( \left[\begin{array}{c}  \mu \\ \mathbf{x}^T \mu  \end{array}\right]  
  ,
    \left[\begin{array}{ c | c }
    \Sigma & \Sigma \mathbf{x} \\
    \hline
    \mathbf{x}^T \Sigma & \mathbf{x}^T \Sigma \mathbf{x} + \sigma^2
  \end{array}\right]
  \right)
$$

To find the distribution of $\theta \mid y$, we can use the [conditional distribution identity](https://en.wikipedia.org/wiki/Multivariate_normal_distribution#Conditional_distributions), which gives:

$$
\bar{\mu} = \mu + \Sigma \mathbf{x}(\mathbf{x^T}\Sigma\mathbf{x} +\sigma^2)^{-1}(y - \mathbf{x}^T \mu)
$$

for the posterior mean, and

$$
\bar{\Sigma} = \Sigma - \Sigma \mathbf{x}(\mathbf{x^T}\Sigma\mathbf{x} +\sigma^2)^{-1}\mathbf{x}^T\Sigma
$$

for the posterior covariance. This allows you to do online Bayesian linear
regression: just update one data point at a time with these equations, updating
your estimates of $\mu$ and $\Sigma$ every time. But what if we want to _forget_
an update?

#### How to forget

How do we recover $\Sigma$ and $\mu$ if we know the posterior -- i.e. $\bar{\Sigma}$ and $\bar{\mu}$ -- as well as $\mathbf{x}$ and $y$?

I first looked at the update for $\bar{\Sigma}$ and initially didn't see how to solve for $\Sigma$. The thing that I found tricky is that it appears twice in the second term on the right hand side. Perhaps there's some easy way to solve it, but I couldn't spot it.

However, the suggestion to look at the Woodbury formula gave me an idea. [That identity is](https://en.wikipedia.org/wiki/Woodbury_matrix_identity):

$$
(A + UCV)^{-1} = A^{-1} - A^{-1}U(C^{-1} + V A^{-1}U)^{-1}VA^{-1}
$$

If we stare a little bit, we can match the right hand side up with the expression for $\bar{\Sigma}$. We set:

* $A = \Sigma^{-1}$
* $U = \mathbf{x}$
* $C = \sigma^{-2}$
* $V = \mathbf{x}^T$

This then gives the more compact expression:

$$
\bar{\Sigma} = (\Sigma^{-1} + \mathbf{x}\sigma^{-2}\mathbf{x}^T)^{-1}
$$

Now we can do some algebra to find the following neat result, which I think [ponzu](https://twitter.com/Gakki43094467) was alluding to:

$$
\Sigma = (\bar{\Sigma}^{-1} - \mathbf{x}\sigma^{-2}\mathbf{x}^T)^{-1}
$$

To get to $\mu$, we can define

$$
\mathbf{h} = \Sigma \mathbf{x}(\mathbf{x}^T \Sigma \mathbf{x} + \sigma^2)^{-1}
$$

to make the maths a bit easier -- and we can compute this now because we can compute $\Sigma$, remember. After a little bit of algebra, we find

$$
\mu = (I - \mathbf{h}\mathbf{x}^T)^{-1}(\bar{\mu} - \mathbf{h}y).
$$

I suspect there's a neater expression, but this is good enough for me, and I hope it's useful to you too. If you can simplify to something nicer, let me know!

#### Code example

Here's some code to try this. First, generate some toy data:

```python
import numpy as np

np.random.seed(2)

N = 5
x = np.random.randn(5, 1)
mu = np.random.randn(N, 1)
y = np.random.randn()
sigma = np.random.randn(N, N)
sigma = (sigma @ sigma.T + np.eye(N)) * 0.1
sigma_obs = np.random.randn()**2
```

Next, make the update:

```python
sigma_y_sq = x.T @ sigma @ x + sigma_obs**2

mu_bar = mu + sigma @ x * sigma_y_sq**(-1) * (y - x.T @ mu)
sigma_bar = sigma - (sigma @ x) * sigma_y_sq**(-1) * (x.T @ sigma)
```

Now, recover the original parameters:

```python
# I normally would rearrange this to avoid the explicit inverses
# but won't here
sigma_rec = np.linalg.inv(np.linalg.inv(sigma_bar) - x @ x.T * sigma_obs**(-2))
h = sigma_rec @ x * (1 / (x.T @ sigma_rec @ x + sigma_obs**2))
mu_rec = np.linalg.solve(np.eye(N) - h @ x.T, mu_bar - h * y)
```

`mu_rec` and `sigma_rec` should now match `mu` and `sigma`.


#### Conclusion

I hope you've found this little post interesting. As I mentioned before, let me
know if you know of a way to simplify the expressions, especially for $\mu$!
