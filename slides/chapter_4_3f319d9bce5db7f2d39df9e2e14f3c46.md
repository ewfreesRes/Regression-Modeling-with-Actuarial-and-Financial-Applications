---
title: Collinearity
key: 3f319d9bce5db7f2d39df9e2e14f3c46

---
## Collinearity

```yaml
type: TitleSlide
key: db24c4265e
```





`@lower_third`
name: Frees
title: Instructor




---
## Collinearity

```yaml
type: FullSlide
key: 68ed1fdc2b
```

`@part1`
- *Collinearity*, or *multicollinearity*, occurs when one explanatory variable is, or nearly is, a linear combination of the other explanatory variables.
    - Think of the explanatory variables as being highly correlated with one another.
- Collinearity neither precludes us from getting good fits nor from making predictions of new observations.
    - Estimates of error variances and, tests of model adequacy, are
still reliable.
- Standard errors of individual regression coefficients can be large.
    - Individual regression coefficients may not be meaningful.
    - Because a large standard error means that the corresponding
*t*-ratio is small, it is difficult to detect the importance of a variable.





`@script`




---
## Quantifying collinearity

```yaml
type: FullSlide
key: 023fc3cf78
```

`@part1`
A common way to quantify collinearity is through the *variance inflation factor (VIF)*.

- Suppose that the set of explanatory variables is labeled $x_1, x_2, ..., x_k$.
- Run the regression using $x_{j}$ as the "outcome" and the other $x$'s  as the explanatory variables.
- Denote the coefficient of determination from this regression by $R_j^2$.
- Define the variance inflation factor

$$
VIF_j=\frac{1}{1-R_j^{2}}
$$





`@script`




---
## Options for handling collinearity

```yaml
type: FullSlide
key: d62b6b5703
```

`@part1`
- Rule of thumb: When $VIF_j$ exceeds 10 (which is equivalent to $R_j^{2}>90\%$), we say that severe collinearity exists. This may signal is a need for action.
- Recode the variables by "centering" - that is, subtract the mean and divide by the standard deviation.
- Ignore the collinearity in the analysis but comment on it in the interpretation. Probably the most common approach.
- Replace one or more variables by auxiliary variables or  transformed versions.
- Remove one or more variables.  Easy.  Which One? is hard.
    - Use interpretation.  Which variable(s) do you feel most comfortable with?
    - Use automatic variable selection procedures to suggest a model.





`@script`




---
## Let's Practice

```yaml
type: FinalSlide
key: 05c4222b59
```






`@script`



