---
title: Selection criteria
key: 5ee9a1ceca54fdf811fb1ed24ed36673

---
## Selection criteria

```yaml
type: TitleSlide
key: ea28a38e93
```





`@lower_third`
name: Frees
title: Instructor




---
## Goodness of fit

```yaml
type: FullSlide
key: 027e480888
```

`@part1`
- Criteria that measure the proximity of the fitted model and realized data are known as
*goodness of fit* statistics.
- Basic examples include:
    - the coefficient of determination $(R^{2})$, 
    - an adjusted version $(R_{a}^{2})$, 
    - the size of the typical error $(s)$, and 
    - $t$-ratios for each regression coefficient.








---
## Goodness of fit and information criteria

```yaml
type: FullSlide
key: 0c54e541dd
```

`@part1`
A general measure is *Akaike's Information Criterion*, defined as

$$
AIC = -2 \times (fitted~log~likelihood) + 2 \times
(number~of~parameters)
$$

- For model comparison, the smaller the $AIC,$ the better is the fit.
- This measures balances the fit (in the first part) with a penalty for complexity (in the second part)
- It is a general measure - for linear regression, it reduces to

$$
AIC = n \ln (s^2) + n \ln (2 \pi) +n +k + 3 .
$$

- So, selecting a model to minimize $s$ or $s^2$ is equivalent to model selection based on minimizing $AIC$ (same *k*).








---
## Out of sample validation

```yaml
type: FullSlide
key: fe2d94bdf9
```

`@part1`
- When you choose a model to minimize $s$ or $AIC$, it is based on how well the model fits the data at hand, or the *model development*, or *training*, data
- As we have seen, this approach is susceptible to overfitting.
- A better approach is to validate the model on a *model validation*, or *test* data set, held out for this purpose.








---
## Out of sample validation procedure

```yaml
type: FullSlide
key: 540d0f849e
```

`@part1`
- (i) Using the model development subsample, fit a candidate model.
- (ii) Using the  Step (ii) model and the explanatory variables from the validation subsample, "predict" the dependent variables in the validation subsample, $\hat{y}_i$, where $i=n_1 + 1,...,n_1 + n_2$.
- (iii) Calculate the *sum of absolute errors*

$$SAE=\sum_{i=n_1+1}^{n_1+n_2} |y_i-\hat{y}_i| . $$

Repeat Steps (i) through (iii) for each candidate model. Choose the
model with the smallest *SAE*.








---
## Cross-validation

```yaml
type: FullSlide
key: 7b5f043603
```

`@part1`
- With out-of-sample validation, the statistic depends on a random split between in-sample and out-of-sample data (a problem for data sets that are not large)
- Alternatively, one may use *cross-validation*
    - Use a random mechanism to split the data into *k* subsets, (e.g., 5-10) 
    - Use the first *k-1* subsamples to estimate model parameters. Then, "predict" the outcomes for the *k*th subsample and use  *SAE* to summarize the fit
    - Repeat this by holding out each of the *k* sub-samples, summarizing with a cumulative *SAE*.
-  Repeat these steps for several candidate models. 
    - Choose the model with the lowest cumulative *SAE* statistic.





`@script`




---
## Final Slide

```yaml
type: FinalSlide
key: 6539a9d743
```








