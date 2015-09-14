# Homework 4
Alexander Tuzhikov  
September 14, 2015  

##

Load the data set mtcars in the datasets R package. Assume that the data set mtcars is a random sample. Compute the mean MPG, xˉ, of this sample.
You want to test whether the true MPG is μ0 or smaller using a one sided 5% level test. (H0:μ=μ0 versus Ha:μ<μ0). Using that data set and a Z test:
Based on the mean MPG of the sample xˉ, and by using a Z test: what is the smallest value of μ0 that you would reject for (to two decimal places)?


```r
data("mtcars")
xdash<- mean(mtcars$mpg)
xdash
```

```
## [1] 20.09062
```

```r
sdmtcars<- sd(mtcars$mpg)
z <- qnorm(.05)
mu0 <- xdash - z * sdmtcars / sqrt(nrow(mtcars))
round(mu0, 2)
```

```
## [1] 21.84
```

##

Consider again the mtcars dataset. Use a two group t-test to test the hypothesis that the 4 and 6 cyl cars have the same mpg. Use a two sided test with unequal variances.
Do you reject at the 5% level (enter 0 for no, 1 for yes).

What is the P-value to 4 decimal places expressed as a proportion?


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following objects are masked from 'package:stats':
## 
##     filter, lag
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
mtcars %>% filter(cyl%in%c(4,6)) -> mtcars.4.6.cyl
mtcars.4.6.cyl %>% filter(cyl==4) -> mtcars.4.cyl
mtcars.4.6.cyl %>% filter(cyl==6) -> mtcars.6.cyl

t.test(mtcars.4.cyl$mpg, mtcars.6.cyl$mpg, var.equal = FALSE, paired = FALSE)
```

```
## 
## 	Welch Two Sample t-test
## 
## data:  mtcars.4.cyl$mpg and mtcars.6.cyl$mpg
## t = 4.7191, df = 12.956, p-value = 0.0004048
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##   3.751376 10.090182
## sample estimates:
## mean of x mean of y 
##  26.66364  19.74286
```

##

A sample of 100 men yielded an average PSA level of 3.0 with a sd of 1.1. What are the complete set of values that a 5% two sided Z test of H0:μ=μ0 would fail to reject the null hypothesis for?
Enter the lower value to 2 decimal places.

Enter the upper value to 2 decimal places. 


```r
xdash<- 3
sd.men<- 1.1
z <- qnorm(.025)
mu0 <- xdash - z * sd.men / sqrt(100)
round(mu0, 2)
```

```
## [1] 3.22
```

```r
#same stuff, but for the upper bound
z <- qnorm(1-.025)
mu0 <- xdash - z * sd.men / sqrt(100)
round(mu0, 2)
```

```
## [1] 2.78
```

##

You believe the coin that you're flipping is biased towards heads. You get 55 heads out of 100 flips.
What's the exact relevant pvalue to 4 decimal places (expressed as a proportion)?

Would you reject a 1 sided hypothesis at α=.05? (0 for no 1 for yes)?


```r
binom.test(x=c(55, 100-55), p = 0.5, alternative = "greater")
```

```
## 
## 	Exact binomial test
## 
## data:  c(55, 100 - 55)
## number of successes = 55, number of trials = 100, p-value = 0.1841
## alternative hypothesis: true probability of success is greater than 0.5
## 95 percent confidence interval:
##  0.4628896 1.0000000
## sample estimates:
## probability of success 
##                   0.55
```

##

A web site was monitored for a year and it received 520 hits per day. In the first 30 days in the next year, the site received 15,800 hits. Assuming that web hits are Poisson.
Give an exact one sided P-value to the hypothesis that web hits are up this year over last to four significant digits (expressed as a proportion).

Does the one sided test reject (0 for no 1 for yes)?


```r
poisson.test(x = 15800, T = 30, r = 520, alternative = "greater")
```

```
## 
## 	Exact Poisson test
## 
## data:  15800 time base: 30
## number of events = 15800, time base = 30, p-value = 0.05533
## alternative hypothesis: true event rate is greater than 520
## 95 percent confidence interval:
##  519.7938      Inf
## sample estimates:
## event rate 
##   526.6667
```

##

A confidence interval for the mean contains:
All of the values of the hypothesized mean for which we would fail to reject with α=1−Conf.Level.
All of the values of the hypothesized mean for which we would fail to reject with 2α=1−Conf.Level.
All of the values of the hypothesized mean for which we would reject with α=1−Conf.Level.
All of the values of the hypothesized mean for which we would reject with 2α=1−Conf.Level.


```r
1
```

```
## [1] 1
```

##

Consider two problems previous. Assuming that 10 purchases per day is a benchmark null value, that days are iid and that the standard deviation is 4 purchases for day. Suppose that you plan on sampling 100 days. What would be the power for a one sided 5% Z mean test that purchases per day have increased under the alternative of μ=11 purchase per day?
Give your result as a proportion to 3 decimal places.


```r
power <- pnorm(10 + qnorm(.95) * .4, mean = 11, sd = .4, lower.tail = FALSE)
```

##

Researchers would like to conduct a study of healthy adults to detect a four year mean brain volume loss of .01 mm3. Assume that the standard deviation of four year volume loss in this population is .04 mm3.
What is necessary sample size for the study for a 5% one sided test versus a null hypothesis of no volume loss to achieve 80% power? (Always round up)


```r
n <- (qnorm(.95) + qnorm(.8)) ^ 2 * .04 ^ 2 / .01^2
```

##

In a court of law, all things being equal, if via policy you require a lower standard of evidence to convict people then

* Less guilty people will be convicted.
* More innocent people will be convicted.
* More Innocent people will be not convicted.


```r
2
```

```
## [1] 2
```

##

Consider the mtcars data set.
Give the p-value for a t-test comparing MPG for 6 and 8 cylinder cars assuming equal variance, as a proportion to 3 decimal places.

Give the associated P-value for a z test.

Give the common standard deviation estimate for MPG across cylinders to 3 decimal places.

Would the t test reject at the two sided 0.05 level (0 for no 1 for yes)?


```r
mt8<- mtcars%>%filter(cyl==8)
mt6<- mtcars%>%filter(cyl==6)
n8<-nrow(mt8)
n6<-nrow(mt6)
s8<- sd(mt8$mpg)
s6<- sd(mt6$mpg)
m8<- mean(mt8$mpg)
m6<- mean(mt6$mpg)
t.test(mt6$mpg, mt8$mpg, alternative = "two.sided", var.equal = TRUE)
```

```
## 
## 	Two Sample t-test
## 
## data:  mt6$mpg and mt8$mpg
## t = 4.419, df = 19, p-value = 0.0002947
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  2.443809 6.841905
## sample estimates:
## mean of x mean of y 
##  19.74286  15.10000
```

```r
mixprob <- (n8 - 1) / (n8 + n6 - 2)
s <- sqrt(mixprob * s8 ^ 2  +  (1 - mixprob) * s6 ^ 2)
z <- (m8 - m6) / (s * sqrt(1 / n8 + 1 / n6))
pz <- 2 * pnorm(-abs(z))
```

##

The Bonferonni correction controls this

* False discovery rate
* The familywise error rate
* The rate of true rejections
* The number of true rejections


```r
2
```

```
## [1] 2
```
