---
  title: "Chapter 4. Variable Selection"
  description: "This chapter describes tools and techniques to help you select variables to enter into a linear regression model, beginning with an iterative model selection process. In applications with many potential explanatory variables, automatic variable selection procedures are available that will help you quickly evaluate many models. Nonetheless, automatic procedures have serious limitations including the inability to account properly for nonlinearities such as the impact of unusual points; this chapter expands upon the Chapter 2 discussion of unusual points. It also describes collinearity, a common feature of regression data where explanatory variables are linearly related to one another. Other topics that impact variable selection, including out-of-sample validation, are also introduced."
  v2: true

---
## An iterative approach to data analysis and modeling

```yaml
type: VideoExercise

xp: 50

key: 9da28ad7dd



```

`@projector_key`
9362f318b5a48b39912dd30a85aa2f41

---
## An iterative approach to data modeling

```yaml
type: MultipleChoiceExercise

xp: 50

key: 3c6425abfa



```

Which of the following is not true?

`@instructions`
- A. Diagnostic checking reveals symptoms of mistakes made in previous specifications.
- B. Diagnostic checking provides ways to correct mistakes made in previous specifications.
- C. Model formulation is accomplished by using prior knowledge of relationships.
- D. Understanding theoretical model properties is not really helpful when matching a model to data or inferring general relationships based on the data.

`@hint`












---
## Automatic variable selection procedures

```yaml
type: VideoExercise

xp: 50

key: 8c0358d3d9



```

`@projector_key`
fd8d5708669990bf0b1da87eaf4e45cc

---
## Data-snooping in stepwise regression

```yaml
type: NormalExercise

xp: 100

key: 3c43eee3af



```

Automatic variable selection procedures, such as the classic stepwise regression algorithm, are very good at detecting patterns. Sometimes they are too good in the sense that they detect patterns in the sample that are not evident in the population from which the data are drawn. The detect "spurious" patterns.

This excercise illustrates this phenomenom by using simulation techniques to draw a sample. The simulation is designed so that the outcome variable (*y*) and the explanatory variables are mutually independent. So, by design, there is no relationship between the outcome and the explanatory variables.

As part of the code set-up, we have *n* = 100 observations generated of the outcome *y* and 50 explanatory variables, `xvar1` through `xvar50`. A few steps show that collections of explanatory variables are not statistically significant. However, with the [stepwise()](https://www.rdocumentation.org/packages/Rcmdr/versions/2.0-4/topics/stepwise) command, you will find some statistically significant relationships. This is because the `stepwise` procedure is repeatedly using *t*-tests - hypothesis testing procedures that are design to falsely detect a relationship $\alpha$ fraction of the time (typically 5\%). For example, if you run a *t*-test 50 times (for each explanatory variable), you can expect to get two or three "statistically significant" explanatory variables even for unrelated variables (because $50 \times 0.05 = 2.5$).

`@instructions`
- Fit a basic linear regression model and multiple linear regression model with the first ten explanatory variables. Compare the models via an *F* test.
- Fit a multiple linear regression model with all fifty explanatory variables. Compare this model to the one with ten variables via an *F* test.
- Use the `stepwise` function to find the best model starting with the fitted model containing all fifty explanatory variables.
- Fit the model identified by the stepwise regression algorithm and summarize the fit.


`@pre_exercise_code`
```{r}
set.seed(1237)
X <- as.data.frame(matrix(rnorm(100*50, mean = 0, sd = 1), ncol = 50))
colnames(X) <- paste("xvar", 1:50, sep = "")
X$y <- with(X, matrix(rnorm(100*1, mean = 0, sd = 1), ncol = 1))
```
`@sample_code`
```{r}
modelStep1 <- lm(y ~ xvar1, data = X)
summary(modelStep1)

modelStep2 <- lm(y ~ xvar1 + xvar2 + xvar3, data = X)
#summary(modelStep2)
anova(modelStep1,modelStep2)

modelStep3 <- lm(y ~ xvar1 + xvar2 + xvar3 + xvar4 + xvar5 + xvar6 + xvar7 + xvar8 + xvar9 + xvar10, data = X)
#summary(modelStep3)
anova(modelStep2,modelStep3)

modelStep4 <- lm(y ~ xvar1 + xvar2 + xvar3 + xvar4 + xvar5 + xvar6 + xvar7 + xvar8 + xvar9 + xvar10 + xvar11 + xvar12 + xvar13 + xvar14 + xvar15 + xvar16 + xvar17 + xvar18 + xvar19 + xvar20 + xvar21 + xvar22 + xvar23 + xvar24 + xvar25 + xvar26 + xvar27 + xvar28 + xvar29 + xvar30 + xvar31 + xvar32 + xvar33 + xvar34 + xvar35 + xvar36 + xvar37 + xvar38 + xvar39 + xvar40 + xvar41 + xvar42 + xvar43 + xvar44 + xvar45 + xvar46 + xvar47 + xvar48 + xvar49 + xvar50, data = X)
#summary(modelStep4)
anova(modelStep4)
anova(modelStep3,modelStep4)

#library(Rcmdr)
#temp <- stepwise(modelStep4, direction = 'backward/forward')
#summary(temp)

#  The function "stepwise" is in the Rcmdr library. Alternatively, you can use "step" function as below:
#  k CONTROLS THE COMPLEXITY OF THE MODEL
#  step(modelStep4, k = log(length(y)))
#  You can check the model of those three explanatory variables to see whether all of them are significant
modelStep5 <- lm(y ~ xvar27 + xvar29 + xvar32, data = X)
summary(modelStep5)
```
`@solution`
```{r}
modelStep1 <- lm(y ~ xvar1, data = X)
summary(modelStep1)

modelStep2 <- lm(y ~ xvar1 + xvar2 + xvar3, data = X)
#summary(modelStep2)
anova(modelStep1,modelStep2)

modelStep3 <- lm(y ~ xvar1 + xvar2 + xvar3 + xvar4 + xvar5 + xvar6 + xvar7 + xvar8 + xvar9 + xvar10, data = X)
#summary(modelStep3)
anova(modelStep2,modelStep3)

modelStep4 <- lm(y ~ xvar1 + xvar2 + xvar3 + xvar4 + xvar5 + xvar6 + xvar7 + xvar8 + xvar9 + xvar10 + xvar11 + xvar12 + xvar13 + xvar14 + xvar15 + xvar16 + xvar17 + xvar18 + xvar19 + xvar20 + xvar21 + xvar22 + xvar23 + xvar24 + xvar25 + xvar26 + xvar27 + xvar28 + xvar29 + xvar30 + xvar31 + xvar32 + xvar33 + xvar34 + xvar35 + xvar36 + xvar37 + xvar38 + xvar39 + xvar40 + xvar41 + xvar42 + xvar43 + xvar44 + xvar45 + xvar46 + xvar47 + xvar48 + xvar49 + xvar50, data = X)
#summary(modelStep4)
anova(modelStep4)
anova(modelStep3,modelStep4)

#library(Rcmdr)
#temp <- stepwise(modelStep4, direction = 'backward/forward')
#summary(temp)

#  The function "stepwise" is in the Rcmdr library. Alternatively, you can use "step" function as below:
#  k CONTROLS THE COMPLEXITY OF THE MODEL
#  step(modelStep4, k = log(length(y)))
#  You can check the model of those three explanatory variables to see whether all of them are significant
modelStep5 <- lm(y ~ xvar27 + xvar29 + xvar32, data = X)
summary(modelStep5)
```







---
## Residual analysis

```yaml
type: VideoExercise

xp: 50

key: 37c4ebf2d6



```

`@projector_key`
1a22b8308fcc14590ae2bdb95030c2a2

---
## Residual analysis and stock liquidity

```yaml
type: NormalExercise

xp: 100

key: d62cb0bd86



```

nothing yet













---
## Added variable plot and refrigerator prices

```yaml
type: NormalExercise

xp: 100

key: ecd90f8bcd



```

What characteristics of a refrigerator are important in determining its price (`price`)? We consider here several characteristics of a refrigerator, including the size of the
refrigerator in cubic feet (`rsize`), the size of the freezer compartment in cubic feet (`fsize`), the average amount of money spent per year to operate the refrigerator (`ecost`, for energy cost), the number of shelves in the refrigerator and freezer doors (`shelves`), and the number of features (`features`). The features variable includes shelves for cans, see-through crispers, ice makers, egg racks and so on.

Both consumers and manufacturers are interested in models of refrigerator prices. Other things equal, consumers generally prefer larger refrigerators with lower energy costs that have more features. Due to forces of supply and demand, we would expect consumers to pay more for these refrigerators. A larger refrigerator with lower energy costs that has more features at the similar price is considered a bargain to the consumer. How much extra would the consumer be willing to pay for this additional space? A model of
prices for refrigerators on the market provides some insight to this question.

To this end, we analyze data from *n* = 37 refrigerators. 

The table provides the basic summary statistics for the response variable price and the five explanatory variables. From this table, we see that the average refrigerator price is $\overline{y}$= \$626.40, with standard deviation $s_{y}$ = \$139.80. Similarly, the average annual amount to operate a refrigerator, or average ecost, is \$70.51.

`@instructions`
Nothing yet












---
## Unusual observations

```yaml
type: VideoExercise

xp: 50

key: f26dac9523



```

`@projector_key`
3958fa9f4bc063310c17d368a7ad400d

---
## Outlier example

```yaml
type: NormalExercise

xp: 100

key: a61e86392e



```

Nothing yet













---
## High leverage and stock liquidity

```yaml
type: NormalExercise

xp: 100

key: e072807cbe



```

placeholder













---
## Collinearity

```yaml
type: VideoExercise

xp: 50

key: 1e651c4018



```

`@projector_key`
3f319d9bce5db7f2d39df9e2e14f3c46

---
## Collinearity and data

```yaml
type: NormalExercise

xp: 100

key: 4d112f601d



```















---
## Selection criteria

```yaml
type: VideoExercise

xp: 50

key: fbe7bc54a3



```

`@projector_key`
5ee9a1ceca54fdf811fb1ed24ed36673

---
## Selection criteria and data

```yaml
type: NormalExercise

xp: 100

key: 40e9eec496



```

Placeholder











