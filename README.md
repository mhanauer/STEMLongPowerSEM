Multigroup analysis in R with lavaan
Visual is x1:x3 which are the measures that make up visual.

Ethnicity needs to be one variable.  Time needs to be four variables.  one
```{r}
library(lavaan)
set.seed(123)
time1 = rnorm(720/4)
time2 = rnorm(720/4)
time3 = rnorm(720/4)
time4 = rnorm(720/4)
eth = c(rep("HIS", 20), rep("BL", 20), rep("AI", 10), rep("AA", 20), rep("WHITE", 180-70))
eth = as.data.frame(eth)

dataTest = cbind(time1, time2, time3, time4, eth)
names(dataTest) = c("t1", "t2", "t3", "t4" , "eth")
dataTest = as.data.frame(dataTest)
head(dataTest)


model <- ' i =~ 1*t1 + 1*t2 + 1*t3 + 1*t4
           s =~ 0*t1 + 1*t2 + 2*t3 + 3*t4 '
fit <- growth(model, data=dataTest, group = "eth")
summary(fit)


data("HolzingerSwineford1939")
HolzingerSwineford1939

HS.model <- '  visual =~ x1 + x2 + x3
              textual =~ x4 + x5 + x6
              speed   =~ x7 + x8 + x9 '
fit <- cfa(HS.model, 
           data = HolzingerSwineford1939, 
           group = "school")

summary(fit)


```
