---
title: Method of least squares
key: f251f87ff6f6208b2a3baba08e275eaa

---
## Method of least squares

```yaml
type: TitleSlide
key: 13ec0dc9f8
```





`@lower_third`
name: Frees
title: Instructor

`@script`




---
## Correlation table

```yaml
type: TwoRows
key: ee15d2fe6e
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
## Scatterplot matrix

```yaml
type: FullImageSlide
key: 0e9613ac4a
```

`@part1`
```
Term3 <- Term2[,c("numhh", "education", "logincome", "logface")]
pairs(Term3, upper.panel = NULL, gap = 0, cex.labels = 1.25)
```
![](https://assets.datacamp.com/production/repositories/2610/datasets/6e496c2af706c1d1889671206e7256d402dabe00/Ch3ScatterplotMatrixA.png)





`@script`




---
## Visualizing a regression plane

```yaml
type: TwoColumns
key: 3a26821b44
```

`@part1`
**This Figure**

*logface* = 5 + 0.221 *education* +0.354 *logincome*

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
## Method of least squares

```yaml
type: TwoRows
key: 4331b60043
```

`@part1`
-  For observation $\{(y, x_1, \ldots, x_k)\}$,   the height of the regression plane is $$b_0 + b_1 x_1 + \cdots + b_k x_k .$$
-  Thus, $y - (b_0 + b_1 x_1 + \cdots + b_k x_k)$ represents the deviation.
- The sum of squared deviations is $$SS(b_0, \ldots, b_k) = \sum (y - (b_0 + b_1 x_1 + \cdots + b_k x_k))^2 .$$
- The *method of least squares* -- determine values of $b_0, \ldots, b_k$ that minimize $SS$.

`@part2`
![](https://assets.datacamp.com/production/repositories/2610/datasets/96cd1706aed99fc70a4979990323cc01313f0621/Ch3RegressionPlane2.png)




`@script`




---
## Fit a multiple linear regression model

```yaml
type: TwoRows
key: 7bc97ca7c8
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

$\hat{logface} = 2.5841 + 0.2064 ~education+0.3060 ~numhh+ 0.4935~logincome$

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
key: b84c3bc685
```






`@script`



