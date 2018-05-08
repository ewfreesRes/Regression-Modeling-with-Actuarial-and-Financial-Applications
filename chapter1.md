---
title: Chapter 1. Regression and the Normal Distribution
description: >-
  Regression analysis is a statistical method that is widely used in many fields of study, with actuarial science being no exception. This chapter provides an introduction to the role of the normal distribution in regression, the use of logarithmic transformations in specifying regression relationships and the sampling basis that is critical for inferring regression results to broad populations of interest.


---
## Fitting a normal distribution

```yaml
type: VideoExercise

xp: 50

key: cc4b0289d5
```

`@projector_key`
02abc0a8a3727420f7c6f719ae15a203

---
## Fitting child's height distribution

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 6154f289da
```

The Galton data has already been read into a dataset called `heights`. These data include the heights of 928 adult children `child_ht`, together with an index of their parents' height `parent_ht`.  The video explored the distribution of the parents' height; in this assignment, we investigate the distribution of the heights of the adult children.

`@instructions`
-  Define the height of an adult child as a local variable
-  Use the function [mean()](https://www.rdocumentation.org/packages/base/versions/3.5.0/topics/mean/) to calculate the mean and the function [sd()](https://www.rdocumentation.org/packages/base/versions/3.5.0/topics/sd/) to calculate the standard deviation 
-  Use the normal approximation and the function [pnorm()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/Normal/)  determine the probability that a child's height is less than 72 inches

`@hint`
Remember that we can reference a variable, say `var`, from a data set such as `injury`, as `injury$var`.

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
mchild
sdchild <- ___
sdchild

#Determine the probability that a child's height is less than 72 inches
___(72, mean=mchild, sd=sdchild)
```
`@solution`
```{r}
ht_child <- heights$child_ht
mchild <- mean(ht_child)
sdchild <- sd(ht_child)
pnorm(72,mean=mchild, sd=sdchild)
```
`@sct`
```{r}
test_error()
test_object("ht_child", incorrect_msg = "The child's height variable was defined in the wrong way. (You might check the hint.)")
success_msg("Excellent! With this procedure, you can now calculate probabilities for any distribution using a normal curve approximation.")
```





---
## Visualizing child's height distribution

```yaml
type: NormalExercise

xp: 100

key: 7dc98dc1ff
```

As in the prior exercise, from the Galton dataset `heights`, the heights of 928 adult children have been used to create a local variable called `ht_child`. We also have basic summary statistics, the mean height `mchild` and the standard deviation of heights in `sdchild`. In this exercise, we explore the fit of the normal curve to this distribution.

`@instructions`
-  To visualize the distribution, use the function [hist()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist/) to calculate the histogram. Use the `freq = FALSE` option to give a histogram with proportions instead of counts.
-  Determine a sequence. Then, function [lines()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/lines/) to superimpose a normal curve on the histogram
-  Determine the probability that a son's height is greater than 72 inches


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
## Visualizing distributions

```yaml
type: VideoExercise

xp: 50

key: a6c75bd534
```

`@projector_key`
eb65055761c45534183ae2de06b6d265

---
## Visualizing bodily injury claims with density plots

```yaml
type: NormalExercise

xp: 100

key: 2b2ea998af
```

In the prior video, you got somebackground information on the Massachusetts bodily injury dataset. This dataset, `injury`, has been read in and local variables `claims` has been created. This assignment reviews the  [hist()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist/) function for visualizing the distribution and allows you to explore density plotting, a smoothed version of the histogram.

`@instructions`
-  Use the function [log()](https://www.rdocumentation.org/packages/base/versions/3.5.0/topics/log/) to create the logarithmic version of the claims variable
-  Calculate a histogram of logarithmic with 40 bins using an option in the [hist()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist/) function,  `breaks = `.
-  Create a density plot of logarithmic claims using the functions [plot()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/plot/) and [density()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/density/).
-  Repeat the density plot, this time using a more refined bandwidth equal to 0.03. Use an option in the  [density()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/density/) function, `bw = `.


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
## Summarizing distributions

```yaml
type: VideoExercise

xp: 50

key: 210f239af2
```

`@projector_key`
548a52c0975ffc2c8719c26dc5a1d00a

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
-  Determine the 25th empirical percentile for claims using the  [quantile()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/quantile/) function.
-  Determine the 25th percentile for claims based on a normal distribution using the  [qnorm()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/Normal/) function.
-  Produce a qq plot for claims. The [qqline()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/qqnorm/) function is handy for producing a reference line.


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






---
## Transformations

```yaml
type: VideoExercise

xp: 50

key: 6efae24831
```

`@projector_key`
470199e6243748dfac8891486e37b372

---
## Distribution of transformed bodily injury claims

```yaml
type: NormalExercise

xp: 100

key: 2127303de1
```

We have now examined the distributions of bodily injury claims and its logarithmic version. Grudgingly, we have concluded that to fit a normal curve the logarithmic version of claims is a better choice (again, we really do not like log dollars but you'll get used to it in this course). But, why logarithmic and not some other transformations?

A partial response to this question will appear in later chapters when we describe interpretation of regression coefficients. Another partial response is that the log transform seems to work well with skewed insurance data sets, as we demonstrate visually in this exercise.

`@instructions`
Use the code `par(mfrow = c(2, 2))` so that four graphs appear in a 2 by 2 matrix format for easy comparisons. Plot the density of

-  claims
-  square root of claims
-  logarithmic claims
-  negative reciprocal of claims


`@pre_exercise_code`
```{r}
injury <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/8cca19d0503fcf6e9d30d9cb912de5ba95ecb9c1/MassBI.csv", header = TRUE)
claims <- injury$claims
```
`@sample_code`
```{r}
#This code helps to organize the four graphs into a 2 by 2 format
par(mfrow = c(2, 2))
#Plot the density of claims
plot(density(___))
#Plot the density of square root of claims
plot(density(___)) 
#Plot the density of logarithmic claims
plot(density(___))
#Plot the density of the negative reciprocal of claims
plot(density(___))
```
`@solution`
```{r}
par(mfrow = c(2, 2))
plot(density(claims))    
plot(density(claims^(0.5)))  
plot(density(log(claims)))  
plot(density(-claims^(-1)))
```




