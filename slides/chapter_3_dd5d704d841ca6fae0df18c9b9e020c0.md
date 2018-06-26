---
title: Term life data
key: dd5d704d841ca6fae0df18c9b9e020c0

---
## Term life data

```yaml
type: TitleSlide
key: 10a4648260
```





`@lower_third`
name: Frees
title: Instructor




---
## Demand for term life insurance

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
## Term life insurance summary statistics

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

The data suggest that *income* and *face* are skewed so we also introduce logarithmic versions.








---
## Summary statistics

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




---
## Final Slide

```yaml
type: FinalSlide
key: f2d9bd6e9b
```








