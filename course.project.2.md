# ToothGrowth Data Exploratory Analysis
Alexander Tuzhikov  
September 14, 2015  
#Synopsis

We are now moving to the part 2 of the task. Below we will exlore the `ToothGrowth` dataset from R `datasets` package. The headers below will correspond to the tasks. The data comes from the study  [The Effect of Vitamin C on Tooth Growth in Guinea Pigs"][1]

#Load the ToothGrowth data and perform some basic exploratory data analyses


```r
library(datasets)
library(gridExtra)
library(ggplot2)
library(dplyr)
data("ToothGrowth")
```

#Provide a basic summary of the data
Well, the data is presented as a data.frame of 60 samples in 3 rows: len, supp, dose



#References

[1]:http://jn.nutrition.org/content/33/5/491.full.pdf "C. I. Bliss (1952) The Statistics of Bioassay. Academic Press." 
