---
title: Chapter 1. Regression and the Normal Distribution
description: Regression analysis is a statistical method that is widely used in many fields of study, with actuarial science being no exception. This chapter provides an introduction to the role of the normal distribution in regression, the use of logarithmic transformations in specifying regression relationships and the sampling basis that is critical for inferring regression results to broad populations of interest.


---
## Fitting Parents' Height Distribution

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 6154f289da
```

The video has explained simple analysis using parents' heights. Now replicate using the heights of sons. Recall that the data are in the file `heights`.


`@instructions`

-  Define the variable
-  Calculate the mean and standard deviation
-  Calculate the histogram
-  Determine a sequence. Then, graph a histogram with a normal curve superimposed
-  Determine the probability that a son's height is less than 72 inches


`@pre_exercise_code`
```{r}
heights <- read.csv("https://assets.datacamp.com/production/course_7546/datasets/galton_height.csv",header=TRUE)
```
`@sample_code`
```{r}
#Define the variable
ht_child <- ___
#Calculate the mean and standard deviation
Mchild <- ___
sdchild <- ___
#Calculate the histogram
___(ht_child, freq=FALSE)
#Determine a sequence. Then, graph a histogram with a normal curve superimposed
x <- seq(60, 80,by=0.1)
#Determine the probability that a son's height is less than 72 inches
___(72, mean=Mchild , sd=sdchild)


```
`@solution`
```{r}
ht_child <- heights$child_ht
(Mchild <- mean(ht_child))
(sdchild <- sd(ht_child))
x <- seq(60, 80,by=0.1)
hist(ht_child, freq=FALSE)
lines(x, dnorm(x, mean=Mchild, sd=sdchild), col="blue")
pnorm(72, mean=Mchild , sd=sdchild)
```
`@sct`
```{r}
str(heights)
```



---
## Fitting a Normal Distribution

```yaml
type: VideoExercise

xp: 50

key: cc4b0289d5
```

`@projector_key`
02abc0a8a3727420f7c6f719ae15a203