---
title: Chapter 3. Multiple Linear Regression
description: >-
  Insert the chapter description here


---
## Method of Least Squares

```yaml
type: VideoExercise

xp: 50

key: 607ecb673f
```

`@projector_key`
dd5d704d841ca6fae0df18c9b9e020c0

---
## Multiple linear regression and the term life purchases

```yaml
type: NormalExercise

xp: 100

key: 7e6008b3b9
```

Suppose that you wish to predict the amount of term life insurance that someone will purchase but are uneasy about the `education` variable. Your sense is that, for purposes of purchasing life insurance, high school graduates and those that attend college should be treated the same. So, in this exercise, your will create a new variable, say `education1` that is equal to years of education for those with education less than or equal to 12 and is equal to 12 otherwise. The *Survey of Consumer Finances* `education` variable is the number of completed years of schooling and so 12 corresponds to completing high school in the US.

The term life dataset, consisting of only those who purchased term life insurance, has already been read into a dataset `Term2`.

`@instructions`
- Use the `pmin` function to create the `education` variable as part of the `Term2` dataset.
- Check your work be examining summary statistics for the revised `Term2` dataset.
- Examine correlations for the revised dataset.
- Using the method of least squares, fit a multiple linear regresion model using `logface` as the dependent variables and using `education`, `numhh`, and `logincome` as explanatory variables.
- With this fitted model, provide a prediction of the face amount of insurance that someone with income of 40,000, 11 years of education, and 4 people in the household would purchase.

`@hint`


`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term2 <- Term1[, c("education", "face", "income", "logface", "logincome", "numhh")]
#library(Rcmdr)
```
`@sample_code`
```{r}
Term2$education1 <- pmin(12, Term2$education)
#summvar <- Rcmdr::numSummary(Term2, statistic = c("mean", "sd", "quantiles"), quantiles = c(0, .5, 1))
#summvar
summary(Term2)
round(cor(Term2), digits=3)
model_mlr1 <- lm(logface ~ education1 + numhh + logincome, data = Term2)
newdata <- data.frame(logincome = log(40000), education1 = 11, numhh = 4)
exp(predict(model_mlr1, newdata))
```
`@solution`
```{r}
Term2$education1 <- pmin(12, Term2$education)
#summvar <- Rcmdr::numSummary(Term2, statistic = c("mean", "sd", "quantiles"), quantiles = c(0, .5, 1))
#summvar
summary(Term2)
round(cor(Term2), digits=3)
model_mlr1 <- lm(logface ~ education1 + numhh + logincome, data = Term2)
newdata <- data.frame(logincome = log(40000), education1 = 11, numhh = 4)
exp(predict(model_mlr1, newdata))
```




