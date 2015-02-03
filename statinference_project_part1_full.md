# Statistical Inference Course Project, Part 1: Simulation Exercises



The exponential distribution can be simulated in R with `rexp(n, lambda)` where
`lambda` $\lambda$ is the rate parameter. The mean of exponential distribution is 
$1/\lambda$ and the standard deviation is also $1/\lambda$. For this simulation,
we set $\lambda=0.2$. In this simulation, we investigate the distribution of
averages of 40 numbers sampled from exponential distribution with $\lambda=0.2$.

Let's do a thousand simulated averages of 40 exponentials.


```r
set.seed(3)
lambda <- 0.2
num_sim <- 1000
sample_size <- 40
sim <- matrix(rexp(num_sim*sample_size, rate=lambda), num_sim, sample_size)
row_means <- rowMeans(sim)
```

The distribution of sample means is as follows.


```r
# plot the histogram of averages
hist(row_means, breaks=50, prob=TRUE,
     main="Distribution of averages of samples,
     drawn from exponential distribution with lambda=0.2",
     xlab="")
# density of the averages of samples
lines(density(row_means))
# theoretical center of distribution
abline(v=1/lambda, col="red")
# theoretical density of the averages of samples
xfit <- seq(min(row_means), max(row_means), length=100)
yfit <- dnorm(xfit, mean=1/lambda, sd=(1/lambda/sqrt(sample_size)))
lines(xfit, yfit, pch=22, col="red", lty=2)
# add legend
legend('topright', c("simulation", "theoretical"), lty=c(1,2), col=c("black", "red"))
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 

The distribution of sample means is centered at 4.9866
