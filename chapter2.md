---
title: Chapter 2. Basic Linear Regression
description: >-
  This chapter considers regression in the case of only one explanatory variable. Despite this seeming simplicity, most of the deep ideas of regression can be developed in this framework. By limiting ourselves to the one variable case, we can illustrate the relationships between two variables graphically. Graphical tools prove to be important for developing a link between the data and a model.


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
## Correlations and the Wisconsin lottery

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


`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
#library(Rcmdr)
#library(psych)
```
`@sample_code`
```{r}
Lot$pop_1000 <- ___/1000
Lot$sales_1000 <- ___
```
`@solution`
```{r}
Lot$pop_1000 <- Lot$pop/1000
Lot$sales_1000 <- Lot$sales/1000
#numSummary(Lot[,c("pop_1000", "sales_1000")], statistics = c("mean", "sd", "quantiles"), quantiles = c(0,.5,1))
#(as.data.frame(psych::describe(Lot)))[,c(2,3,4,5,8,9)]
plot(Lot$pop_1000, Lot$sales_1000)
cor(Lot$pop_1000, Lot$sales_1000)
```






---
## Method of least squares

```yaml
type: VideoExercise

xp: 50

key: 5209238d14
```

`@projector_key`
6e4030abdd8e964f0911ab70682762cd

---
## Least squares fit using housing prices

```yaml
type: NormalExercise

xp: 100

key: 97ec81af2a
```

Instead of population, suppose that you wish to understand the effect that housing prices have on the sale of lottery tickets. In the Wisconsin lottery dataset  `Wisc_lottery` is the variable `medhome` which is the median house price for each zip code, in thousands of dollars. In this exercise, we will give feel for the distribution of this variable by examining summary statistics, examine its relationship with sales graphically and via correlations, fit a basic linear regression model and use this model to predict sales.

`@instructions`
- Create a table summarizing the distributions of `medhome` and `sales`.
- Plot `medhome` versus `sales` and calculate the corresponding correlation coefficient.
- Regress `medhome`, the explanatory variable, on `sales`, the dependent variable.
- Use the fitted regression model to predict sales assuming that the median house price for a zip code is 50 (in thousands of dollars).


`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
```
`@sample_code`
```{r}
#(as.data.frame(psych::describe(Lot[,c("medhome", "sales")])))[,c(2,3,4,5,8,9)]
cor(Lot$medhome,Lot$sales)
plot(Lot$medhome,Lot$sales)
model_blr1 <- lm(sales ~ medhome, data = Lot)
round(coefficients(model_blr1), digits=4)
newdata <- data.frame(medhome = 50)
predict(model_blr1, newdata)
```
`@solution`
```{r}
#(as.data.frame(psych::describe(Lot[,c("medhome", "sales")])))[,c(2,3,4,5,8,9)]
cor(Lot$medhome,Lot$sales)
plot(Lot$medhome,Lot$sales)
model_blr1 <- lm(sales ~ medhome, data = Lot)
round(coefficients(model_blr1), digits=4)
newdata <- data.frame(medhome = 50)
predict(model_blr1, newdata)
```






---
## Understanding Variability

```yaml
type: VideoExercise

xp: 50

key: ac4eb7cd57
```

`@projector_key`
72cd0d9806aa6b026cecc961b32c2a13

---
## Summarizing measures of uncertainty

```yaml
type: NormalExercise

xp: 100

key: e97a0cfbd0
```

Instead of population, in this exercise we will consider the variable `medhome` which is the median house price for each zip code, in thousands of dollars, available in the Wisconsin lottery dataset  `Wisc_lottery`. We will run a regression of `medhome` on `sales`. It will be helpful if you compare the results to the regression of `pop` on `sales`. We have seen that `pop` is more highly correlated with `sales` than `medhome`, so we are expecting greater uncertainty in this regression fit.

`@instructions`
- Run a regression of `medhome` on `sales`.
- Summarize the fitted regression model in an ANOVA table.
- Determine the size of the typical residual, $s$.
- Determine the coefficient of determination, $R^2$.


`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
```
`@sample_code`
```{r}
model_blr <- lm(sales  ~ medhome, data = Lot)
anova(model_blr)
sqrt(anova(model_blr)$Mean[2])
summary(model_blr)$r.squared
```
`@solution`
```{r}
model_blr <- lm(sales  ~ medhome, data = Lot)
anova(model_blr)
sqrt(anova(model_blr)$Mean[2])
summary(model_blr)$r.squared
```






---
## Effects of linear transforms on measures of uncertainty

```yaml
type: NormalExercise

xp: 100

key: 1f57405e27
```

Let us see how rescaling, a special kind of linear transformation, affects our measures of uncertainty. As before, the Wisconsin lottery dataset  `Wisc_lottery` is available and this dataset contains `sales_1000`, sales in thousands of dollars, and `pop_1000`, zip code population in thousands. How do measures of uncertainty change when going from the original units to thousands of those units?

`@instructions`
- Run a regression of `pop` on `sales_1000` and summarize this in an ANOVA table.
- For this regression, determine the $s$ and the coefficient of determiniation, $R^2$.  
- Run a regression of `pop_1000` on `sales_1000` and summarize this in an ANOVA table.
- For this regression, determine the $s$ and the coefficient of determination, $R^2$.


`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
Lot$pop_1000 <- Lot$pop/1000
Lot$sales_1000 <- Lot$sales/1000
```
`@sample_code`
```{r}
model_blr1 <- lm(sales_1000  ~ pop, data = Lot)
anova(model_blr1)
sqrt(anova(model_blr1)$Mean[2])
summary(model_blr1)$r.squared
model_blr2 <- lm(sales_1000  ~ pop_1000 , data = Lot)
anova(model_blr2)
sqrt(anova(model_blr2)$Mean[2])
summary(model_blr2)$r.squared
```
`@solution`
```{r}
model_blr1 <- lm(sales_1000  ~ pop, data = Lot)
anova(model_blr1)
sqrt(anova(model_blr1)$Mean[2])
summary(model_blr1)$r.squared
model_blr2 <- lm(sales_1000  ~ pop_1000 , data = Lot)
anova(model_blr2)
sqrt(anova(model_blr2)$Mean[2])
summary(model_blr2)$r.squared
```






---
## Statistical inference

```yaml
type: VideoExercise

xp: 50

key: 4e5ae2cad6
```

`@projector_key`
d2a8a48c0938cd9168aa1467e9d1cef0

---
## Statistical inference and Wisconsin lottery

```yaml
type: NormalExercise

xp: 100

key: 7f691f8ace
```

As an alternative to population, in this exercise we will summarize the effect that `medhome` has on `sales`. For interpretation, recall that `medhome` is in thousands of dollars whereas sales is in dollars. These variables are available in the dataset `Wisc_lottery` which has already been read in. This exercise will give you practice i the standard inferential tasks: hypothesis testing, confidence intervals, and prediction.

`@instructions`
- Summarize the regression model and identify the $t$-statistic for testing the importance of the regression coefficient associated with `medhome`.
- Provide a 95\% confidence interval for the regression coefficient associated with `medhome`.
- Consider a zip code with a median housing price equal to 50 (in thousands of dollars). Provide a point prediction and a 95\% prediction interval for sales.


`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
```
`@sample_code`
```{r}
model_blr1 <- lm(sales ~ medhome, data = Lot)
summary(model_blr1)
#Rcmdr::Confint(model_blr1, level = .95)
confint(model_blr1, level = .95)
NewData1 <- data.frame(medhome = 50)
predict(model_blr1, NewData1, interval = "prediction", level = .95)
```
`@solution`
```{r}
model_blr1 <- lm(sales ~ medhome, data = Lot)
summary(model_blr1)
#Rcmdr::Confint(model_blr1, level = .95)
confint(model_blr1, level = .95)
NewData1 <- data.frame(medhome = 50)
predict(model_blr1, NewData1, interval = "prediction", level = .95)
```






---
## Diagnostics

```yaml
type: VideoExercise

xp: 50

key: 62746a09aa
```

`@projector_key`
5a57a76dab158361957acfdc662c35ea