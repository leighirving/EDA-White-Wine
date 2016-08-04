---
title: "Exploratory Data Analysis of White Wine Quality"
author: "Leighann Irving"
date: "July 29, 2016"
output: html_document
---


```
## Error in setwd("/Users/lirving/Documents/R Prac/EDA_Course_Materials/Final Project"): cannot change working directory
```


###Overview of the data

```r
str(white_wine)
```

```
## 'data.frame':	4898 obs. of  12 variables:
##  $ fixed.acidity       : num  7 6.3 8.1 7.2 7.2 8.1 6.2 7 6.3 8.1 ...
##  $ volatile.acidity    : num  0.27 0.3 0.28 0.23 0.23 0.28 0.32 0.27 0.3 0.22 ...
##  $ citric.acid         : num  0.36 0.34 0.4 0.32 0.32 0.4 0.16 0.36 0.34 0.43 ...
##  $ residual.sugar      : num  20.7 1.6 6.9 8.5 8.5 6.9 7 20.7 1.6 1.5 ...
##  $ chlorides           : num  0.045 0.049 0.05 0.058 0.058 0.05 0.045 0.045 0.049 0.044 ...
##  $ free.sulfur.dioxide : num  45 14 30 47 47 30 30 45 14 28 ...
##  $ total.sulfur.dioxide: num  170 132 97 186 186 97 136 170 132 129 ...
##  $ density             : num  1.001 0.994 0.995 0.996 0.996 ...
##  $ pH                  : num  3 3.3 3.26 3.19 3.19 3.26 3.18 3 3.3 3.22 ...
##  $ sulphates           : num  0.45 0.49 0.44 0.4 0.4 0.44 0.47 0.45 0.49 0.45 ...
##  $ alcohol             : num  8.8 9.5 10.1 9.9 9.9 10.1 9.6 8.8 9.5 11 ...
##  $ quality             : int  6 6 6 6 6 6 6 6 6 6 ...
```

```r
summary(white_wine)
```

```
##  fixed.acidity    volatile.acidity  citric.acid     residual.sugar  
##  Min.   : 3.800   Min.   :0.0800   Min.   :0.0000   Min.   : 0.600  
##  1st Qu.: 6.300   1st Qu.:0.2100   1st Qu.:0.2700   1st Qu.: 1.700  
##  Median : 6.800   Median :0.2600   Median :0.3200   Median : 5.200  
##  Mean   : 6.855   Mean   :0.2782   Mean   :0.3342   Mean   : 6.391  
##  3rd Qu.: 7.300   3rd Qu.:0.3200   3rd Qu.:0.3900   3rd Qu.: 9.900  
##  Max.   :14.200   Max.   :1.1000   Max.   :1.6600   Max.   :65.800  
##    chlorides       free.sulfur.dioxide total.sulfur.dioxide
##  Min.   :0.00900   Min.   :  2.00      Min.   :  9.0       
##  1st Qu.:0.03600   1st Qu.: 23.00      1st Qu.:108.0       
##  Median :0.04300   Median : 34.00      Median :134.0       
##  Mean   :0.04577   Mean   : 35.31      Mean   :138.4       
##  3rd Qu.:0.05000   3rd Qu.: 46.00      3rd Qu.:167.0       
##  Max.   :0.34600   Max.   :289.00      Max.   :440.0       
##     density             pH          sulphates         alcohol     
##  Min.   :0.9871   Min.   :2.720   Min.   :0.2200   Min.   : 8.00  
##  1st Qu.:0.9917   1st Qu.:3.090   1st Qu.:0.4100   1st Qu.: 9.50  
##  Median :0.9937   Median :3.180   Median :0.4700   Median :10.40  
##  Mean   :0.9940   Mean   :3.188   Mean   :0.4898   Mean   :10.51  
##  3rd Qu.:0.9961   3rd Qu.:3.280   3rd Qu.:0.5500   3rd Qu.:11.40  
##  Max.   :1.0390   Max.   :3.820   Max.   :1.0800   Max.   :14.20  
##     quality     
##  Min.   :3.000  
##  1st Qu.:5.000  
##  Median :6.000  
##  Mean   :5.878  
##  3rd Qu.:6.000  
##  Max.   :9.000
```

<!-- Note: The variables `fixed.acidity`, `volatile.acidity`,`citric.acid`, `residual.sugar`, `chlorides`, and `sulphates` were recorded in g/ dm^3^ units but since $1g/ dm^{3} = 1 litre$ I will describe these variables in litres. -->

Given the data set I want to find which variables influence the wine experts' ranking of `quality`.

Since `quality` must be an integer value between 0 and 10 (i.e. discrete and categorical) it should should be changed to a factor.


```r
white_wine$quality <- factor(white_wine$quality, ordered = TRUE)
```

##Univariate Analysis

###Looking at distribution of quality

```r
qplot(quality, data = white_wine)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png)

The `quality` of the white wine is approximately normally distributed. 

Interestingly, no white wine was determined to be "very excellent" and given a perfect score of 10/10. Contrastingly, none was determined to be "very bad" and given a score of 0, as well as a score of 1 or 2.


```r
table(white_wine$quality)
```

```
## 
##    3    4    5    6    7    8    9 
##   20  163 1457 2198  880  175    5
```

About 45% of the wines were given a score of 6 and 93% were between 5 and 7 therefore most were considered "average" by the wine experts.

###Histogram of each variable

```r
fixed.acid.count <- qplot(fixed.acidity, data = white_wine)
vol.acid.count <- qplot(volatile.acidity, data = white_wine)
citric.acid.count <- qplot(citric.acid, data = white_wine)
res.sugar.count <- qplot(residual.sugar, data = white_wine)
chlorides.count <- qplot(chlorides, data = white_wine)
free.s02.count <- qplot(free.sulfur.dioxide, data = white_wine)
total.so2.count <- qplot(total.sulfur.dioxide, data = white_wine)
density.count <- qplot(density, data = white_wine)
pH.count <- qplot(pH, data = white_wine)
sulphates.count <- qplot(sulphates, data = white_wine)
alcohol.count <- qplot(alcohol, data = white_wine)

grid.arrange(fixed.acid.count, vol.acid.count, citric.acid.count, 
             res.sugar.count, chlorides.count, free.s02.count, total.so2.count,
             density.count, pH.count, sulphates.count, alcohol.count, ncol = 3)
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-1.png)



###Closer look at residual.sugar


```r
qplot(residual.sugar, data = white_wine, xlim = c(0,20), 
      color = I('black'), fill = I('purple'))
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7-1.png)

There is an extremely high peak between 1 and 2g / litre of `residual.sugar`.


```r
summary(white_wine$residual.sugar)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.600   1.700   5.200   6.391   9.900  65.800
```

Since 45 g/ litre is the standard of sweetness, the low median (5.2 g/ litre) means that majority of the white wines were very bitter. Maybe the `quality` of the wines would have been higher on average had there been a larger percentage of sweet wines. This warrants an investigation of the relationship between `residual.sugar` and `quality`.


###Closer look at percent alcohol content

```r
qplot(alcohol, data = white_wine, color = I('black'), fill = I('purple'))
```

![plot of chunk unnamed-chunk-9](figure/unnamed-chunk-9-1.png)

The distribution is skewed right with a peak between 9 and 10% alcohol.

It looks like there are about three peaks in this distribution.

####Close-up of the first peak

```r
qplot(alcohol, data = white_wine, color = I('black'), fill = I('purple'),
      xlim = c(8,10))
```

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10-1.png)

####Close-up of the second peak

```r
qplot(alcohol, data = white_wine, color = I('black'), fill = I('purple'),
      xlim = c(10,12))
```

![plot of chunk unnamed-chunk-11](figure/unnamed-chunk-11-1.png)

####Close-up of the third peak

```r
qplot(alcohol, data = white_wine, color = I('black'), fill = I('purple'),
      xlim = c(12,14))
```

![plot of chunk unnamed-chunk-12](figure/unnamed-chunk-12-1.png)


```r
qplot(alcohol, data = white_wine, color = I('black'), fill = I('purple'),
      binwidth = 0.05)
```

![plot of chunk unnamed-chunk-13](figure/unnamed-chunk-13-1.png)

From the close-ups and the more detailed histogram above it can be seen that there are evenly-spaced gaps (or `alcohol` levels with extremely low counts) among the distributions. Why would this happen?


```r
head(white_wine$alcohol,15)
```

```
##  [1]  8.8  9.5 10.1  9.9  9.9 10.1  9.6  8.8  9.5 11.0 12.0  9.7 10.8 12.4
## [15]  9.7
```

```r
tail(white_wine$alcohol,15)
```

```
##  [1] 11.50  9.60  9.55 12.15 13.00  9.20  9.40 11.80 10.60  9.70 11.20
## [12]  9.60  9.40 12.80 11.80
```

Looking at some of the raw values of `alcohol`, the pattern in the distributions may be explained by most of the values rounded to one decimal place while a few (the gaps) were rounded to two.

###Closer look at volatile acidity


```r
qplot(volatile.acidity, data = white_wine, color = I('black'), fill = I('purple'))
```

![plot of chunk unnamed-chunk-15](figure/unnamed-chunk-15-1.png)

Most of the white wines had a `volatile acidity` around 0.25 g/ litre. The distribution appears somewhat symmetric but with a long right-tail. Why is this? "Too high" levels are said to lead to an unpleasant, vinegar taste so presumably this long tail has a negative relationship with quality. I will investigate this `volatile acidity`-`quality` relationship later on.

###Closer look at citric acid quantities


```r
qplot(citric.acid, data = white_wine, color = I('black'), fill = I('purple'))
```

![plot of chunk unnamed-chunk-16](figure/unnamed-chunk-16-1.png)

Between 0 and about 0.75g /litre, the histogram appears to be normally distributed. However, there is a long right-tail. This may be accounted for by the fact that citric acid is said to add 'freshness' and flavor to wines and as such more wines would be made with a high citric acid content. I will investigate the relationship between `citric acid` and `quality` later on.

###Closer look at potassium sulphates


```r
qplot(sulphates, data = white_wine, color = I('black'), fill = I('purple'))
```

![plot of chunk unnamed-chunk-17](figure/unnamed-chunk-17-1.png)

Most sulphates are between 0.3 and 0.75 litres.


```r
qplot(sulphates, data = white_wine, color = I('black'), fill = I('purple'),
      binwidth = 0.01)
```

![plot of chunk unnamed-chunk-18](figure/unnamed-chunk-18-1.png)

The histogram is approximately normally distributed but with a long-right tail.

###Closer look at free sulfur dioxide


```r
qplot(free.sulfur.dioxide, data = white_wine, 
      color = I('black'), fill = I('purple'))
```

![plot of chunk unnamed-chunk-19](figure/unnamed-chunk-19-1.png)


```r
qplot(free.sulfur.dioxide, data = white_wine, 
      color = I('black'), fill = I('purple'),
      xlim = c(0,100), binwidth = 1 )
```

![plot of chunk unnamed-chunk-20](figure/unnamed-chunk-20-1.png)

It is said that at free sulfur dioxide (SO2) concentrations over 50g/ litre, SO2 becomes evident in the nose and taste of wine but there is no change in the pattern of the distribution around 50g / litre. 

However, there is a long right-tail so wine makers are making wine with disproportionately high free SO2 levels. Presumably this happens because the effect of high free SO2 concentrations is more pleasant to buyers. I shall test this by later examining the relationship between free SO2 levels and quality.


###Summary of Univariate Data:

There are 4,898 white wines in the dataset with 12 features(fixed.acidity, volatile.acidity, citric.acid, residual.sugar, chlorides, free.sulfur.dioxide, total.sulfur.dioxide, density, pH, sulphates, alcohol, quality).

The goal of this EDA is to ascertain which variables are good predictors of quality.

volatile.acidity, citric.acid, residual.sugar and free.sulfur.dioxide are the variables expected to be the best predictors.

##Bivariate Analysis

###Overview

```r
set.seed(1234)
ggpairs(white_wine[sample.int(nrow(white_wine), 1000), ])
```

![plot of chunk unnamed-chunk-21](figure/unnamed-chunk-21-1.png)

####Quality vs. Residual Sugar


```r
ggplot(aes(x = quality, y = residual.sugar), data = white_wine) + 
  geom_point(alpha = 1/4)
```

![plot of chunk unnamed-chunk-22](figure/unnamed-chunk-22-1.png)



```r
plot(x = white_wine$quality, y = white_wine$residual.sugar)
```

![plot of chunk unnamed-chunk-23](figure/unnamed-chunk-23-1.png)



```r
by(white_wine$residual.sugar, white_wine$quality, summary)
```

```
## white_wine$quality: 3
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.700   1.588   4.600   6.392  10.700  16.200 
## -------------------------------------------------------- 
## white_wine$quality: 4
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.700   1.300   2.500   4.628   7.100  17.550 
## -------------------------------------------------------- 
## white_wine$quality: 5
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.600   1.800   7.000   7.335  11.500  23.500 
## -------------------------------------------------------- 
## white_wine$quality: 6
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.700   1.700   5.300   6.442   9.900  65.800 
## -------------------------------------------------------- 
## white_wine$quality: 7
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.900   1.700   3.650   5.186   7.325  19.250 
## -------------------------------------------------------- 
## white_wine$quality: 8
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.800   2.100   4.300   5.671   8.200  14.800 
## -------------------------------------------------------- 
## white_wine$quality: 9
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    1.60    2.00    2.20    4.12    4.20   10.60
```


From the boxplot above it can be seen that the highest-rated white wines (`quality` ranking 9) had the smallest range and the lowest median of residual sugar however there seems to be no clear relationship between `quality` and `residual.sugar`.


####Quality vs. Citric Acid

```r
plot(x = white_wine$quality, y = white_wine$citric.acid)
```

![plot of chunk unnamed-chunk-25](figure/unnamed-chunk-25-1.png)

From the boxplot above it can be seen that the median `citric.acid` are quite close among the `quality` scores and that the highest-rated white wines (`quality` ranking 9) had the highest median `citric.acid`. However, there seems to be no clear relationship between `quality` and `citric.acid`.

####Quality vs. Fee Sulfur Dioxide

```r
plot(x = white_wine$quality, y = white_wine$free.sulfur.dioxide)
```

![plot of chunk unnamed-chunk-26](figure/unnamed-chunk-26-1.png)

```r
by(white_wine$free.sulfur.dioxide, white_wine$quality, summary)
```

```
## white_wine$quality: 3
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    5.00   13.25   33.50   53.32   47.50  289.00 
## -------------------------------------------------------- 
## white_wine$quality: 4
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    3.00    9.00   18.00   23.36   30.50  138.50 
## -------------------------------------------------------- 
## white_wine$quality: 5
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    2.00   22.00   35.00   36.43   50.00  131.00 
## -------------------------------------------------------- 
## white_wine$quality: 6
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    3.00   24.00   34.00   35.65   46.00  112.00 
## -------------------------------------------------------- 
## white_wine$quality: 7
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    5.00   25.00   33.00   34.13   41.00  108.00 
## -------------------------------------------------------- 
## white_wine$quality: 8
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    6.00   28.00   35.00   36.72   44.50  105.00 
## -------------------------------------------------------- 
## white_wine$quality: 9
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    24.0    27.0    28.0    33.4    31.0    57.0
```

From the boxplot above it can be seen that the median `free.sulfur.dioxide` are quite close among the `quality` scores and there seems to be no clear relationship between the variables.

####Quality vs. pH

```r
plot(x = white_wine$quality, y = white_wine$pH)
```

![plot of chunk unnamed-chunk-27](figure/unnamed-chunk-27-1.png)

From the boxplot above it can be seen that the highest-rated wines had the highest `pH` and from a quality ranking of 5 through 9 there is a corresponding increase in `pH` however it is hard to tell from just the plot whether the two variables are correlated therefore I shall conduct a correlation test.


```r
white_wine$quality <- as.numeric(white_wine$quality)
cor.test(white_wine$pH, white_wine$quality)
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  white_wine$pH and white_wine$quality
## t = 6.9917, df = 4896, p-value = 3.081e-12
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.07162022 0.12707983
## sample estimates:
##        cor 
## 0.09942725
```

With a correlation coefficient of 0.10, no linear relationship exists between `pH` and `quality`.




####Quality vs. Volatile Acidity

```r
plot(x = white_wine$quality, y = white_wine$volatile.acidity)
```

![plot of chunk unnamed-chunk-30](figure/unnamed-chunk-30-1.png)

```r
by(white_wine$volatile.acidity, white_wine$quality, summary)
```

```
## white_wine$quality: 1
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.1700  0.2375  0.2600  0.3332  0.4125  0.6400 
## -------------------------------------------------------- 
## white_wine$quality: 2
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.1100  0.2700  0.3200  0.3812  0.4600  1.1000 
## -------------------------------------------------------- 
## white_wine$quality: 3
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.100   0.240   0.280   0.302   0.340   0.905 
## -------------------------------------------------------- 
## white_wine$quality: 4
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.0800  0.2000  0.2500  0.2606  0.3000  0.9650 
## -------------------------------------------------------- 
## white_wine$quality: 5
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.0800  0.1900  0.2500  0.2628  0.3200  0.7600 
## -------------------------------------------------------- 
## white_wine$quality: 6
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.1200  0.2000  0.2600  0.2774  0.3300  0.6600 
## -------------------------------------------------------- 
## white_wine$quality: 7
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.240   0.260   0.270   0.298   0.360   0.360
```

There doesn't seem to be a strong correlation between `volatile acidity` and `quality`.  

####Quality vs. Chlorides

```r
plot(x = white_wine$quality, y = white_wine$chlorides)
```

![plot of chunk unnamed-chunk-31](figure/unnamed-chunk-31-1.png)

```r
by(white_wine$chlorides, white_wine$quality, summary)
```

```
## white_wine$quality: 1
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## 0.02200 0.03625 0.04100 0.05430 0.05400 0.24400 
## -------------------------------------------------------- 
## white_wine$quality: 2
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.0130  0.0380  0.0460  0.0501  0.0540  0.2900 
## -------------------------------------------------------- 
## white_wine$quality: 3
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## 0.00900 0.04000 0.04700 0.05155 0.05300 0.34600 
## -------------------------------------------------------- 
## white_wine$quality: 4
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## 0.01500 0.03600 0.04300 0.04522 0.04900 0.25500 
## -------------------------------------------------------- 
## white_wine$quality: 5
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## 0.01200 0.03100 0.03700 0.03819 0.04400 0.13500 
## -------------------------------------------------------- 
## white_wine$quality: 6
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## 0.01400 0.03000 0.03600 0.03831 0.04400 0.12100 
## -------------------------------------------------------- 
## white_wine$quality: 7
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.0180  0.0210  0.0310  0.0274  0.0320  0.0350
```

From the boxplot it can be seen that the median `chlorides` are quite close among the `quality` scores but it seems there could be a negative correlation between `chlorides` and `quality` with the highest ranked wines having the lowest amount of `chlorides` however to be sure I shall conduct a correlation test.


```r
white_wine$quality <- as.numeric(white_wine$quality)
cor.test(white_wine$chlorides, white_wine$quality)
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  white_wine$chlorides and white_wine$quality
## t = -15.024, df = 4896, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  -0.2365501 -0.1830039
## sample estimates:
##        cor 
## -0.2099344
```

With a correlation of -0.21, no linear relationship exists between `chlorides` and `quality`.




####Quality vs. Alcohol

```r
plot(x = white_wine$quality, y = white_wine$alcohol)
```

![plot of chunk unnamed-chunk-34](figure/unnamed-chunk-34-1.png)

From the boxplot, the highest-rated wines had the highest median `alcohol` percentage and  `quality` scores 1-3 are correlated with decreasing `alcohol` while 3-9 are correlated with increasing `alcohol` therefore I shall conduct a correlation test to determine if there is an overall correlation.


```r
white_wine$quality <- as.numeric(white_wine$quality)
cor.test(white_wine$alcohol, white_wine$quality)
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  white_wine$alcohol and white_wine$quality
## t = 33.858, df = 4896, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.4126015 0.4579941
## sample estimates:
##       cor 
## 0.4355747
```

With a correlation coefficient of 0.44 there is a weak positive relationship between `alcohol` and `quality`.


```r
ggplot(aes (x = quality, y = alcohol), data = white_wine) +
  geom_point() + geom_smooth(method = 'lm', color = 'purple')
```

![plot of chunk unnamed-chunk-36](figure/unnamed-chunk-36-1.png)




####Quality vs Density


```r
plot(x = white_wine$quality, y = white_wine$density)
```

![plot of chunk unnamed-chunk-38](figure/unnamed-chunk-38-1.png)

From the boxplot the highest-rated wines had the lowest median `density` and it seems there may be a negative relationship between `density` and `quality`. To be sure I shall conduct a correlation test. 


```r
white_wine$quality <- as.numeric(white_wine$quality)
cor.test(white_wine$quality, white_wine$density)
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  white_wine$quality and white_wine$density
## t = -22.581, df = 4896, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  -0.3322718 -0.2815385
## sample estimates:
##        cor 
## -0.3071233
```

With a correlation of -0.31 there is, in fact, a strong negative (linear) relationship between `density` and `quality`.

###Summary of Bivariate Data:

* No variable was strongly or moderately correlated with `quality`.
* There is a weak positive correlation between `alcohol` and `quality`.
* There is a weak negative correlation between `density` and `quality`.



###Multivariate Analysis

Since `alcohol` and `density` both affect `quality` let's plot `alcohol` against `density` distinguished by `quality` to see if there is a pattern.

####Alcohol vs Density by Quality

```r
ggplot(aes(x = alcohol, y = density), data = white_wine) +
  geom_point(aes(color = quality), stat = "summary", fun.y = median) 
```

![plot of chunk unnamed-chunk-41](figure/unnamed-chunk-41-1.png)

There is a strong negative relationship between `alcohol` and `density` however, the `quality` scores are scattered among the plot and there is no pattern.

##Reflection

* None of the variables that were expected to influence `quality` (`residual.sugar`, `citric.acid`, `volatile.acidity` and `free.sulfur.dioxide`) did.
* Only 2 variables correlated with `quality` (`alcohol` and `density`) and even those were weak correlations.
* This indicates that the wine experts may determine `quality` based on some unknown variable, for example price.

