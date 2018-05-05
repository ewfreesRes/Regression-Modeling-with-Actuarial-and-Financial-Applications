---
title: Chapter 1. Regression and the Normal Distribution
description: >-
  Regression analysis is a statistical method that is widely used in many fields of study, with actuarial science being no exception. This chapter provides an introduction to the role of the normal distribution in regression, the use of logarithmic transformations in specifying regression relationships and the sampling basis that is critical for inferring regression results to broad populations of interest.


---
## Fitting Parents' Height Distribution

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 6154f289da
```

The video has explained simple analysis using parents' heights. Now replicate using the heights of sons.


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
summary(heights)
```
`@solution`
```{r}
ht_child <- heights$child_ht
(Mchild <- mean(ht_child))
(sdchild <- sd(ht_child))
x <- seq(60, 80,by=0.1)
hist(ht_child, freq=FALSE)
lines(x, dnorm(x,mean=Mchild, sd=sdchild), col="blue")
pnorm(72,mean=Mchild , sd=sdchild)
```
`@sct`
```{r}
str(heights1)
```





---
## Galton Data

```yaml
type: TabExercise
lang: r
xp: 100

key: ece8f5d002
```





`@pre_exercise_code`
```{r}
heights <- read.csv("https://assets.datacamp.com/production/course_7546/datasets/GaltonFamily.csv",header=TRUE)
```
`@sample_code`
```{r}
str(heights)
```






***



```yaml
type: NormalExercise

xp: 35

key: d649521c6d
```



`@instructions`
The data has already been read into a dataset called `heights`. Examine the structure of the data and use the `head` command to looks at the first few records.

`@hint`




`@solution`
```{undefined}
str(heights)
head(heights)
```
`@sct`
```{undefined}
str(heights)
head(heights)
```






***



```yaml
type: NormalExercise

xp: 35

key: 7a9447abd4
```



`@instructions`
Next, examine the distribution of the child's height and then examine the distribution of the parents height.

`@hint`




`@solution`
```{undefined}
plot(density(heights$PARENTC, bw=.6))
plot(density(heights$CHILDC) )
```
`@sct`
```{undefined}
plot(density(heights$PARENTC, bw=.6))
plot(density(heights$CHILDC) )
```






***



```yaml
type: NormalExercise

xp: 30

key: 575a39d478
```



`@instructions`
Finally, plot the data, using the jitter option to see a bit more of the relationship.

`@hint`




`@solution`
```{undefined}
plot(jitter(heights$PARENTC),jitter(heights$CHILDC), ylim=c(60,80), xlim=c(60,80))
abline(lm(heights$CHILDC~ heights$PARENTC))
summary(lm(heights$CHILDC~ heights$PARENTC))
```
`@sct`
```{undefined}
plot(jitter(heights$PARENTC),jitter(heights$CHILDC), ylim=c(60,80), xlim=c(60,80))
abline(lm(heights$CHILDC~ heights$PARENTC))
summary(lm(heights$CHILDC~ heights$PARENTC))
```






---
## <<<New Exercise>>>

```yaml
type: VideoExercise
lang: r
xp: 50
skills: 1
key: 82997984a4
```

`@projector_key`
undefined

---
## Fitting a Normal Distribution

```yaml
type: VideoExercise

xp: 50

key: cc4b0289d5
```

`@projector_key`
02abc0a8a3727420f7c6f719ae15a203