---
title: Chapter 3. Multiple Linear Regression
description: >-
  This chapter introduces linear regression in the case of several explanatory variables, known as multiple linear regression. Many basic linear regression concepts extend directly, including goodness of fit measures such as the coefficient of determination and inference using t-statistics. Multiple linear regression models provide a framework for summarizing highly complex, multivariate data. Because this framework requires only linearity in the parameters, we are able to fit models that are nonlinear functions of the explanatory variables, thus providing a wide scope of potential applications.


---
## Method of least squares

```yaml
type: VideoExercise

xp: 50

key: 607ecb673f
```

`@projector_key`
dd5d704d841ca6fae0df18c9b9e020c0

---
## Least squares and term life data

```yaml
type: NormalExercise

xp: 100

key: 7e6008b3b9
```

Suppose that you wish to predict the amount of term life insurance that someone will purchase but are uneasy about the `education` variable. Your sense is that, for purposes of purchasing life insurance, high school graduates and those that attend college should be treated the same. So, in this exercise, your will create a new variable, say `education1` that is equal to years of education for those with education less than or equal to 12 and is equal to 12 otherwise. The *Survey of Consumer Finances* `education` variable is the number of completed years of schooling and so 12 corresponds to completing high school in the US.

The term life dataset, consisting of only those who purchased term life insurance, has already been read into a dataset `Term2`.

`@instructions`
- Use the [pmin()](https://www.rdocumentation.org/packages/mc2d/versions/0.1-17/topics/pmin) function to create the `education` variable as part of the `Term2` dataset.
- Check your work be examining summary statistics for the revised `Term2` dataset.
- Examine correlations for the revised dataset.
- Using the method of least squares, fit a multiple linear regresion model using `logface` as the dependent variables and using `education`, `numhh`, and `logincome` as explanatory variables.
- With this fitted model, provide a prediction of the face amount of insurance that someone with income of 40,000, 11 years of education, and 4 people in the household would purchase.


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






---
## Interpreting term life regression coefficients

```yaml
type: NormalExercise

xp: 100

key: 9d20cb1de4
```

In the previous exercise, you fit a multiple linear regresion model using `logface` as the dependent variables and using `education`, `numhh`, and `logincome` as explanatory variables. It turned out that the coefficient associated with `education` was 0.2064 and the coefficient associated with `logincome` was 0.4935. We now wish to interpret these regression coefficients.

The typical interpretation of coefficients in a regression model is as a partial slope. That is, for the coefficient $b\_{1}$ associated with $x\_{1}$, we interpret $b\_{1}$ to be amount that the expected outcome changes per unit change in $x\_{1}$, holding the other explanatory variables fixed. For the term life example, the units of the outcome are in logarithmic dollars. So, for small values of $b\_{1}$, we can interpret this to be a *proportional* change in dollars (this is the reason for using natural logarithms).

When both $x\_{1}$ and $y$ are in logarithmic units, then we can interpret $b\_{1}$ to be ratio of two percentage changes, known as an *elasticity* in economics.

`@instructions`
- Determine least square fitted values for several selected values of `education`, holding other explantory variables fixed. For this part of the demonstration, we used their mean values.
- Determine the proportional changes. Note the relation between these values from a discrete change approximation to the regression coefficient for `education` equal to 0.2064.
- For several selected values of `logincome`, determine the corresponding proportional changes.
- Determine least square fitted values for several selected values of `logincome`, holding other explanatory variables fixed and the corresponding proportional changes for the fitted values. 
- Calculate the ratio of proportional changes of fitted values to those for income. Note the relation between these values (from a discrete change approximation) to the regression coefficient for `logincome` equal to 0.4935.


`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term2 <- Term1[, c("education", "face", "income", "logface", "logincome", "numhh")]
model_mlr <- lm(logface ~ education + numhh + logincome, data = Term2)
#summary(model_mlr)$coefficients[,1]
```
`@sample_code`
```{r}
educ_predict <- c(14,14.1,14.2,14.3)
newdata1 <- data.frame(logincome=mean(Term2$logincome), education=educ_predict, numhh=mean(Term2$numhh))
lsfits1 <- predict(model_mlr, newdata1)
lsfits1
lsfits1[2:4] - lsfits1[1:3]
pchange_fits1 <- exp(lsfits1[2:4] - lsfits1[1:3])
pchange_fits1

logincome_pred <- c(11,11.1,11.2,11.3)
pchange_income <- 100*(exp(logincome_pred[2:4])/exp(logincome_pred[1:3])-1)
pchange_income
newdata2 <- data.frame(logincome=logincome_pred,education=mean(Term2$education), numhh=mean(Term2$numhh))
lsfits2 <- predict(model_mlr, newdata2)
pchange_fits2 <- 100*(exp(lsfits2[2:4])/exp(lsfits2[1:3])-1)
pchange_fits2
pchange_fits2/pchange_income
```
`@solution`
```{r}
educ_predict <- c(14,14.1,14.2,14.3)
newdata1 <- data.frame(logincome=mean(Term2$logincome), education=educ_predict, numhh=mean(Term2$numhh))
lsfits1 <- predict(model_mlr, newdata1)
lsfits1
lsfits1[2:4] - lsfits1[1:3]
pchange_fits1 <- exp(lsfits1[2:4] - lsfits1[1:3])
pchange_fits1

logincome_pred <- c(11,11.1,11.2,11.3)
pchange_income <- 100*(exp(logincome_pred[2:4])/exp(logincome_pred[1:3])-1)
pchange_income
newdata2 <- data.frame(logincome=logincome_pred,education=mean(Term2$education), numhh=mean(Term2$numhh))
lsfits2 <- predict(model_mlr, newdata2)
pchange_fits2 <- 100*(exp(lsfits2[2:4])/exp(lsfits2[1:3])-1)
pchange_fits2
pchange_fits2/pchange_income
```






---
## Statistical inference and multiple linear regression

```yaml
type: VideoExercise

xp: 50

key: cfa3072c7c
```

`@projector_key`
c77074330c0754662a1dbb56fbca3e43

---
## Statistical inference and term life

```yaml
type: NormalExercise

xp: 100

key: 81c84d6420
```

In later chapters, we will learn how to specify a model using diagnostics techniques; these techniques were used to specify face in log dollars for the outcome and similarly income in log dollars as an explanatory variable. Just to see how things work, in this exercise we will create new variables `face` and `income` that are in the original units and run a regression for with these. We have already seen that rescaling by constants do not affect relationships but can be helpful with interpretations, so we define both  `face` and `income` to be in thousands of dollars.

`@instructions`
- Create `Term2$face` by exponentiating `logface` and dividing by 1000. For convenience, we are storing this variable in the data set `Term2`. Use the same process to create `Term2$income`.
- Run a regression using `face` as the outcome variable and `education`, `numhh`, and `income` as explanatory variables.
- Summarize this model and identify the residual standard error ($s$) as well as the coefficient of determination ($R^2$) and the version adjusted for degrees of freedom ($R_a^2$).
`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term2 <- Term1[, c("education", "face", "income", "logface", "logincome", "numhh")]
```
`@sample_code`
```{r}
Term2$face <- exp(Term2$logface)/1000
Term2$income <- exp(Term2$logincome)/1000
Term_mlr1 <- lm(face ~ education + numhh + income, data = Term2)
summary(Term_mlr1)
```
`@solution`
```{r}
Term2$face <- exp(Term2$logface)/1000
Term2$income <- exp(Term2$logincome)/1000
Term_mlr1 <- lm(face ~ education + numhh + income, data = Term2)
summary(Term_mlr1)
```


---
## Binary variables

```yaml
type: VideoExercise

xp: 50

key: ff359ef406
```

`@projector_key`
a27f0e9bfd20f2e7d3c30b25a5acb7a8

---
## Binary variables and term life

```yaml
type: NormalExercise

xp: 100

key: 2f0001026b
```

We have seen how the variable `single` can be used with logarithmic income to explain logarithmic face amounts of term life insurance that people purchase. The coefficient associated with this variable turns out to be negative is intuitively appealing; if an individual is single, then that person may not have the strong need to purchase financial security for others in the family in the event of unexpected death. In this exercise, we will extend this by incorporating `single` into our larger regression model that contains other explanatory varibles, `logincome`, `education` and `numhh`. 

From a correlation table, you will see that there are relationships with among explanatory variables and so it is not clear whether adding `single` to the model is helpful. We will explore this by first fitting a model by just adding the binary variable single, examining summary statistics, and checking the significance of the variable. Then, we will explore the utility of the interaction of `single` with logarithmic income.

`@instructions`
- Calculate a table of correlation coefficients to examine pairwise linear relationships among the variables `numhh`, `education`, `logincome`, `single`, and  `logface`.
- Fit a multiple linear regression model of `logface` using explanatory variables `numhh`, `education`, `logincome`, and `single`. Examine the residual standard deviation $s$, the coefficient of determination $R^2$, and the adjusted version $R_a^2$. Also note the statistical significance of the coefficient associated with `single`.
- Repeat this but adding the interaction term  `single*logincome`.


`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term4 <- Term1[,c("numhh", "education", "logincome", "marstat", "logface")]
Term4$single <- 1*(Term4$marstat == 0)
```
`@sample_code`
```{r}
round(cor(Term4[,c("numhh", "education", "logincome", "single", "logface")]), digits = 3)
Term_mlr3 <- lm(logface ~ education + numhh + logincome + single, data = Term4)
summary(Term_mlr3)
Term_mlr4 <- lm(logface ~ education + numhh + logincome + single + single*logincome, data = Term4)
summary(Term_mlr4)
```
`@solution`
```{r}
round(cor(Term4[,c("numhh", "education", "logincome", "single", "logface")]), digits = 3)
Term_mlr3 <- lm(logface ~ education + numhh + logincome + single, data = Term4)
summary(Term_mlr3)
Term_mlr4 <- lm(logface ~ education + numhh + logincome + single + single*logincome, data = Term4)
summary(Term_mlr4)
```






---
## Categorical variables

```yaml
type: VideoExercise

xp: 50

key: ec71e48d7d
```

`@projector_key`
a96ac5c8eed3af533c4c8897c2b57542

---
## Categorical variables and Wisconsin hospital costs

```yaml
type: NormalExercise

xp: 100

key: 29d2203fad
```

This exercise examines the impact of various predictors on hospital charges. Identifying predictors of hospital charges can provide direction for hospitals, government, insurers and consumers in controlling these variables that in turn leads to better control of hospital costs. The data, from 1989, are aggregated by: 

- `drg`, diagnostic related groups of costs, 
- `payer`, type of health care provider (Fee for service, HMO, and other), and 
- `hsa`, nine major geographic areas.

Some preliminary analysis of the data has already been done. In this exercise, we will analyze `logcharge`, the logarithm of total hospital charges per number of discharges, in terms of `log_numdschg`, the logarithm of the number of discharges. In the dataset `Hcost` which has been loaded in advance, we restrict consideration to three types of drgs, numbers 209, 391, and 431.

`@instructions`
- Fit a basic linear regression model using logarithmic number of discharges to predict logarithmic hospital costs and superimposed the fitted regression line on the scatter plot.
- Produce a scatter plot of logarithmic number of discharges to predict logarithmic hospital costs. Allow plotting symbols and colors to vary by diagnostic related group.
- Fit a multiple linear regression using logarithmic number of discharges to predict logarithmic hospital costs, allowing intercepts and slopes to vary by diagnostic related groups.
- Superimposed the fits from the multiple linear regression model on the scatter plot of logarithmic number of discharges to predict logarithmic hospital costs. Note how slopes differ dramatically from the slope from the basic linear regression model.

`@hint`


`@pre_exercise_code`
```{r}
Hcost <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/2cc1e2739bf827093db31d7c4e6dcdc348ac984e/WiscHcosts.csv", header = TRUE)
Hcost1 <- subset(Hcost, drg == 209|drg == 391|drg == 430)
```
`@sample_code`
```{r}
hosp_blr <- lm(logcharge~log_numdschg, data=Hcost1)
plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge")
abline(hosp_blr, col="red")

plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge",
    pch= as.numeric(as.factor(Hcost1$drg)), 
    col = c("red", "black", "blue")[as.factor(Hcost1$drg)])
legend("left", legend=c("drg 209","drg 391", "drg 430"), col=c("red", "black", "blue"), pch = c(1,2,3))

hosp_mlr <- lm(logcharge~log_numdschg + as.factor(drg)*log_numdschg, data=Hcost1)
#summary(hosp_mlr)$coefficients[,1]
plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge",
         pch= as.numeric(as.factor(Hcost1$drg)), 
    col = c("red", "black", "blue")[as.factor(Hcost1$drg)])
xseq <- seq(0,10,length.out=100)
coef <- summary(hosp_mlr)$coefficients[,1]
fit209 <- coef[1] + coef[2]*xseq
lines(xseq,fit209, col="red")
fit391 <- coef[1] + coef[3] + (coef[2] + coef[5])*xseq
lines(xseq,fit391, col="black")
fit430 <- coef[1] + coef[4] + (coef[2] + coef[6])*xseq
lines(xseq,fit430, col="blue")
```
`@solution`
```{r}
hosp_blr <- lm(logcharge~log_numdschg, data=Hcost1)
plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge")
abline(hosp_blr, col="red")

plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge",
    pch= as.numeric(as.factor(Hcost1$drg)), 
    col = c("red", "black", "blue")[as.factor(Hcost1$drg)])
legend("left", legend=c("drg 209","drg 391", "drg 430"), col=c("red", "black", "blue"), pch = c(1,2,3))

hosp_mlr <- lm(logcharge~log_numdschg + as.factor(drg)*log_numdschg, data=Hcost1)
#summary(hosp_mlr)$coefficients[,1]
plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge",
         pch= as.numeric(as.factor(Hcost1$drg)), 
    col = c("red", "black", "blue")[as.factor(Hcost1$drg)])
xseq <- seq(0,10,length.out=100)
coef <- summary(hosp_mlr)$coefficients[,1]
fit209 <- coef[1] + coef[2]*xseq
lines(xseq,fit209, col="red")
fit391 <- coef[1] + coef[3] + (coef[2] + coef[5])*xseq
lines(xseq,fit391, col="black")
fit430 <- coef[1] + coef[4] + (coef[2] + coef[6])*xseq
lines(xseq,fit430, col="blue")
```






---
## Hypothesis testing

```yaml
type: VideoExercise

xp: 50

key: 156ef40aaf
```

`@projector_key`
df2187184761fab4d774149af7725157

---
## Hypothesis testing and Wisconsin hospital costs

```yaml
type: NormalExercise

xp: 100

key: f80245771a
```



`@instructions`


`@hint`









