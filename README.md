## The result of updating step by step is the same as updating at once

Suppose that you have finite samples: $X^{(1)}, X^{(2)},\cdots,X^{(n)}$. Then the result of (1) Finding the posterior distribution of parameters at once is the same as (2) Finding the posterior distribution of parameters iteratively using the following algorithm.

<div style="background-color: #f2c2f2; padding: 10px; border-radius: 5px; font-family: 'Times New Roman', Times, serif;">

Algorithm:

Initialize Prior Distribution $P(\theta)$ whatever you want.

Compute the distribution $\omega_1(\theta,X^{(1)})$ using the following formulas: $\omega_1(\theta,X^{(1)}) = \frac{P(X^{(1)}|\theta)P(\theta)}{P(X^{(1)})}$

Loop $i$ from $2$ to $n$:

  $~~~~~~$ Compute the distribution $\omega$ using the following formulas: 
  
  $~~~~~~ \omega_i(\theta,X^{(1)},\cdots,X^{(i)}) = \frac{P(X^{(1)},\cdots,X^{(i)}|\theta)\omega_{i-1}(\theta,X^{(1)},\cdots,X^{(i-1)})}{\int_{\theta}P(X^{(1)},\cdots,X^{(i)}|\theta)\omega_{i-1}(\theta,X^{(1)},\cdots,X^{(i-1)}) d\theta}$

</div>

$~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~$


Now, we want to prove that for each $i$ from $1$ to $n$, the
$w_i(\theta,X^{(1)},\cdots,X^{(i)}) = P(\theta|X^{(1)},\cdots,X^{(i)})$.
(The algorithm does give the posterior distribution of Bayesian inference)



Proof: 

We can prove by induction.

When $i = 1$: $\omega_1(\theta,X^{(1)}) = \frac{P(X^{(1)}|\theta)P(\theta)}{P(X^{(1)})} = P(\theta|X^{(1)})$, which proves that it is indeed the posterior distribution.

When $i = 2$: Now we have two samples $X^{(1)}$ and $X^{(2)}$.

Since we compute the $\omega_1(\theta,X^{(1)})$ at first, we have already got:

$$
\begin{align}
& ~ \omega_1(\theta,X^{(1)}) \\
= &~ \frac{P(X^{(1)}|\theta)P(\theta)}{P(X^{(1)})}
\end{align}
$$

Then, we use $\omega_1(\theta,X^{(1)})$ to be the prior distribution of next iteration:

$$
\begin{align}
&~ w_2(\theta,X^{(1)},X^{(2)}) \\
= &~ \frac{P(X^{(2)}|\theta)\omega_1(\theta,X^{(1)})}{\int_{\theta}P(X^{(2)}|\theta)\omega_1(\theta,X^{(1)})d\theta} \\
= &~ \frac{P(X^{(2)}|\theta)\frac{P(X^{(1)}|\theta)P(\theta)}{P(X^{(1)})}}{\int_{\theta}P(X^{(2)}|\theta)\frac{P(X^{(1)}|\theta)P(\theta)}{P(X^{(1)})}d\theta} \\
= &~ \frac{P(X^{(2)}|\theta)\frac{P(X^{(1)}|\theta)P(\theta)}{P(X^{(1)})}}{\frac{1}{P(X^{(1)})}\int_{\theta}P(X^{(2)}|\theta)P(X^{(1)}|\theta)P(\theta)d\theta} \\
= &~ \frac{P(X^{(2)}|\theta)P(X^{(1)}|\theta)P(\theta)}{\int_{\theta}P(X^{(2)}|\theta)P(X^{(1)}|\theta)P(\theta)d\theta} \\
\end{align}
$$

Now, since when given a fixed $\theta$, samples are pairwisely independent (this is the basic assumption of statistics, samples should be independent under the same models), which means that:

$$
\begin{align}
&~ P(X^{(1)},X^{(2)},\cdots,X^{(n)}|\theta) \\
= &~ P(X^{(1)}|\theta)P(X^{(2)}|X^{(1)},\theta)\cdots P(X^{(n)}|X^{(1)},X^{(2)},\cdots,X^{(n-1)},\theta)\\
= &~ P(X^{(1)}|\theta)P(X^{(2)}|\theta)\cdots P(X^{(n)}|\theta)
\end{align}
$$

Continue on $\frac{P(X^{(2)}|\theta)P(X^{(1)}|\theta)P(\theta)}{\int_{\theta}P(X^{(2)}|\theta)P(X^{(1)}|\theta)P(\theta)d\theta}$ we have,

$$
\begin{align}
&~ \omega_2(\theta,X^{(1)},X^{(2)}) \\
= &~ \frac{P(X^{(2)}|\theta)P(\theta|X^{(1)})}{\int_{\theta}P(X^{(2)}|\theta)P(\theta|X^{(1)})d\theta} \\
= &~ \frac{P(X^{(2)}|\theta)P(X^{(1)}|\theta)P(\theta)}{\int_{\theta}P(X^{(2)}|\theta)P(X^{(1)}|\theta)P(\theta)d\theta} \\
= &~ \frac{P(X^{(1)},X^{(2)}|\theta)P(\theta)}{\int_{\theta}P(X^{(1)},X^{(2)}|\theta)P(\theta)d\theta} \\
= &~ \frac{P(X^{(1)},X^{(2)},\theta)}{\int_{\theta}P(X^{(1)},X^{(2)},\theta)d\theta} \\
= &~ \frac{P(X^{(1)},X^{(2)},\theta)}{P(X^{(1)},X^{(2)})} \\
= &~ P(\theta|X^{(1)},X^{(2)})
\end{align}
$$

This proves that $\omega_2(\theta,X^{(1)},X^{(2)})$ is indeed the posterior distribution $P(\theta|X^{(1)},X^{(2)})$.

Now, we start the induction part.

Suppose that when $i = k$, the $w_i(\theta,X^{(1)},\cdots,X^{(i)}) = P(X^{(1)},\cdots,X^{(i)}|\theta)$ holds. That is $w_k(\theta,X^{(1)},\cdots,X^{(k)}) = P(X^{(1)},\cdots,X^{(k)}|\theta)$

Then, when $i = k+1$, we have samples $X^{(1)}, X^{(2)},\cdots,X^{(k+1)}$.

$$
\begin{align}
&~ \omega_{k+1}(\theta,X^{(1)}, X^{(2)},\cdots,X^{(k+1)}) \\
=&~ \frac{P(X^{(k+1)}|\theta)P(\theta|X^{(1)},\cdots,X^{(k)})}{\int_{\theta}P(X^{(k+1)}|\theta)P(\theta|X^{(1)},\cdots,X^{(k)})d\theta} \\
= &~ \frac{P(X^{(k+1)}|\theta)\frac{P(X^{(k)}|X^{(1)},\cdots,\theta)P(\theta)}{P(X^{(1)},\cdots,X^{(k)})}}{\int_{\theta}P(X^{(k+1)}|\theta)\frac{P(X^{(1)},\cdots,X^{(k)}|\theta)P(\theta)}{P(X^{(1)},\cdots,X^{(k)})}d\theta} \\
= &~ \frac{P(X^{(k+1)}|\theta)\frac{P(X^{(1)},\cdots,X^{(k)}|\theta)P(\theta)}{P(X^{(1)},\cdots,X^{(k)})}}{\frac{1}{P(X^{(1)},\cdots,X^{(k)})}\int_{\theta}P(X^{(k+1)}|\theta)P(X^{(1)},\cdots,X^{(k)}|\theta)P(\theta)d\theta} \\
= &~ \frac{P(X^{(k+1)}|\theta)P(X^{(1)},\cdots,X^{(k)}|\theta)P(\theta)}{\int_{\theta}P(X^{(k+1)}|\theta)P(X^{(1)},\cdots,X^{(k)}|\theta)P(\theta)d\theta} \\
= &~ \frac{P(X^{(k+1)}|\theta, X^{(1)},\cdots,X^{(k)})P(X^{(1)},\cdots,X^{(k)}|\theta)P(\theta)}{\int_{\theta}P(X^{(k+1)}|\theta,X^{(1)},\cdots,X^{(k)})P(X^{(1)},\cdots,X^{(k)}|\theta)P(\theta)d\theta} \\
= &~ \frac{P(X^{(1)},\cdots,X^{(k)},X^{(k+1)}|\theta)P(\theta)}{\int_{\theta}P(X^{(1)},\cdots,X^{(k)},X^{(k+1)}|\theta)P(\theta)d\theta} \\
= &~ \frac{P(X^{(1)},\cdots,X^{(k)},X^{(k+1)}|\theta)P(\theta)}{P(X^{(1)},\cdots,X^{(k)},X^{(k+1)})} \\
= & P(\theta|X^{(1)},\cdots,X^{(k)},X^{(k+1)})
\end{align}
$$

For summary, you show that if 

$$
\begin{align}
\omega_{k}(\theta,X^{(1)}, X^{(2)},\cdots,X^{(k)}) = P(\theta|X^{(1)},\cdots,X^{(k)})
\end{align}
$$

we can prove that 

$$
\begin{align}
\omega_{k+1}(\theta,X^{(1)}, X^{(2)},\cdots,X^{(k+1)}) = P(\theta|X^{(1)},\cdots,X^{(k+1)})
\end{align}
$$

We finish the induction reasoning part of proof.
