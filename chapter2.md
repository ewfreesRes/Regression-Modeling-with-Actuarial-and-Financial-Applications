---
title: Chapter 2. Basic Linear Regression
description: >-
  Insert the chapter description here


---
## Method of Least Squares

```yaml
type: VideoExercise
lang: r
xp: 50
skills: 1
key: e36068d39a
```

`@projector_key`
undefined

---
## Correlation

```yaml
type: VideoExercise

xp: 50

key: 5e5beff472
```

`@projector_key`
98aeb5a5bd795a7c8716aba8e177decb

---
## Linear transformations of Wisconsin lottery data

```yaml
type: NormalExercise

xp: 100

key: a485262f71
```

The Wisconsin lottery dataset has already been read into a dataset `Wisc_lottery`.

Like insurance claims, lotteries are uncertain events and so you want to be able to work and interpret with lottery data readily. Much of the reports that you read have sales and population in thousands of units, so this exercise gives you practice in rescaling data via linear transformations.

`@instructions`
- From the available population and sales variables, create new variables, say, `pop_1000` and `sales_1000` that are in thousands (of people and of dollars, respectively).
- Create summary statistics for the new variables.
- Plot `pop_1000` versus `sales_1000`.
- Calculation the correlation between `pop_1000` versus `sales_1000`. How does this differ between the correlation between population and sales in the original units?

`@hint`


`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
#library(Rcmdr)
```

`@solution`
```{r}
Lot$pop_1000 <- Lot$pop/1000
Lot$sales_1000 <- Lot$sales/1000
#numSummary(Lot[,c("pop_1000", "sales_1000")], statistics = c("mean", "sd", "quantiles"), quantiles = c(0,.5,1))
plot(Lot$pop_1000, Lot$sales_1000)
cor(Lot$pop_1000, Lot$sales_1000)
```




