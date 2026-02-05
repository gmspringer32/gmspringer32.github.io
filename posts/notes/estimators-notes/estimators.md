[Main Page](../../../)

[Projects](../../projects/projects-index.md)

# Statistical Estimators
## Graphical estimators for location scale families (QQ plot)
Quantile-Quantile (QQ) plots are used to compare the quantile functions of two distributions in order to see how alike the two distributions are. To do this we plot the theoretical quantiles on the x axis and the empirical quantiles on the y axis. The straighter the line is, the more alike the two distributions are. You can also fit a simple linear regression line to this and $\beta_0$ = the shift in means and $\beta_1$ = the ratio of the standard deviations, which means that if $\beta_0$ = 0 and $\beta_1$ = 1 then the distributions are the same.

In R you can plot QQ plots using qqplot:

**For normal distributions**
```{r}
# your data
x <- rnorm(100)

# theoretical normal distribution   
theoretical_q <- qnorm(ppoints(length(x)))

qqplot(theoretical_q, x,
       xlab = "Theoretical Quantiles",
       ylab = "Empirical Quantiles")
abline(0, 1, col = "red")
```
![](qqplot.png)


[Main Page](../../../)

[Projects](../../projects/projects-index.md)