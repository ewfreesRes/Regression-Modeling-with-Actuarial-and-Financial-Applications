---
title: Insert title here
key: dd5d704d841ca6fae0df18c9b9e020c0

---
## Method of Least Squares

```yaml
type: TitleSlide
key: 10a4648260
```





`@lower_third`
name: Frees
title: Instructor




---
## Demand for Term Life Insurance

```yaml
type: FullSlide
key: 3797e62ab5
```

`@part1`
“Who buys insurance and how much do they buy?”
- Companies have data on current customers
- How do get info on potential (new) customers?

To understand demand, consider the Survey of Consumer Finances (*SCF*)
- This is a nationally representative sample that contains extensive information on potential U.S. customers.
- We study a random sample of 500 of the 4,519 households with positive income that were interviewed in the 2004 survey.
- We now focus on *n* = 275 households that purchased term life insurance








---
## Term Life Insurance Summary Statistics

```yaml
type: FullSlide
key: 51042694ec
```

`@part1`
We study *y = face*, the amount that the company will pay in the event of the death of the named insured.

 We focus on *k* = 3 explanatory variables
- annual *income*,
- the number of years of *education* of the survey respondent and
- the number of household members, *numhh*.

The statistics suggest that *income* and *face* are skewed.








---
## Summary Statistics

```yaml
type: TwoRows
key: 1cc72133a1
```

`@part1`
```
library(Rcmdr)
Term2 <- Term1[, c("education", "face", "income", "logface", "logincome", 
   "numhh")]
options(scipen = 100, digits = 4)
summvar <- numSummary(Term2, statistic = c("mean", "sd", "quantiles"), 
   quantiles = c(0, .5, 1))
summvar
```

`@part2`
```
               mean          sd      0%       50%        100%   n
education     14.52       2.549   2.000     16.00       17.00 275
face      747581.45 1674362.433 800.000 150000.00 14000000.00 275
income    208974.62  824009.775 260.000  65000.00 10000000.00 275
logface       11.99       1.871   6.685     11.92       16.45 275
logincome     11.15       1.295   5.561     11.08       16.12 275
numhh          2.96       1.493   1.000      3.00        9.00 275
```




`@script`




---
## Scatter plots of income versus face in original and logarithmic units

```yaml
type: FullImageSlide
key: a6913ce44f
```

`@part1`
```
par(mfrow = c(1, 2))
plot(Term2$income, Term2$face, xlab = "income", ylab = "face")
plot(Term2$logincome, Term2$logface, xlab = "log", ylab = "log face")
```
![](https://assets.datacamp.com/production/repositories/2610/datasets/4452970eef5312f68838ed2ebb931dcdab764795/Ch3TermLifeBasic.png)





`@script`




---
## Table of Correlations

```yaml
type: TwoRows
key: c7743fa611
```

`@part1`
```
round(cor(Term2), digits=3)
```

`@part2`
```
          education  face income logface logincome  numhh
education     1.000 0.244  0.163   0.383     0.343 -0.064
face          0.244 1.000  0.217   0.656     0.323  0.107
income        0.163 0.217  1.000   0.251     0.518  0.142
logface       0.383 0.656  0.251   1.000     0.482  0.288
logincome     0.343 0.323  0.518   0.482     1.000  0.179
numhh        -0.064 0.107  0.142   0.288     0.179  1.000
```




`@script`




---
## Scatterplot Matrix

```yaml
type: FullImageSlide
key: dc73fa06e8
```

`@part1`
```
Term3 <- Term2[,c("numhh", "education", "logincome", "logface")]
pairs(Term3, upper.panel = NULL, gap = 0, cex.labels = 1.25)
```
![](https://assets.datacamp.com/production/repositories/2610/datasets/6e496c2af706c1d1889671206e7256d402dabe00/Ch3ScatterplotMatrixA.png)





`@script`




---
## Regression Plane

```yaml
type: TwoColumns
key: a7cdc911f7
```

`@part1`
```
education <- seq(3, 16, length = 15)
logincome <- seq(5, 15, length = 15)
f <- function(education,logincome){ 
  r <- 5 + 0.221*education + 
             0.354*logincome
  }
logface <- 
     outer(education, logincome,f)
persp(education, logincome, logface, 
      theta = 30, phi = 30, 
      expand = 0.5, 
      ticktype = "detailed")
```

`@part2`
![](https://assets.datacamp.com/production/repositories/2610/datasets/65af12e346237f01d770c86d32ec484c8bb02127/Ch3RegressionPlane.png)




`@script`




---
## Fit a Multiple Linear Regression Model

```yaml
type: TwoRows
key: 8d8a7b9205
```

`@part1`
```
model_mlr <- lm(logface ~ education + numhh + logincome, data = Term2)
round(coefficients(model_mlr), digits=4)
```
```
> (Intercept)   education       numhh   logincome 
>    2.5841      0.2064      0.3060      0.4935 
```

$\hat{logface} = 2.5841 + 0.2064 education+0.3060 numhh+ 0.4935logincome$

`@part2`
```
newdata <- data.frame(education = 12, numhh = 3, logincome = log(60000))
exp(predict(model_mlr, newdata))
```

```
>         1 
>  90135.86 
```




`@script`




---
## Let's Practice

```yaml
type: FinalSlide
key: f2d9bd6e9b
```








