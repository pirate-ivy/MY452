```
{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

```
getwd()
load("C:/Users/emmaw/OneDrive/MASTERS/MY452M/exercises/Week 2/hiedata_short.Rdata")
```
Inspect summary statistics for income and age
Summary(data[, c()])
Double quotes around variables
`summary(hiedata_short[, c("income", "age")])`

Create regression model
```
lm.mod <- lm(income ~ education + age + ghi, data = hiedata_short)
lm.mod
summary(lm.mod)
```

Create confindent intervals
`confint(object = lm.mod, parm = c("education", "age", "ghi"), level = 0.95)`

1) They're all significant (standard error is high relative to coefficient estimate)

`plot(x = hiedata_short$education, y = hiedata_short$income, type = "p", xlab = "Level of education", ylab = "Income", main = "Relationship between education and income \n")`

2) Expect the pearson's correlation coefficient to be neither positive nor negative, as the relationship doesn't look linear (maybe quadratic?)
```
lm.mod.educ <- lm(formula = income ~ education, data = hiedata_short)
abline(reg = lm.mod.educ, lwd = 2, col = "purple")
```
Line slopes upwards so linear pearson's correlation coefficient

`summary(lm.mod.educ)`
Estimate for intercept = 4.367, for education coefficient = 0.481
`confint(object = lm.mod.educ, parm = "education", level = 0.95)`

The coefficient estimate is equal to the gradient of the line. The intercept estimate is equal to the intercept of the line.
The t-value is greater than the critical value of 1.96. This is also reflected in the p-value which is highly significant at the 0.999 level.
The r-squared is 0.04424 meaning that the model (i.e. education alone) explains 4.4% of the VARIANCE in income.

```
lm.mod.all <- lm(formula = income ~ age + education + ghi, data = hiedata_short)
summary(lm.mod.all)
confint(object = lm.mod.all, parm = c("education", "age", "ghi", level = 0.95))
```
Now 13% of the variance in income is explained by the model (education, age and ghi together)

All coefficient estimates are significant as before.
NB: `education = education.pts` <- must define the variable as education
Feed the matrix -> data frame
```
education.pts <- seq(from = 0, to = 25, by = 1)`

fitted.values.data <- data.frame(education = education.pts, age = 30, ghi = 70)

fitted.values <- predict(object = lm.mod.all, newdata = fitted.values.data, interval = "confidence", level = 0.95)

fitted.values <- data.frame(fitted.values)

plot(x = education.pts, y = fitted.values$fit, type = "l", col = "red", xlab = "education (0 - 25 years)", ylab = "predicted income", main = "predicted relationship between education and income: \n age = 30, ghi = 70", ylim = c(0,20))

matlines(education.pts, fitted.values[, c("lwr", "upr")], lty = "dashed", col = "black", lwd = 2)
```
CLASS EXERCISES
1a) A one point increase in education level is associated with an increase in income of $560.
1b) H0 = education is not associated with income. T-value is 10.379 which is greater than (and large compared to) the critical value of 1.96 for a significance level of 0.95. Therefore, we can reject the null hypothesis that there is no association.
1c) R-squared is 0.1301: the model (with three explanatory variables) explains 13% of the variance in income observed. This is quite low.

Ex4) 0.559634
Ex3) 0.48

```
cor(hiedata_short[, c("education", income", "age", "ghi")], use = "complete.obs")
```
age and education are negatively correlated, but age is positively correlated with income. Adding age to the model reduces the size of the effect of education as some of this is absorbed by age?
