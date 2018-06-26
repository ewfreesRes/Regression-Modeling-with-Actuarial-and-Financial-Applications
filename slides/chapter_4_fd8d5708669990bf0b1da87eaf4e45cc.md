---
title: Automatic variable selection
key: fd8d5708669990bf0b1da87eaf4e45cc

---
## Automatic variable selection procedures

```yaml
type: TitleSlide
key: c38244cfd4
```





`@lower_third`
name: Frees
title: Instructor




---
## Classic stepwise regression algorithm

```yaml
type: FullSlide
key: dd46fa3c66
```

`@part1`
Suppose that the analyst has identified one variable as the outcome, $y$, and $k$ potential explanatory variables, $x_1, x_2, \ldots, x_k$.

- (i). Consider all possible regressions using one explanatory variable. Choose the one with the highest *t*-statistic.
- (ii). Add a variable to the model from the previous step. The variable to enter is with the highest *t*-statistic.
- (iii). Delete a variable to the model from the previous step. Delete the variable with the small *t*-statistic if the statistic is less than, e.g., 2 in absolute value.
- (iv). Repeat steps (ii) and (iii) until all possible additions and deletions are performed.





`@script`




---
## Drawbacks of stepwise regression

```yaml
type: FullSlide
key: b123833808
```

`@part1`
- The procedure "snoops" through a large number of models and may fit the data "too well."
- There is no guarantee that the selected model is the best. 
    - The algorithm does not consider models that are based on nonlinear combinations of explanatory variables. 
    - It ignores the presence of outliers and high leverage points.





`@script`




---
## Data-snooping in stepwise regression

```yaml
type: TwoRows
key: e9da613a72
```

`@part1`
- Generate `y` and `xvar1` through `xvar50` using a random number generator
- By design, there is no relation between `y` and   `xvar1` through `xvar50`

- **But**, through stepwise regression, we **"discover"** a relationship that explains 14% of the variation!!!

`@part2`
```
Call: lm(formula = y ~ xvar27 + xvar29 + xvar32, data = X)
Coefficients:
            Estimate Std. Error t value Pr(>|t|)  
(Intercept)  -0.04885    0.09531  -0.513   0.6094  
xvar27        0.21063    0.09724   2.166   0.0328 *
xvar29        0.24887    0.10185   2.443   0.0164 *
xvar32        0.25390    0.09823   2.585   0.0112 *

Residual standard error: 0.9171 on 96 degrees of freedom
Multiple R-squared:  0.1401,    Adjusted R-squared:  0.1132 
F-statistic: 5.212 on 3 and 96 DF,  p-value: 0.002233
```




`@script`




---
## Variants of stepwise regression

```yaml
type: FullSlide
key: ef5f73311d
```

`@part1`
This uses the `R` function [step()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/step)

- The option `direction` can be used to change how variables enter
    - Forward selection. Add one variable at a time without trying to delete variables.
    - Backwards selection. Start with the full model and delete one variable at a time without trying to add variables. 
- The option `scope` can be used to specify which variables must be included





`@script`




---
## Automatic variable selection procedures

```yaml
type: FullSlide
key: c5aeb5b831
```

`@part1`
- Stepwise regression is a type of automatic variable selection procedure.
- These procedures are useful because they can quickly search through several candidate models. They  mechanize certain routine tasks and are excellent at discovering patterns in data.
- They are so good at detecting patterns that they analyst must be wary of overfitting (data-snooping)   
- They can miss certain patterns (nonlinearities, unusual points)
- A model suggested by automatic variable selection procedures should be subject to the same careful diagnostic checking procedures as a model arrived at by any other means





`@script`




---
## Final Slide

```yaml
type: FinalSlide
key: 9b306278c0
```








