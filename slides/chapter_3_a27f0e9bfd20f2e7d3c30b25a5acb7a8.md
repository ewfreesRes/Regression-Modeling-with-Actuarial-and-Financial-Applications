---
title: Insert title here
key: a27f0e9bfd20f2e7d3c30b25a5acb7a8

---
## Binary variables

```yaml
type: TitleSlide
key: 192f00eedc
```





`@lower_third`
name: Frees
title: Instructor

`@script`




---
## Binary variables

```yaml
type: FullSlide
key: 23249e5b8e
```

`@part1`
- We can define a new variable

$$
single= \left\\{ \begin{array}{ll}
        0 & \text{for other respondents} \\\\
        1 & \text{for single respondents}
\end{array} \right.
$$
- The variable *single* is said to be an *indicator*, or *dummy*, variable.
- To interpret coefficients, we now consider the regression function

$$\text{E }logface = \beta_0 + \beta_1 logincome + \beta_2 single$$
- This can be expressed as two lines

$$
\text{E }logface = \left\\{ \begin{array}{ll}
        \beta_0 + \beta_1  logincome           & \text{for other respondents} \\\\
        \beta_0 + \beta_2 + \beta_1  logincome & \text{for single respondents}
\end{array}\right. .
$$
- The least squares method of calculating the estimators, and the resulting theoretical properties, are the still valid when using
binary variables.





`@script`




---
## Visualize effect of binary variables

```yaml
type: FullImageSlide
key: 444157d3f9
```

`@part1`
![](https://assets.datacamp.com/production/repositories/2610/datasets/c4674f54cee57f9512d8e863da90785e1c62e01d/Ch3PlotIncomeFaceSingle.png)





`@script`




---
## R script for visualization

```yaml
type: FullCodeSlide
key: d8dfaddc8e
```

`@part1`
```
Term4 <- Term1[,c("numhh", "education", "logincome", "logface", "marstat")]

Term4$marstat <- as.factor(Term4$marstat)
Term4$single <- 1*(Term4$marstat == 0)

model_single <- lm(logface ~ logincome + single, data = Term4)

plot(Term4$logincome,Term4$logface,xlab="logarithmic income", ylab="log face",
    pch= 1+16*Term4$single, col = c("red", "black", "black")[Term4$marstat])

Ey1 <- model_single$coefficients[1]+model_single$coefficients[2]*Term4$logincome
Ey2 <- Ey1 + model_single$coefficients[3]
lines(Term4$logincome, Ey1)
lines(Term4$logincome, Ey2, col="red")
```





`@script`




---
##  Interaction Terms

```yaml
type: FullSlide
key: ddc7338a16
```

`@part1`
- Linear regression models are defined in terms of linear combinations of explanatory varibles but we can expand their scope through nonlinear transformations
   - One type of nonlinear transform is the product of two varibles that is used to create what is known as an *interaction* variable
- To interpret coefficients, we now consider the regression function

$$\text{E }logface = \beta_0 + \beta_1 logincome + \beta_2 single + \beta_3 single*logincome
$$
- This can be expressed as two lines with different slopes

$$
\text{E }logface = \left\\{ \begin{array}{ll}
        \beta_0 + \beta_1   logincome           & \textrm{for other respondents} \\\\
        \beta_0 + \beta_2 + (\beta_1  + \beta_3) logincome & \textrm{for single respondents}
\end{array} \right. .
$$





`@script`




---
## Visualizing binary variables with interactions terms

```yaml
type: FullImageSlide
key: 09d570a71b
```

`@part1`
![](https://assets.datacamp.com/production/repositories/2610/datasets/b8be15b4d80025f71806807c5d501ad9b83b788e/Ch3PlotIncomeFaceSingleInteract.png)





`@script`




---
## Let's Practice

```yaml
type: FinalSlide
key: cdcc25c08e
```






`@script`



