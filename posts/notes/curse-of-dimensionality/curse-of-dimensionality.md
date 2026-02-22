
[Main Page](../../../)

[Projects](../../projects/projects-index.md)

[Back](../notes-index.md)

# Curse of Dimensionality
The basic idea of the curse of dimensionality is that when the number of dimensions of your data is much larger than the size of your data, the volume of the space increases so fast that the available data becomes sparse. This has applications in many areas but here we will just talk about its place in machine learning.

Suppose X is uniformly distributed from [0,1]. Suppose we want to use KNN to predict a test observation using observations that are within 10% of the range of X that is closest to that test observation. For example, in order to predict the response for a test observation with X = 0.6 then we will use the observations in the range [0.55, 0.65]. On average what fraction of the available observations will we use to make the prediction?

Well that will be 1/10 of the data or 10% on average (that is if you say that when X is 0.02 for example we test from [0, 0.1] instead of [0, 0.07]). 

Great, but what happens when instead of predicting for one X you bump it up to two? Now we are trying to predict an observation that is within 10% of $X_1$ and 10% of $X_2$. On average now, how many of the available observations will be available?

For this we just take $0.1^2$ which is 1% of the observations on average (assuming that $X_1$ and $X_2$ are independent you can just multiply the probabilities together). 

What if we have 100 predictors? Then it would be $0.1^{100}$ which is tiny. So you can see if you do not have a lot of data to work with, this could be a problem.

[Main Page](../../../)

[Projects](../../projects/projects-index.md)

[Back](../notes-index.md)
