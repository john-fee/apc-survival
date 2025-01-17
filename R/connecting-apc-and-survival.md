Connecting continuous survival analysis, discrete survival analysis, and
age-period cohort analysis
================
John Fee
2024-07-03

- [Continuous survival times](#continuous-survival-times)
  - [Survival function](#survival-function)
  - [Hazard rate](#hazard-rate)
  - [Mean residual life](#mean-residual-life)
  - [AFT models](#aft-models)
- [Discrete failure times](#discrete-failure-times)
  - [Survival function](#survival-function-1)

# Continuous survival times

## Survival function

We are interested in inferring the probability of an individual
surviving past a constant time $x$, where $X$ is a continuous r.v.
representing their survival time and $S(x)$ is the function
$S(x) = P(X > x)$.

Some basic properties of $S(x)$:

From the definition of a CDF $$\begin{align}
S(x) &= 1 - P(X \leq x)\\
&= 1 - F(x)\\
\implies \frac{d S(x)}{dx} &= \frac{d}{dx}(1 - F(x))\\
f(x) &= - \frac{d S(x)}{dx}
\end{align}$$

$S(x)$ is also a decreasing function with range $[0,1]$.

## Hazard rate

With continuous $X$, the hazard rate or intensity function is given by

$$\begin{equation}
h(x) = \frac{f(x)}{S(x)}
\end{equation}$$ or equivalently $$\begin{equation}
h(x) = -\frac{d}{dx}\ln S(x)
\end{equation}$$

The latter is useful because we can define the cumulative hazard $H(x)$
where $$\begin{align}
H(x) &= \int\limits_{0}^{x}h(u)du\\
&= - \ln S(x)
\end{align}$$

which means we can connect the survival time to the cumulative hazard.
$$\begin{align}
S(x) &= \exp(-H(x))\\
&= \exp (-\int\limits_{0}^{x}h(u)du)
\end{align}$$

## Mean residual life

The expected lifetime remaining to an individual who has was alive until
time $x$ is given by the area under the survival curve to the right of
$x$ normalized by the total AUC. $$\begin{align}
\text{mrl}(x) &= \dfrac{\int\limits_{x}^{\infty}(t-x)f(t)dt}{S(x)}\\
&= \dfrac{\int\limits_{x}^{\infty}S(t)dt}{S(x)}
\end{align}$$

Of obvious interest is the expected lifetime of a new individual
($x = 0$) which is given by $$\begin{align}
\text{mrl}(0) &= \text{E}[X]\\
&= \int\limits_{0}^{\infty}tf(t)dt\\
&= \int\limits_{0}^{\infty}S(t)dt
\end{align}$$

## AFT models

Consider a vector of possibly time-varying covariates $\mathbf{Z}(x)$
associated with the failure time $X$ ($X > 0$) of an individual.

The AFT approach to modeling the failure times would be to assume a
model of the following form:

$$\begin{equation}
Y = \ln X = \mu + \mathbf{\beta}'\mathbf{Z} + \sigma W
\end{equation}$$

where $\mu$ is a location parameter, $\sigma$ is a scale parameter,
$\beta$ is a vector of regression coefficients, and $W$ is a r.v.
representing the error distribution.

Why is this called Accelerated Failure Time? Consider the case where
$\mathbf{Z} = \mathbf{0}$. Then $$\begin{align}
X &= \exp \left(\mu + \sigma W\right)
\end{align}$$

Let us denote the survival function of $X$ when
$\mathbf{Z} = \mathbf{0}$ as $S_{0}(x)$.

Now consider the survival function for $X$ conditional on $\mathbf{Z}$.

$$\begin{align}
P(X > x | \mathbf{Z}) &= P(\exp \left(\mu + \mathbf{\beta}'\mathbf{Z} + \sigma W\right) > x | \mathbf{Z})\\
&= P(\exp \left(\mu + \sigma W\right) > x \exp (-\mathbf{\beta}'\mathbf{Z}) | \mathbf{Z})
\end{align}$$

Note that the left side quantity is $X | \mathbf{Z} = \mathbf{0}$, and
the right side quantity is a constant. Therefore

$$\begin{align}
P(X > x | \mathbf{Z})  &= S_{0}(x \exp (-\mathbf{\beta}'\mathbf{Z}))
\end{align}$$

Covariates have the effect of increasing or decreasing the time scale of
the individual.

# Discrete failure times

## Survival function

We are interested in inferring the probability of an individual
surviving past a constant time $x$, where $X$ is a discrete r.v. that
can take on values in the set $\{x_{j}\}$ with $j \in \mathcal{Z}$, $X$
has pmf $f(x_{j})$ where $x_{1} < x_{2} < \ldots$. The survival function
$S(x)$ is therefore:

$$\begin{align}
S(x) &= P(X > x)\\
&= \sum\limits_{x_{j} > x} f(x_{j})
\end{align}$$
