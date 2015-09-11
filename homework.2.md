# Homework 2
Alexander Tuzhikov  
September 10, 2015  

##

Suppose that the number of web hits to a particular site are approximately normally distributed with a mean of 100 hits per day and a standard deviation of 10 hits per day. What's the probability that a given day has fewer than 93 hits per day expressed as a percentage to the nearest percentage point?


```r
pnorm(93, mean=100, sd=10)
```

```
## [1] 0.2419637
```

##

The probability that a manuscript gets accepted to a journal is 12% (say). However, given that a revision is asked for, the probability that it gets accepted is 90%. Is it possible that the probability that a manuscript has a revision asked for is 20%?

```r
0.045/((0.045*0.95) - 0.95*0.88)
```

```
## [1] -0.05672865
```

##

Suppose that the number of web hits to a particular site are approximately normally distributed with a mean of 100 hits per day and a standard deviation of 10 hits per day. What's the probability that a given day has fewer than 93 hits per day expressed as a percentage to the nearest percentage point?

```r
round(qnorm(p = 0.95, mean = 100, sd = 10, lower.tail = TRUE))
```

```
## [1] 116
```
##

Suppose 5% of housing projects have issues with asbestos. The sensitivity of a test for asbestos is 93% and the specificity is 88%. What is the probability that a housing project has no asbestos given a negative test expressed as a percentage to the nearest percentage point?


```r
#P(Ac|T−)=P(T−|Ac)P(Ac)/(P(T−|Ac)P(Ac)+P(T−|A)P(A))
(0.88 * 0.95) / (0.88 * 0.95 + 0.07 * 0.05)
```

```
## [1] 0.9958309
```

##

Suppose that the number of web hits to a particular site are approximately normally distributed with a mean of 100 hits per day and a standard deviation of 10 hits per day.
What number of web hits per day represents the number so that only 5% of days have more hits? Express your answer to 3 decimal places.


```r
round(qnorm(.95, mean = 100, sd = 10), 3)
```

```
## [1] 116.449
```

## 

Suppose that the number of web hits to a particular site are approximately normally distributed with a mean of 100 hits per day and a standard deviation of 10 hits per day.
Imagine taking a random sample of 50 days. What number of web hits would be the point so that only 5% of averages of 50 days of web traffic have more hits? Express your answer to 3 decimal places. 

```r
round(qnorm(0.05,mean = 100, sd = (10^2)/50, lower.tail = FALSE),3)
```

```
## [1] 103.29
```

##

You don't believe that your friend can discern good wine from cheap. Assuming that you're right, in a blind test where you randomize 6 paired varieties (Merlot, Chianti, ...) of cheap and expensive wines
What is the change that she gets 5 or 6 right expressed as a percentage to one decimal place?


```r
round(pbinom(4, prob = .5, size = 6, lower.tail = FALSE) * 100, 1)
```

```
## [1] 10.9
```

##

Consider a uniform distribution. If we were to sample 100 draws from a a uniform distribution (which has mean 0.5, and variance 1/12) and take their mean, Xˉ
What is the approximate probability of getting as large as 0.51 or larger expressed to 3 decimal places?


```r
round(pnorm(0.51, mean = 0.5, sd = sqrt(1/12/100), lower.tail = FALSE),3)
```

```
## [1] 0.365
```

##

If you roll ten standard dice, take their average, then repeat this process over and over and construct a histogram,
what would it be centered at?

```r
(60+10)/10/2
```

```
## [1] 3.5
```

##

If you roll ten standard dice, take their average, then repeat this process over and over and construct a histogram,
what would be its variance expressed to 3 decimal places?

```r
mean((1 : 6 - 3.5)^2 / 10)
```

```
## [1] 0.2916667
```

##

The number of web hits to a site is Poisson with mean 16.5 per day.
What is the probability of getting 20 or fewer in 2 days expressed as a percentage to one decimal place?


```r
round(ppois(20, lambda = 16.5 * 2) * 100, 1)
```

```
## [1] 1
```
