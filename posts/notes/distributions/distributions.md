[Main Page](../../../)

[Projects](../../projects/projects-index.md)

# Common Statistical Distributions

## Continuous Distributions

### Normal (Gaussian)
Use: Measurement error, natural phenomena, Central Limit Theorem  
Parameters: mean μ, variance σ²

PDF:
$$
f(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)
$$

CDF:
$$
F(x) = \Phi\left(\frac{x-\mu}{\sigma}\right)
$$

Mean: μ  
Variance: σ²

---

### Uniform
Use: Complete uncertainty over an interval  
Parameters: a < b

PDF:
$$
f(x) = \frac{1}{b-a}, \quad a \le x \le b
$$

CDF:
$$
F(x) = \frac{x-a}{b-a}, \quad a \le x \le b
$$

Mean: (a + b) / 2  
Variance: (b − a)² / 12

---

### Exponential
Use: Time until an event (memoryless property)  
Parameters: rate λ > 0

PDF:
$$
f(x) = \lambda e^{-\lambda x}, \quad x \ge 0
$$

CDF:
$$
F(x) = 1 - e^{-\lambda x}
$$

Mean: 1 / λ  
Variance: 1 / λ²

---

### Gamma
Use: Waiting time for multiple events  
Parameters: shape α > 0, rate β > 0

PDF:
$$
f(x) = \frac{\beta^\alpha}{\Gamma(\alpha)} x^{\alpha-1} e^{-\beta x}, \quad x \ge 0
$$

CDF:
$$
F(x) = \frac{\gamma(\alpha, \beta x)}{\Gamma(\alpha)}
$$

Mean: α / β  
Variance: α / β²

---

### Beta
Use: Probabilities and proportions; Bayesian priors  
Parameters: α > 0, β > 0

PDF:
$$
f(x) = \frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha,\beta)}, \quad 0 \le x \le 1
$$

CDF:
$$
F(x) = I_x(\alpha,\beta)
$$

Mean: α / (α + β)  
Variance: (αβ) / [(α + β)²(α + β + 1)]

---

### Lognormal
Use: Positive skewed data (income, lifetimes)  
Parameters: μ, σ² (of log X)

PDF:
$$
f(x) = \frac{1}{x\sigma\sqrt{2\pi}} \exp\left(-\frac{(\ln x - \mu)^2}{2\sigma^2}\right)
$$

CDF:
$$
F(x) = \Phi\left(\frac{\ln x - \mu}{\sigma}\right)
$$

Mean: exp(μ + σ² / 2)  
Variance: (exp(σ²) − 1) exp(2μ + σ²)

---

## Discrete Distributions

### Bernoulli
Use: Single yes/no trial  
Parameters: success probability p

PMF:
$$
P(X=x) = p^x (1-p)^{1-x}, \quad x \in \{0,1\}
$$

CDF:
$$
F(x) =
\begin{cases}
0 & x < 0 \\
1-p & 0 \le x < 1 \\
1 & x \ge 1
\end{cases}
$$

Mean: p  
Variance: p(1 − p)

---

### Binomial
Use: Number of successes in n trials  
Parameters: n, p

PMF:
$$
P(X=k) = \binom{n}{k} p^k (1-p)^{n-k}
$$

CDF:
$$
F(k) = \sum_{i=0}^k \binom{n}{i} p^i (1-p)^{n-i}
$$

Mean: np  
Variance: np(1 − p)

---

### Geometric
Use: Trials until first success  
Parameters: p

PMF:
$$
P(X=k) = (1-p)^{k-1} p, \quad k = 1,2,\dots
$$

CDF:
$$
F(k) = 1 - (1-p)^k
$$

Mean: 1 / p  
Variance: (1 − p) / p²

---

### Poisson
Use: Count of rare events over time/space  
Parameters: rate λ > 0

PMF:
$$
P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!}
$$

CDF:
$$
F(k) = \sum_{i=0}^k \frac{\lambda^i e^{-\lambda}}{i!}
$$

Mean: λ  
Variance: λ

---

### Negative Binomial
Use: Failures until r successes; overdispersed counts  
Parameters: r, p

PMF:
$$
P(X=k) = \binom{k+r-1}{k} (1-p)^k p^r
$$

CDF:
$$
F(k) = \sum_{i=0}^k \binom{i+r-1}{i} (1-p)^i p^r
$$

Mean: r(1 − p) / p  
Variance: r(1 − p) / p²

---

### Hypergeometric
Use: Sampling without replacement  
Parameters: population N, successes K, sample size n

PMF:
$$
P(X=k) = \frac{\binom{K}{k} \binom{N-K}{n-k}}{\binom{N}{n}}
$$

CDF:
$$
F(k) = \sum_{i=0}^k \frac{\binom{K}{i} \binom{N-K}{n-i}}{\binom{N}{n}}
$$

Mean: n(K / N)  
Variance: n(K / N)(1 − K / N)\frac{N − n}{N − 1}

[Main Page](../../../)

[Projects](../../projects/projects-index.md)