---
title: Correlation
key: 98aeb5a5bd795a7c8716aba8e177decb

---
## Correlation

```yaml
type: TitleSlide
key: 0901319abc
```





`@lower_third`
name: Frees
title: Instructor




---
## Wisconsin lottery data description

```yaml
type: FullSlide
key: 141ba302d2
```

`@part1`
- What factors affect lottery sales? Helpful to know for marketing, e.g., where to establish new retail outlets.
- *i* unit of analysis, zip (postal) code
- *n* = 50 randomly selected geographic areas
- *y*= average lottery sales (sales)
- *x* = population (pop), measure of size of the area.





`@script`




---
## Summary statistics

```yaml
type: TwoRows
key: 61bb65a96a
```

`@part1`
```
(as.data.frame(psych::describe(Lot)))[,c(2,3,4,5,8,9)]

#library(Rcmdr)
#options(scipen = 100, digits = 4)
#numSummary(Lot[,c("pop", "sales")], statistics = c("mean", "sd", "quantiles"), 
#                            quantiles = c(0,.5,1))

```

`@part2`
```
         n     mean          sd   median   min     max
pop     50 9311.040 11098.15695 4405.500 280.0 39098.0
sales   50 6494.829  8103.01250 2426.406 189.0 33181.4
medhome 50   57.092    18.37312   53.900  34.5   120.0
```







---
## Visualizing skewed distributions

```yaml
type: FullImageSlide
key: 61e50a6ab8
```

`@part1`
```
par(mfrow = c(1, 2)); hist(Lot$pop, main = ""); hist(Lot$sales, main = "")
```
![](https://assets.datacamp.com/production/repositories/2610/datasets/d56a7b1a213b62bc51a55e00b8e13f3975de06f9/Ch2DistnPop_Sales.png)








---
## Visualizing relationships with a scatter plot

```yaml
type: FullImageSlide
key: 6f0c4e1815
```

`@part1`
```
plot(Lot$pop, Lot$sales, xlab = "population", ylab = "sales")```
![](https://assets.datacamp.com/production/repositories/2610/datasets/95126817af9ffd6f0dde8977d357a58b9e2216c6/Ch2PlotPop_Sales.png)








---
## Correlation coefficient

```yaml
type: FullSlide
key: 23565d7a07
```

`@part1`
- The ordinary, or Pearson, correlation coefficient is defined as

$$
r = \frac{1}{(n-1) sd(x) sd(y)} \sum_i (x_i - mean(x))(y_i - mean(y))
$$
- The correlation coefficient is said to be a “unitless” measure.
    - It is unaffected by scale and location changes of either, or both,
variables.





`@script`




---
## Let's Practice

```yaml
type: FinalSlide
key: 81b9a849f9
```






`@script`



