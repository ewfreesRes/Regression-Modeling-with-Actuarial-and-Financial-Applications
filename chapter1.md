---
title: Chapter 1. Regression and the Normal Distribution
description: >-
  Regression analysis is a statistical method that is widely used in many fields of study, with actuarial science being no exception. This chapter provides an introduction to the role of the normal distribution in regression, the use of logarithmic transformations in specifying regression relationships and the sampling basis that is critical for inferring regression results to broad populations of interest.


---
## Fitting a Normal Distribution

```yaml
type: VideoExercise

xp: 50

key: cc4b0289d5
```

`@projector_key`
02abc0a8a3727420f7c6f719ae15a203

---
## Fitting Child's Height Distribution

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 6154f289da
```

The Galton data has already been read into a dataset called `heights`. These data include the heights of 928 adult children (child\_ht), together with an index of their parents' height (parent\_ht).  The video explored the distribution of the parents' height; in this assignment, we investigate the distribution of the heights of the adult children.

`@instructions`
-  Define the variable
-  Use the `R` function `mean` to calculate the mean and the function `sd` to calculate the standard deviation 
-  Use the normal approximation and the `R` function `pnorm` determine the probability that a child's height is less than 72 inches

`@hint`


`@pre_exercise_code`
```{r}
heights <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/c85ede6c205d22049e766bd08956b225c576255b/galton_height.csv", header = TRUE)
```
`@sample_code`
```{r}
#Define the variable
ht_child <- ___

#Calculate the mean and standard deviation
mchild <- ___
sdchild <- ___
mchild
sdchild

#Determine the probability that a child's height is less than 72 inches
___(72, mean=mchild, sd=sdchild)
```
`@solution`
```{r}
ht_child <- heights$child_ht
(mchild <- mean(ht_child))
(sdchild <- sd(ht_child))
pnorm(72,mean=mchild, sd=sdchild)
```
`@sct`
```{r}
str(heights)
```





---
## Visualizing Child's Height Distribution

```yaml
type: NormalExercise

xp: 100

key: 7dc98dc1ff
```

As in the prior exercise, from the Galton dataset `heights`, the heights of 928 adult children have been used to create a local variable called `ht_child`. We also have basic summary statistics, the mean height `mchild` and the standard deviation of heights in `sdchild`. In this exercise, we explore the fit of the normal curve to this distribution.

`@instructions`
-  To visualize the distribution, use the `R` function `hist` to calculate the histogram. Use the `freq = FALSE` option to give a histogram with proportions instead of counts.
-  Determine a sequence. Then,  `R` function `lines` to superimpose a normal curve on the histogram
-  Determine the probability that a son's height is greater than 72 inches

`@hint`


`@pre_exercise_code`
```{r}
heights <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/c85ede6c205d22049e766bd08956b225c576255b/galton_height.csv", header = TRUE)
ht_child <- heights$child_ht
mchild <- mean(ht_child)
sdchild <- sd(ht_child)
```
`@sample_code`
```{r}
#Visualize the Distribution
___(___, freq = FALSE)

#Determine a sequence. Then, graph a histogram with a normal curve superimposed
x <- seq(60, 80,by = 0.1)
___(x, dnorm(x,mean = mchild, sd = sdchild), col = "blue")

# Determine the probability that a son's height is greater than 60 inches
1 - pnorm__
```
`@solution`
```{r}
hist(ht_child, freq = FALSE)
x <- seq(60, 80,by = 0.1)
lines(x, dnorm(x,mean = mchild, sd = sdchild), col = "blue")
1 - pnorm(72, mean = mchild , sd = sdchild)
```






---
## Visualizing bodily injury claims with density plots

```yaml
type: NormalExercise

xp: 100

key: 2b2ea998af
```

In the prior video, you got some background information on the Massachusetts bodily injury dataset. This dataset, `injury`, has been read in and local variables `claims` has been created. This assignment reviews the `R` function `hist` for visualizing the distribution and allows you to explore density plotting, a smoothed version of the histogram.

`@instructions`
-  Use the `R` function `log` to create the logarithmic version of the claims variable
-  Calculate a histogram of logarithmic with 40 bins using the `R` option `breaks = `.
-  Create a density plot of logarithmic claims using the `R` functions `plot` and `density`.
-  Repeat the density plot, this time using a more refined bandwidth equal to 0.03. Use the `R` option `bw = `.

`@hint`


`@pre_exercise_code`
```{r}
injury <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/8cca19d0503fcf6e9d30d9cb912de5ba95ecb9c1/MassBI.csv", header = TRUE)
claims <- injury$claims
```
`@sample_code`
```{r}
#Create the logarithmic claims variable
logclaims <- ___

#Create a histogram usins 40 bins
___(logclaims, breaks = 40,freq = FALSE)
box()

# Create a density plot of logarithmic claims
plot(___(logclaims))

# Create a density plot of logarithmic claims with a smaller bandwidth
___
```
`@solution`
```{r}
logclaims <- log(claims)
hist(logclaims , breaks = 40,freq = FALSE)
box()
plot(density(logclaims))
plot(density(logclaims, bw = 0.03))
```






---
## Summarizing bodily injury claims with box and qq plots

```yaml
type: NormalExercise

xp: 100

key: 70a5a3a60b
```

The Massachusetts bodily injury data has already been read and used to create the local variable `claims` representing bodily injury claims. The previous video showed how to present the distribution of logarithmic claims which appeared to be approximately normally distributed. However, users are not really interested in log dollars but want to know about a unit of measurement that is more intuitive, such as dollars. 

So this assignment is based on claims, not the logarithmic version. You will review the functions  [boxplot()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/boxplot/) and [qqnorm()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/qqnorm/) for visualizing the distribution through boxplots and quantile-quantile, or qq-, plots. But, because we are working with such a skewed distribution, do not be surprised that it is difficult to interpret results readily.

`@instructions`
-  Produce a box plot for claims
-  Determine the 25th empirical percentile for claims using the `R` function `quantile`.
-  Determine the 25th percentile for claims based on a normal distribution using the function [qqnorm()].
-  Produce a qq plot for claims

`@hint`


`@pre_exercise_code`
```{r}
injury <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/8cca19d0503fcf6e9d30d9cb912de5ba95ecb9c1/MassBI.csv", header = TRUE)
claims <- injury$claims
```
`@sample_code`
```{r}
#Produce a box plot for claims
___(claims)

#Determine the 25th empirical percentile for claims
___(claims, probs = ___)

#Determine the 25th percentile for claims based on a normal distribution
___(p = ___, mean = mean(claims), sd = sd(claims))

#Produce a qq plot for claims
___(claims)
___(claims) 
```
`@solution`
```{r}
boxplot(claims)
quantile(claims, probs = 0.25)
qnorm(p = 0.25, mean = mean(claims), sd = sd(claims))
qqnorm(claims)
qqline(claims) 
```




