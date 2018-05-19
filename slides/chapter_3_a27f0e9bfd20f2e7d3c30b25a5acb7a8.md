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
## Final Slide

```yaml
type: FinalSlide
key: cdcc25c08e
```






`@script`



