# Statistical Inference: The Study of the Exponential Distribution, A Simulation Exercise
Alexander Tuzhikov  
September 14, 2015  



#Overview: Exponential Distribution

In accordance with [Wikipedia](https://en.wikipedia.org/wiki/Exponential_distribution), **e**xponential **d**istribution (ED) *is the probability distribution that describes the time between events in a Poisson process, i.e. a process in which events occur continuously and independently at a constant average rate.* Both *mean* and *standard deviation* of the ED is *1/lambda*. As suggested in the study objective, here we will use lambda = 0.2. However, for the purpose of introduction, let's reconstruct the wiki plots of the ED with different lambda:


```r
lambdas<- c(0.2, 0.5, 1, 1.5)#the given in the task + those from wikipedia
n<- 40 #given by ".. you will investigate the distribution of 
       #averages of 40 exponential(0.2)s" in the task
sampling.count<- 1000  #given by ".. you will need to do a 
       #thousand or so simulated averages of 40 exponentials" in the task
set.seed(2015) #seed for reproducibility
ed.mean<- mean(rexp(1e6, 0.2))
ed.sd<- sd(rexp(1e6, 0.2))
all.equal(ed.mean, ed.sd, tolerance = 1e-2) #mean and standard deviation are equal up to 1e-2 level of prescision
```

```
## [1] TRUE
```

```r
#prepare a data.frame for the plot, melt by x, plot as line
ed.plot.df<- as.data.frame(cbind(
        x=0:40,
        la.0.2=dexp(x=0:40, lambdas[1]),
        la.0.5=dexp(x=0:40, lambdas[2]),
        la.1=dexp(x=0:40, lambdas[3]),
        la.1.5=dexp(x=0:40, lambdas[4])
)) %>% 
        melt(id.vars="x") %>%
        ggplot(data=., mapping=aes(x=x, group=variable, y=value, color=variable)) + 
        geom_line(size=2) + theme_bw() + xlim(0,20) + ylim(0,1) +
        labs(title="ED Probability Density Function") + ylab("Probability") +
        scale_color_manual(values=rainbow(4, start = 0.3, end = 0.9), labels=c("0.2","0.5", "1.0", "1.5"), name="Lambda")
plot(ed.plot.df)
```

![](course.project_files/figure-html/Overview 1-1.png) 

We just checked if the mean and the standard deviation are equal and plotted the probability density function at different levels of lambda.

#Simulations: Sampling the ED

Now, let's move to the first task:  
*1. Show the sample mean and compare it to the theoretical mean of the distribution.* First we gonna need 1000 samples of size 40 form ED.


```r
#sampling
samples<- as.data.frame(do.call(what = "cbind", args = lapply(1:sampling.count, function(x){return(rexp(n, lambdas[1]))})))
samples.colMeans<- colMeans(samples) #calculate the column means
```

#Sample Mean versus Theoretical Mean

Ok, now let's compare the theoretical mean, which is:


```r
ed.mean.theo<- 1/lambdas[1]
```

to that of the simulation procedure:


```r
ed.mean.sim<- mean(samples.colMeans) #calculate the total mean
print(c(theoretical.mean= ed.mean.theo, simulation.mean=ed.mean.sim))
```

```
## theoretical.mean  simulation.mean 
##         5.000000         5.016687
```

```r
#compare
all.equal(ed.mean.theo,ed.mean.sim)
```

```
## [1] "Mean relative difference: 0.003337434"
```

The difference is neglegible in our case.

#Sample Variance versus Theoretical Variance 

Now we will do the same in order to calculate the variance and see if it differs from the theoretical variance, as being asked in the second task:
*2. Show how variable it is and compare it to the theoretical variance of the distribution.*


```r
#simulated variance
ed.var.sim<- var(colMeans(samples))
#the theoretical variance is
ed.var.theo<- (1/lambdas[1]/sqrt(n))^2
print(c(thoretical.var=ed.var.theo, simulated.var=ed.var.sim))
```

```
## thoretical.var  simulated.var 
##       0.625000       0.605856
```

```r
#compare
all.equal(ed.var.theo,ed.var.sim)
```

```
## [1] "Mean relative difference: 0.03063041"
```
#Distribution: Sampling Means Are Distributed Approximately Normaly

Now we move to the third task: *3. Show that the distribution is approximately normal.* 


```r
#generate normally distributed data and combine both menas and the generated data in a data.frame
as.data.frame(cbind(n=1:sampling.count, sampling.means=samples.colMeans, 
                    normal.data=dnorm(seq(0.01, 10, 0.01), mean = ed.mean.theo, sd = sqrt(ed.var.theo)),
                    normal.prob=rnorm(1000, mean = ed.mean.theo, sd = sqrt(ed.var.theo)))) -> ed.plot.data
combined.theo.sim.plot<- ggplot() +  geom_histogram(data=ed.plot.data, mapping=aes(x=samples.colMeans, y=..density..,fill="lightsteelblue1"),color="skyblue3", stat="bin",binwidth=0.25)+
        geom_line(data=ed.plot.data, mapping=aes(x=seq(0.01, 10, 0.01),y= normal.data,color = "chocolate"), size=1.5) + 
        geom_vline(aes(xintercept=ed.mean.sim, color="green")) +
        geom_vline(aes(xintercept=ed.mean.theo, color="red")) +
        xlim(2.5, 7.5)+theme_bw() + labs(title="Sample Distribution vs Theoretical Distribution") + xlab("Means") + ylab("Density") +
        scale_fill_identity(name = "", guide = "legend",labels = c("Simulated Means")) +
        scale_colour_manual(name = "", values =c("chocolate"="chocolate","red"="red", "green"="green"), 
                            labels = c("Theoretical Distribution","Theoretical Mean", "Simulated Mean")) +
        theme(legend.position="bottom",legend.box = "horizontal")
qq.plot<- ggplot() + stat_qq(data=ed.plot.data, mapping=aes(sample=sampling.means,color="skyblue3")) +
        stat_qq(data=ed.plot.data, mapping=aes(sample=normal.prob,color="chocolate")) + theme_bw() +
        xlab("Theoretical") + ylab("Sample") + labs(title="Normal QQ-Plot") + 
        scale_color_manual(name="", values=c("skyblue3"="skyblue3","chocolate"="chocolate"), labels=c("Sampling Means","Normal Data"))+
        theme(legend.position="bottom")

library(gridExtra)
```

```
## Loading required package: grid
```

```r
grid.arrange(combined.theo.sim.plot, qq.plot, ncol=2,widths=c(2, 1))
```

```
## Warning: Removed 499 rows containing missing values (geom_path).
```

![](course.project_files/figure-html/distribution 1-1.png) 
The above two plots demonstrate that the simulated meand are very close to be distributed normally. Finally, let's see how *the distribution of a large collection of random exponentials and the distribution of a large collection of averages of 40 exponentials* differ. 


```r
ed.means.hist<- ggplot() + geom_histogram(data=ed.plot.data, mapping=aes(x=sampling.means, y=..density..), fill="lightsteelblue1", color="skyblue3", stat="bin", binwidth=0.25) +
        theme_bw() + xlab("Sampling Means") + ylab("Density") + labs(title="Sampling Means Density") +  xlim(2.5, 7.5)
ed.values.hist<- ggplot() +geom_histogram(data=melt(samples), mapping=aes(x=value, y=..density..), fill="palegreen", color="darkgreen", stat="bin", binwidth=0.25) +
        theme_bw() + xlab("ED Simulations") + ylab("Density") + labs(title="ED Density")+  xlim(0, 20)
```

```
## No id variables; using all as measure variables
```

```r
grid.arrange(ed.means.hist, ed.values.hist, ncol=2)
```

![](course.project_files/figure-html/distribution 2-1.png) 
The above plot shows how the sampling means becomes more and more "Normal distribution"-like shaped with the increase in the number of samples taken, while the density of ED becomes strongly non-normal.


