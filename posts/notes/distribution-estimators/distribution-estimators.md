[Main Page](../../../)

[Projects](../../projects/projects-index.md)

# Statistical Distribition Estimates (Empirical CDFs)
So you have your data, but you have no idea what distribution it follows, you need to estimate your CDF and that is called your empirical CDF (ECDF).

## ECDFs
Suppose we observe data

$$
x_1, x_2, \dots, x_n.
$$

The empirical cumulative distribution function (ECDF) is defined as

$$
\hat{F}_n(x) = \frac{1}{n} \sum_{i=1}^{n} \mathbf{1}(x_i \le x),
$$

where $\mathbf{1}(x_i \le x)$ is the indicator function, equal to 1 if $x_i \le x$ and 0 otherwise.

Thus, $\hat{F}_n(x)$ represents the **proportion of observations less than or equal to $x$**.

### Step 1: Sort the data

Let the ordered sample be

$$
x_{(1)} \le x_{(2)} \le \dots \le x_{(n)}.
$$

### Step 2: Assign cumulative probabilities

At each ordered observation,

$$
\hat{F}_n(x_{(k)}) = \frac{k}{n}, \quad k = 1,2,\dots,n.
$$


### Example

Suppose the sample is

$$
3, 7, 2, 9, 5.
$$

After sorting:

$$
2, 3, 5, 7, 9.
$$

Since $n = 5$, the ECDF values at the ordered points are:

| $x_{(k)}$ | $\hat{F}_n(x_{(k)})$ |
|------------|-----------------------|
| 2 | $\frac{1}{5} = 0.2$ |
| 3 | $\frac{2}{5} = 0.4$ |
| 5 | $\frac{3}{5} = 0.6$ |
| 7 | $\frac{4}{5} = 0.8$ |
| 9 | $1$ |

For example,

$$
\hat{F}_n(6) = \frac{3}{5} = 0.6,
$$

since three observations are less than or equal to 6.


### Properties

- The ECDF is a **step function**.
- It increases by $\frac{1}{n}$ at each data point.
- It is **right-continuous**.
- $\hat{F}_n(-\infty) = 0$ and $\hat{F}_n(\infty) = 1$.



[Main Page](../../../)

[Projects](../../projects/projects-index.md)