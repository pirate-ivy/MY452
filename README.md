```
{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

```
getwd()
load("C:/Users/emmaw/OneDrive/MASTERS/MY452M/exercises/Week 2/hiedata_short.Rdata")
```

You will fit linear regression models for which the quantitative response variable is family income (i.e., income in the data frame hiedata_short). The variables education, age, and ghi (i.e., General Health Index) will be used as explanatory variables.

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
