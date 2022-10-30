---
layout: post
title: Deriving the objective in Hensman et al. 2015
---

{% include mathjax.html %}

One of the main useful papers in my PhD was the [2015 paper by James Hensman, Alexander G. de G. Matthews, and Zoubin Ghahramani](https://proceedings.mlr.press/v38/hensman15.pdf). It's a really terrific and influential paper which allows GPs to be fitted to huge datasets. However, as it is  a conference paper, it is quite short and leaves out some details. It took me quite a long time to get there, but I think I have a fairly good understanding of the method now, so I thought I'd try to share my derivation in case it's useful for others. 

#### The general problem

The problem that the paper is trying to solve is that GP methods do not scale well with the number of data points, $N$. The paper presents an _inducing point_ approach: the idea is that we could perhaps approximate the full GP, conditioned on all $N$ points, by cleverly selecting a much smaller set of $M$ points. If we choose the GP values at these points well, we can hope to make predictions that are similar to those made using the full dataset. Intuitively, this will work particularly well if the function approximated by the GP doesn't vary very quickly. In that case, even a few well-chosen points and values could do a good job at approximating the full GP.

#### How does this help?

Before we go into how to fit an inducing point model, let's first consider how it could actually work. Let's say we have a set of inducing points $Z$. This $Z$ will be a matrix of shape $M \times D$, where $D$ is the number of dimensions in our dataset. These are intended to summarise the design matrix $X$ which has shape $N \times D$. Inducing point models like the one in Hensman et al. approximate the GP's function values $u$ at these points.

How do we actually predict new data $f^*$? Well, under the GP prior, the function values at any set of data points are jointly normal, and their covariance at any two points $x_1$ and $x_2$ is given by the value of the kernel function, $k(x_1, x_2)$. Generally, we also assume that the GP prior has zero mean. So the prior is then:

$$
\left[\begin{array}{c}  f^* \\ u  \end{array}\right] \sim
  \mathcal{N}\left( \left[\begin{array}{c}  0 \\ 0  \end{array}\right]  
  ,
    \left[\begin{array}{ c | c }
    k(x^*, x^*) & k(x^*, z) \\
    \hline
    k(z, x^*) & k (z, z)
  \end{array}\right]
  \right) 
  = 
    \mathcal{N}\left( \left[\begin{array}{c}  0 \\ 0  \end{array}\right]  
  ,
    \left[\begin{array}{ c | c }
    K_{nn} & K_{mn} \\
    \hline
    K_{nm} & K_{mm}
  \end{array}\right]
  \right)
$$

Here, the second equality just simplifies the notation a bit for later. Now we can condition. Let's say we knew the exact value at the inducing points. Then by the [general expressions for the multivariate normal](https://en.wikipedia.org/wiki/Multivariate_normal_distribution#Conditional_distributions), we know that the conditional distribution of $f^*$ is going to be multivariate normal with mean

$$
\mu = K_{nm} K_{mm}^{-1} u
$$

and covariance

$$
\Sigma = K_{nn} - K_{nm}K_{mm}^{-1}K_{mn}.
$$

So if we had a point estimate of the function value at the inducing points, we could predict a distribution at any other set of points using the kernel function and these expressions. Later we'll see that we can do this even if $u$ is itself not a single point but follows a normal distribution.

#### The variational idea

The posterior distribution we're interested in is

$$
p(u | y, \theta) = \frac{p(u|\theta) p(y | u, \theta)}{p(y | \theta)},
$$

where $u$ are the values of the GP at the inducing points, and $\theta$ are hyperparameters like lengthscales and variances. In general, when the likelihood is non-Gaussian, we cannot find the distribution on the left hand side analytically. So what do we do? Variational inference considers the following KL-divergence:

$$
KL[q(u | \eta) || p(u|y, \theta)].
$$

Here, $q(u \mid \eta)$ is a distribution we choose to approximate the posterior distribution on the inducing point values $u$. Here, we'll choose

$$
q(u|\eta) = \mathcal{N}(u|m, S),
$$

so our variational parameters $\eta$ consist of the means $m$ and a covariance matrix $S$. Essentially, the goal is to pick $m$ and $S$ so that $q(u \mid \eta)$ matches our posterior distribution, $p(u \mid y, \theta)$, as closely as possible in the sense of the KL divergence. That means we minimise the divergence as a function of $m$ and $S$.

#### The first bound

OK, so we'll be using the KL divergence. Where does this actually get us? Let's see. The KL divergence between $q(x)$ and $p(x)$ can be written as

$$
\mathbb{E}_{x \sim q(x)} [\log q(x) - \log p(x)].
$$

I will spare you the mathematical details, but if you plug in the posterior distribution for $p(x)$ and the variational approximation for $q(x)$, you will find:

$$
KL[q(u|\eta) || p(u|y, \theta)] = KL[q(u|\eta) || p(u | \theta)] - \mathbb{E}_{u \sim q(u|\eta)} \log p(y | u, \theta) + const.,
$$

where the constant term is constant with respect to the variational parameters $\eta$ we are seeking to find. This is what we'd like to minimise. Note that it sort of makes sense: the first term encourages the approximation to be close to the prior, and minimising the second implies maximising the expected likelihood under the approximation.

How do we compute this? The first term is easy. We defined $q(u \mid \eta)$ to be multivariate normal, and $p(u \mid \theta)$ is the GP prior, which is also multivariate normal. The KL divergence between two multivariate normals has a closed form, so no issues there.

The second term is more problematic. Really, the likelihood is a function of $f$, the value of the GP at the data points, and not at the inducing points u. These two are related as follows:

$$
p(y | u, \theta) = \int p(y | u, f, \theta) p(f | u, \theta) df = \mathbb{E}_{f \sim p(f | u, \theta)} [p(y | f, \theta)].
$$

Note that I didn't forget the $u$ in the last equality: the likelihood is actually conditionally independent of $u$ given $f$. If we know the GP value at the training locations, we don't need to know anything else.

OK but this isn't great. Now we have the following beast to deal with:

$$
-\mathbb{E}_{u \sim q(u|\eta)} \log \left[ \mathbb{E}_{f \sim p(f | u, \theta)} p(y |f, \theta) \right].
$$

Intuitively, this expression actually makes sense. To estimate the log likelihood using Monte Carlo samples, we could draw the value of the GP at the inducing points, $u$; then we draw the value of the GP at the data points given them and the hyperparameters, $f \mid u, \theta$; and then we use these to compute the log likelihood. But the problem is that this isn't terribly easy to optimise.

#### Jensen's inequality to the rescue

So how do we make progress? Well, it would be terrific if we could exchange the $\log$ and the second expectation. That's because, at a high level, we currently have

$$
\mathbb{E} \left[ \log (\mathbb{E} \left[X | Y\right]) \right].
$$

If instead we had

$$
\mathbb{E} \left[ \mathbb{E}[\log X | Y] \right],
$$

we could use the law of total expectation to instead compute

$$
\mathbb{E} \log X.
$$

In our case, this would mean computing

$$
\mathbb{E}_{f \sim q(f | \eta)} \log p(y | f, \theta)
$$

which, as we'll see later, we can do efficiently.

In fact, Jensen's inequality says that

$$
\log \mathbb{E} X \geq \mathbb{E} \log X.
$$

So if we're willing to use another bound, we can say that

$$
\log \left[ \mathbb{E}_{f \sim p(f | u, \theta)} p(y |f, \theta) \right] \geq \mathbb{E}_{f \sim p(f|u, \theta)} \log p(y | f, \theta),
$$

and so

$$
-\mathbb{E}_{u \sim q(u|\eta)} \log \left[ \mathbb{E}_{f \sim p(f | u, \theta)} p(y |f, \theta) \right] \leq -\mathbb{E}_{u \sim q(u | \eta)} \mathbb{E}_{f \sim p(f | u, \theta)} \log p(y |f, \theta).
$$

Why is using this bound OK? Well, note first that we're minimising this term. This term is the negation of an expected likelihood, so we're basically maximising a likelihood. By maximising this bound, we know that the true value is going to be at least as large. So we're pushing up a lower bound. Still, I'd essentially forgotten that this extra step was necessary; it means that we're not actually minimising the KL divergence exactly, which is interesting.

Now, using the law of total expectation, we can write the second part as

$$
-\mathbb{E}_{f \sim q(f | \eta, \theta)} \log p(y| f, \theta).
$$

Phew! OK. So if we're OK with making this additional approximation, we can
replace the complicated likelihood term with this one which, as we'll see in a
moment, we can compute.

#### Computing this bound

Where does that get us? Well, in most cases, a given outcome $y_i$ depends only on its local GP value $f_i$. In that case:

$$
p(y | f, \theta) = \prod_{i=1}^N p(y_i | f_i, \theta),
$$

and so

$$
-\mathbb{E}_{f \sim q(f | \eta, \theta)} \log p(y| f, \theta) = \\
-\mathbb{E}_{f \sim q(f | \eta, \theta)} \sum_{i=1}^N \log p(y_i| f_i, \theta) = \\
-\sum_{i=1}^N \mathbb{E}_{f_i \sim q(f_i | \eta, \theta)} \log p(y_i| f_i, \theta)
$$

This is now the sum of a bunch of 1D expectations, which can be solved efficiently and accurately using quadrature.

#### Last step: how do we actually find the implied function values?

OK so I missed out one key step. How do we actually find this distribution:

$$
q(f | \eta, \theta)
$$

This is where the neat trick comes in that actually originally motivated this blog post. Near the start, I mentioned that if

$$
				 \left[\begin{array}{c}  f^* \\ u  \end{array}\right] \sim  \mathcal{N}\left( \left[\begin{array}{c}  0 \\ 0  \end{array}\right]    ,    \left[\begin{array}{ c | c }    k(x^*, x^*) & k(x^*, z) \\    \hline    k(z, x^*) & k (z, z)  \end{array}\right]  \right)   =     \mathcal{N}\left( \left[\begin{array}{c}  0 \\ 0  \end{array}\right]    ,    \left[\begin{array}{ c | c }    K_{nn} & K_{mn} \\    \hline    K_{nm} & K_{mm}  \end{array}\right]  \right)	
					
$$

then the conditional distribution of $f^*$ given $u = a$ has mean

$$
\mu = K_{nm} K_{mm}^{-1} a
$$

and covariance

$$
\Sigma = K_{nn} - K_{nm}K_{mm}^{-1}K_{mn}.
$$

But what if $u$ itself has a distribution, so:

$$
u \sim \mathcal{N}(m, S)
$$

In that case, we can use some neat tricks. First, we have that

$$
\mu = \mathbb{E}[f^*|u, \eta] = K_{nm}K_{mm}^{-1}u,
$$

so

$$
\mathbb{E}[f^* | \eta] = \mathbb{E}[\mathbb{E}[f^* |u, \eta]] = K_{nm}K_{mm}^{-1} \mathbb{E}[u | \eta] = K_{nm}K_{mm}^{-1}m
$$

by the law of total expectation. Even better, we can use the law of total covariance to get the covariance. We have that

$$
\Sigma = \text{Cov}(f^*, f^*|\eta, u) = K_{mn} - K_{nm}K_{mm}^{-1}K_{mn}.
$$

By the [law of total covariance](https://en.wikipedia.org/wiki/Law_of_total_covariance), we have

$$
\text{Cov}(f^*, f^* | \eta) = \mathbb{E} [\text{Cov}(f^*, f^*|\eta, u)] + \text{Cov}(\mathbb{E}[f^* |\eta, u], \mathbb{E}[f^*|\eta, u])
$$

The first term here is just $\Sigma$ again, as it's constant. The second term is

$$
\text{Cov}(K_{nm}K_{mm}^{-1}u, K_{nm}K_{mm}^{-1}u|\eta) =  \\ K_{nm}K_{mm}^{-1} \text{Cov}(u, u|\eta)K_{mm}^{-1}K_{mn} = \\ K_{nm}K_{mm}^{-1}SK_{mm}^{-1}K_{mn}
$$

Defining $A = K_{nm}K_{mm}^{-1}$ gives:

$$
\text{Cov}(f^*, f^* | \eta) = K_{nn} - A K_{mn} + ASA^T = K_{nn} + A(S - K_{mm})A^T,
$$

as stated in the Hensman et al. paper.

To summarise, then, if we'd like to get the mean and covariance at a new set of points, we can use the laws of total covariance and total expectation to derive them from the variational distribution at the inducing points. When computing our approximate likelihood, we need just the marginal means and variances at the data points, which we can then use with quadrature.

#### Putting it all together & short summary

Now we have all the pieces we need. As stated before, the first part of the KL
divergence has a closed form. The second term involving the likelihood was more
tricky. We first had to bound it using Jensen's inequality. Then we could use
the laws of total expectation and covariance to get the means and variances
needed at each data point. Finally, we could use these together with quadrature
to compute the expectations required for our bound on the log likelihood.

And that's it! That's all we need. Note that this is all pretty neat. As long as
we can compute the 1D expectations, any likelihood will do. For some, like the
Poisson, we can even compute them analytically. For others, like the Bernoulli
with a logit or probit link, we can use quadrature, as mentioned. And the
largest matrix we have to invert is of size $M \times M$, which is manageable.

This blog post ended up a bit longer than I thought it would, and to be honest,
even after several years of thinking about this I'd still like to be a bit
clearer on some of the details here. Still, I hope some of the derivation is of
interest / use to you. If nothing else, I hope you'll find the use of law of
total expectation and total covariance slightly neat. And if there are any
problems / improvements to the derivation, please let me know, I'd love to hear
about them.
