---
title: Insert title here
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

`@script`




---
## Description of the data

```yaml
type: FullSlide
key: 141ba302d2
```

`@part1`






`@script`




---
## Summary Statistics

```yaml
type: TwoRows
key: 61bb65a96a
```

`@part1`
```
library(Rcmdr)
options(scipen = 100, digits = 4)
numSummary(Lot[,c("pop", "sales")], statistics = c("mean", "sd", "quantiles"), 
                              quantiles = c(0,.5,1))
```

`@part2`
```
      mean    sd  0%  50%  100%  n
pop   9311 11098 280 4406 39098 50
sales 6495  8103 189 2426 33181 50
```




`@script`




---
## Visualizing Skewed Distributions

```yaml
type: FullImageSlide
key: 61e50a6ab8
```

`@part1`
```
par(mfrow = c(1, 2))
hist(Lot$pop, main = "")
hist(Lot$sales, main = "")
```





`@script`




---
## Visualizing relationships with a scatter plot

```yaml
type: FullImageSlide
key: 6f0c4e1815
```

`@part1`
```
plot(Lot$pop, Lot$sales)
```





`@script`




---
## Correlation Coefficient

```yaml
type: FullSlide
key: 23565d7a07
```

`@part1`
Correlation Coefficient





`@script`




---
## Final Slide

```yaml
type: FinalSlide
key: 81b9a849f9
```






`@script`



