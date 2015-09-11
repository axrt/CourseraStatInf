# Homework 3
Alexander Tuzhikov  
September 11, 2015  

#Homework

##
Load the data set mtcars in the datasets R package. Calculate a 95% confidence interval to the nearest MPG for the variable mpg.
What is the lower endpoint of the interval?
What is the upper endpoint of the interval?


```r
data("mtcars")
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```

```r
round(t.test(mtcars$mpg)$conf.int)
```

```
## [1] 18 22
## attr(,"conf.level")
## [1] 0.95
```

##
Suppose that standard deviation of 9 paired differences is 1. What value would the average difference have to be so that the lower endpoint of a 95% students t confidence interval touches zero?
Give the number here to two decimal places


```r
round(qt(.975, df = 8) * 1 / 3, 2)
```

```
## [1] 0.77
```

##
An independent group Student's T interval is used instead of a paired T interval when:  

* The observations are paired between the groups.
* The observations between the groups are naturally assumed to be statistically independent
* As long as you do it correctly, either is fine.
* More details are needed to answer this question


```r
2
```

```
## [1] 2
```

##

Consider the mtcars dataset. Construct a 95% T interval for MPG comparing 4 to 6 cylinder cars (subtracting in the order of 4 - 6) assume a constant variance.
What is the lower endpoint of the interval to 1 decimal place?

What is the upper endpoint of the interval to 1 decimal place?


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
mtcars %>% filter(cyl==4) -> four.cyl
mtcars %>% filter(cyl==6) -> six.cyl
round(t.test(four.cyl$mpg, six.cyl$mpg, paired = FALSE, var.equal = TRUE)$conf.int,1)
```

```
## [1]  3.2 10.7
## attr(,"conf.level")
## [1] 0.95
```

##

If someone put a gun to your head and said "Your confidence interval must contain what it's estimating or I'll pull the trigger", what would be the smart thing to do?

* Make your interval as wide as possible
* Make your interval as small as possible
* Call the authorities


```r
1
```

```
## [1] 1
```

##

Refer back to comparing MPG for 4 versus 6 cylinders. What do you conclude?

* The interval is above zero, suggesting 6 is better than 4 in the terms of MPG
* The interval is above zero, suggesting 4 is better than 6 in the terms of MPG
* The interval does not tell you anything about the hypothesis test; you have to do the test.
* The interval contains 0 suggesting no difference.


```r
2
```

```
## [1] 2
```

##

Suppose that 18 obese subjects were randomized, 9 each, to a new diet pill and a placebo. Subjects' body mass indices (BMIs) were measured at a baseline and again after having received the treatment or placebo for four weeks. The average difference from follow-up to the baseline (followup - baseline) was 3 kg/m2 for the treated group and 1 kg/m2 for the placebo group. The corresponding standard deviations of the differences was 1.5 kg/m2 for the treatment group and 1.8 kg/m2 for the placebo group. The study aims to answer whether the change in BMI over the four week period appear to differ between the treated and placebo groups.
What is the pooled variance estimate? (to 2 decimal places)


```r
n1 <- n2 <- 9
x1 <- -3  ##treated
x2 <- 1  ##placebo
s1 <- 1.5  ##treated
s2 <- 1.8  ##placebo
spsq <- ( (n1 - 1) * s1^2 + (n2 - 1) * s2^2) / (n1 + n2 - 2)
spsq
```

```
## [1] 2.745
```

##

For Binomial data the maximum likelihood estimate for the probability of a success is

* The proportion of successes
* The proportion of failures
* A shrunken version of the proportion of successes
* A shrunken version of the proportion of failures


```r
1
```

```
## [1] 1
```

##

Bayesian inference requires

* A type I error rate
* Setting your confidence level
* Assigning a prior probability distribution
* Evaluating frequency error rates


```r
3
```

```
## [1] 3
```
