---
title: Chapter 1. Regression and the Normal Distribution
description: >-
  Regression analysis is a statistical method that is widely used in many fields of study, with actuarial science being no exception. This chapter provides an introduction to the role of the normal distribution in regression, the use of logarithmic transformations in specifying regression relationships and the sampling basis that is critical for inferring regression results to broad populations of interest.


---
## Ex 1.1

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 6154f289da
```

Do some data science. Okay

`@instructions`
Frees testy

`@hint`


`@pre_exercise_code`
```{r}
heights1 <- read.csv("https://assets.datacamp.com/production/course_7546/datasets/GaltonFamily.csv",header=TRUE)
```
`@sample_code`
```{r}
str(heights1)
```
`@solution`
```{r}
str(heights1)
```
`@sct`
```{r}
str(heights1)
```






---
## Galton Data

```yaml
type: TabExercise
key: ece8f5d002
lang: r
xp: 100
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

### Sub Heading

```yaml
type: NormalExercise
xp: 100
key: d649521c6d
```

`@instructions`

The data has already been read into a dataset called `heights`. Examine the structure of the data and use the `head` command to looks at the first few records.

`@solution`
```{r}
str(heights)
head(heights)
```

`@hint`

`@sct`
```{r}
str(heights)
head(heights)
```

***

### Sub Heading 2

```yaml
type: NormalExercise
xp: 100
key: 7a9447abd4
```

`@instructions`

Next, examine the distribution of the child's height and then examine the distribution of the parents height.

`@solution`
```{r}
plot(density(heights$PARENTC, bw=.6))
plot(density(heights$CHILDC) )

```

`@hint`

`@sct`
```{r}
plot(density(heights$PARENTC, bw=.6))
plot(density(heights$CHILDC) )

```

***

### Sub Heading 3

```yaml
type: NormalExercise
xp: 100
key: 575a39d478
```

`@instructions`

Finally, plot the data, using the jitter option to see a bit more of the relationship.

`@solution`
```{r}
plot(jitter(heights$PARENTC),jitter(heights$CHILDC), ylim=c(60,80), xlim=c(60,80))
abline(lm(heights$CHILDC~ heights$PARENTC))
summary(lm(heights$CHILDC~ heights$PARENTC))

```

`@hint`

`@sct`
```{r}
plot(jitter(heights$PARENTC),jitter(heights$CHILDC), ylim=c(60,80), xlim=c(60,80))
abline(lm(heights$CHILDC~ heights$PARENTC))
summary(lm(heights$CHILDC~ heights$PARENTC))

```

---
## <<<New Exercise>>>

```yaml
type: VideoExercise
key: 82997984a4
lang: r
xp: 50
skills: 1
video_link: player.vimeo.com/video/154783078
```



































































