Overview
========

In this project we will investigate the exponential distribution in R
and compare it with the Central Limit Theorem. The mean of exponential
distribution is 1/lambda and the standard deviation is also 1/lambda. We
will set lambda = 0.2 for all of the simulations. We ill investigate the
distribution of averages of 40 exponentials. \# Simulation First we run
a simulation, then calcualte the sample mean and variance and
theoretcial mean and variance.

    lambda <- 0.2
    n <- 40
    B <- 1000
    set.seed(10)
    sim <- matrix(rexp(n*B, lambda), B, n)
    means <- apply(sim, 1, mean)
    sampleMean <- mean(means)
    theoreticalMean <- 1/lambda
    sampleVar <- var(means)
    theoreticalVar <- (1/lambda)^2/n

Next we display a histogram of the simulation and compare to the
theoretical mean and variance with the sample mean and variance.

    hist(means, col = "green", breaks = 30, main = "Histogram of exponential random variants with lambda = 0.2", xlab = "Sample Means of 40 Replications")
    text(7,80, paste("Sample Mean = ", round(sampleMean, 4), "\n Theorectical Mean =", theoreticalMean, "\n", "\n Sample Variance = ", round(sampleVar, 4), "\n Theorectical Variance =", theoreticalVar))

![](Exponential-Sample_files/figure-markdown_strict/unnamed-chunk-2-1.png)

In order to show that the distribution is approximatly normal, we
overlay a density plot.

    hist(means, col = "blue", breaks = 30, main = "Histogram of exponential random variants compared with normal", xlab = "Sample Means of 40 Replications", prob = TRUE)
    lines(density(means), col = "red")

![](Exponential-Sample_files/figure-markdown_strict/unnamed-chunk-3-1.png)

Now we will calculate a 95% confidence interval for the exponential
sample mean.

    t.test(means)$conf.int

    ## [1] 4.994869 5.095250
    ## attr(,"conf.level")
    ## [1] 0.95
