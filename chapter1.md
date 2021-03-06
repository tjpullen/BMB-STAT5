---
title       : STAT5 - Hypothesis Testing 2
description : Hypothesis testing in more detail





--- type:NormalExercise lang:r xp:100 skills:1 key:b1eb285d60
## One sample t test

The **one sample t test** compares the mean of one sample to a particular value.

**Example: Are our students taller than average?**

The mean height of 19 year-old females in the WHO reference data is 163.1548 cm. You could use a one sample t test to compare a sample of this year's students to this mean value.

*** =instructions

The height of a sample of 20 female students in this age group was measured and placed in the vector `heights`.

Perform a one sample t test to compare the mean of `heights` to the population mean (`mu =`) of 163.15.

You need to use the `t.test()` function, and you need to give it the list of all the heights in the sample rather than just the sample mean.

*** =hint
You need to enter 2 arguments: the vector of heights and the population mean: `mu = 163.15`
*** =pre_exercise_code
```{r}
set.seed(967)
heights <- rnorm(n = 20, mean = 163.1548 + 4, sd = 6.5409)

```

*** =sample_code
```{r}
# t test to compare heights to 163.15


```

*** =solution
```{r}
# t test to compare heights to 163.15
t.test(heights, mu = 163.15)

```

*** =sct
```{r}
test_function("t.test", args = c("x", "mu"))
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:f15bb8f875
## One sample t test (2)

Perform the t test again to compare `heights` to a population mean of 163.15.

Look at the output.

With a threshold of $\alpha = 0.05$ do you reject the null hypothesis?

*** =instructions
- yes
- no
*** =hint

*** =pre_exercise_code
```{r}
set.seed(967)
heights <- rnorm(n = 20, mean = 163.1548 + 4, sd = 6.5409)
```

*** =sct
```{r}
test_mc(correct = 1)
```

--- type:NormalExercise lang:r xp:100 skills:1 key:04f47ebac9
## Two sample t test

The **two sample t test** compares the means of two samples.

Say you want to test whether a new compound causes overweight mice to lose weight. You could treat 10 mice with the drug and compare them to 10 mice which were not treated with the drug (or better still treated with a placebo drug).

The weights of 10 mice for each cohort have been stored in `data1`. The data are arranged with the weights stored in the `weight` column and a `treatment` column containing either `control` or `drug`.

*** =instructions

First use a box plot to compare the weights grouped by treatment.

Tip: Remember to use the `~` symbol in your formula for the boxplot.
*** =hint
The `~` symbol means, 'is explained by' or 'described by'. So you want to plot `weight` described by `treatment`. You also need to tell boxplot that the data is stored in `data1`.
*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
```

*** =sample_code
```{r}
# Boxplot of weight grouped by treatment

```

*** =solution
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

```

*** =sct
```{r}
test_function("boxplot", args = c("formula", "data"))
```




--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:7706d7aba9
## Two sample t test (2)

Take a look at the boxplot (resize the panel if necessary).

Does it look like the drug-treated mice have lost weight compared to the control mice?
*** =instructions
- Yes
- No
*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
boxplot(weight ~ treatment, data = data1)
```

*** =sct
```{r}
test_mc(correct = 1)
```
--- type:NormalExercise lang:r xp:100 skills:1 key:1bb567adc1
## Two sample t test (3)

Since it looks like there's an effect, let's do a formal hypothesis test to quantify this.

*** =instructions
Perform a two sample t test to compare the weights grouped by treatment option.

*** =hint
Since you are entering the same data in `t.test()` and `boxplot()` you can use exactly the same formula.
*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
boxplot(weight ~ treatment, data = data1)
```

*** =sample_code
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

# t test of weight grouped by treatment


```

*** =solution
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

# t test of weight grouped by treatment
t.test(weight ~ treatment, data = data1)

```

*** =sct
```{r}
test_function("t.test", args = c("formula", "data"))
```




--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:e70c80f493
## Two sample t test (4)

Repeat the t test you just performed and look at the output.

(t test on `weight` grouped by `treatment` in `data1`)

This time with a threshold of $\alpha = 0.01$ do you reject the null hypothesis?

*** =instructions
- Yes
- No
*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
# boxplot(weight ~ treatment, data = data1)
```

*** =sct
```{r}
test_mc(correct = 2)
```



--- type:NormalExercise lang:r xp:100 skills:1 key:028ac3286c
## Dealing with variation between replicates

Statistics can be used to distinguish an effect which is masked by random variation - in other words, to detect a signal over the background noise.

The dataframe `data2`, contains the results of an siRNA knockdown experiment. In this experiment, a cell line was transfected with either an siRNA targetting a gene of interest (gene A) or control siRNA. The expression level of gene B was measured and is in the `output` column. 6 replicates were performed on different days. Take a look at the data to see if knocking down gene A has an effect on the expression level of gene B.

*** =instructions
Plot a boxplot for the `output` column grouped by `treatment` for the data in `data2`.
*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
```

*** =sample_code
```{r}
# Boxplot of output grouped by treatment

```

*** =solution
```{r}
# Boxplot of output grouped by day
boxplot(output ~ treatment, data = data2)

```

*** =sct
```{r}
test_function("boxplot", args = c("formula", "data"))
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:4fb9825166
## Dealing with variation between replicates (2)

Take a look at the boxplot you just plotted.

Does it look like the siRNA has an effect on expression of gene B?

*** =instructions
- Yes, a large effect
- Yes, a small but clear effect
- Possibly, a small effect
- No, no clear effect
*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
boxplot(output ~ treatment, data = data2)
```

*** =sct
```{r}
test_mc(correct = 3)
```



--- type:NormalExercise lang:r xp:100 skills:1 key:c1998ab6d2
## Dealing with variation between replicates (3)

It looks like there may be an effect, but the effect is small relative to the dispersion of the data.

Perform a two sample t test to determine the likelihood of observing a result like this if there were no effect.
*** =instructions
Perform a two sample t test on `output` grouped by `treatment` from `data2`.

Look at the output, and note down the *p value*.
*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
```

*** =sample_code
```{r}
# t test on output grouped by treatment

```

*** =solution
```{r}
# t test on output grouped by treatment
t.test(output ~ treatment, data = data2)

```

*** =sct
```{r}
test_function("t.test", args = c("formula", "data"))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:acf3acd269
## Dealing with variation between replicates (4)

With $\alpha = 0.05$ do you reject the null hypothesis?
*** =instructions
- Yes
- No
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
test_mc(correct = 2)
```

--- type:NormalExercise lang:r xp:100 skills:1 key:77c5375f09
## Looking at the data more closely

You failed to reject the null hypothesis, but let's take a closer look at the data.

The trouble with boxplots is that they don't show the individual data points. By looking at the raw data, you may see a pattern that isn't apparent from summary statistics.

You can use the `plot()` function to plot individual data points grouped by `day` to see how much variation there was between replicates. However, if the grouping variable is a factor, R will produce a box plot. If you tell it to treat `day` as a numeric variable using `as.numeric(day)`, it will plot a scatter plot.

*** =instructions
Plot a scatter plot of `output` grouped by `day` from `data2`
*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
```

*** =sample_code
```{r}
# Scatter plot of output grouped by day

```

*** =solution
```{r}
# Scatter plot of output grouped by day
plot(output ~ as.numeric(day), data = data2)
```

*** =sct
```{r}
test_function("plot", args = c("formula", "data"))
```



--- type:NormalExercise lang:r xp:100 skills:1 key:660cefb3bd
## Looking at the data (even) more closely

That's great, but it would be helpful to know which datapoint refers to which treatment.

You can easily do this by colouring the data points with the `col =` argument.


*** =instructions
Add in the `col = ` argument to colour the datapoints by `treatment`.
*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
```

*** =sample_code
```{r}
# Scatter plot of output grouped by day and coloured by treatment
plot(output ~ as.numeric(day), data = data2)
```

*** =solution
```{r}
# Scatter plot of output grouped by day and coloured by treatment
plot(output ~ as.numeric(day), data = data2, col = treatment)

```

*** =sct
```{r}
test_function("plot", args = c("formula", "data"))
# test_function("plot", args = "col")
test_error()
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:dee54eda39
## Dealing with variation between replicates (5)

Look at the scatter plot and interpret what the data show.

Note: Black = control and Red = siRNA

*** =instructions
- Output is consistently higher in siRNA group
- Output is consistently higher in control group
- No consistent difference between siRNA  control groups

*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))
# Scatter plot of output grouped by day and coloured by treatment
plot(output ~ as.numeric(day), data = data2, col = treatment)
```

*** =sct
```{r}
test_mc(correct = 1)
```


--- type:NormalExercise lang:r xp:100 skills:1 key:1dd88f988a
## Paired t test

Although the expression level in the control group varies considerably between replicates, the siRNA treatment appears to have a consistent effect on expression. The trouble with the two sample t test is that it compares the *mean* of each group. In this case, the variation between replicates swamps the siRNA effect.

So how can you analyse the data so that the consistent effect is detected over the variation between replicates?

The paired t test can help because, as the name suggests, it analyses the data in pairs. Try adding the argument `paired = True` to the t test to see how this affects the outcome.


*** =instructions
Perform a paired t test on `output` grouped by `treatment` in `data2`.
*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_2.RData"))

```

*** =sample_code
```{r}
# Paired t test on output grouped by treatment

```

*** =solution
```{r}
# Paired t test on output grouped by treatment
t.test(output ~ treatment, data = data2, paired = T)
```

*** =sct
```{r}
test_function("t.test", args = c("formula", "data", "paired"))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:869ab52c54
## Paired t test (2)

Once the background variation is controlled for, the siRNA effect now has $p < 0.00005$

For the paired t test to work in R, the data must be arranged in the same order in each group. In this case, both the control and siRNA data are sorted by day.

The paired t test can be used when observations in one group can be paired with observations in the other group. This may be because the observations were performed on the same subject (eg. mouse or patient), or because they were performed at the same time. There needs to be some reason why an observation in one group is more closely related to one particular observation, than the other observations in the second group.

Which of the following would not be suitable for analysis with a paired t test:
*** =instructions
- Does caffeine affect reaction time? Reaction times were measured in 20 students before and after taking caffeine.
- Does this cohort score higher marks than the last cohort? Exam scores from this year's cohort are compared to the same exam scores from last year's cohort.
- Is there a difference between steps recorded by smartphone apps or dedicated pedometers? Over a 24 hour period, 100 students recorded their steps on both a smartphone app and a pedometer device. The results from each device were compared.
- Have our students improved over the year? End of year exam scores of a cohort of 2nd year students were compared to their 1st year exam scores.

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
test_mc(correct = 2)
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:1a4c22d00a
## Assumptions of the t test (1)

Hypothesis tests are based on certain assumptions about the data. If the data do not fit these assumptions, the probability calculations underlying the test are likely to be incorrect. This could increase the chance of false positive or false negative results with potentially serious consequences.

So it is important to check the assumptions of any test you perform.

**Assumption 1: Continuous independent variable and bivariate dependent variable**

That's a bit of a mouthful, but it simply means that the outcome variable needs to be continuous, and the experimental variable needs to be categorical. Because the t test can only compare two groups, there can only have two levels for the dependent variable - that's what bivariate means. The underlying data may have more than two levels, but you can only analyse them two at a time with a t test.

Which of the following analyses fulfills this first assumption:
*** =instructions
- Testing whether the genotype of transgenic mice (homozygous, heterozygous or wild type for mutation A) affects the blood glucose level.
- Testing whether diet in mice (normal diet vs 'Western' diet) affects the time spent on running on an exercise wheel.
- Testing whether the number of eggs consumed in a month affects the blood cholesterol level.
- Testing whether the number of eggs consumed in a month affects the probability of suffering from myocardial infarction (heart attack).
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
test_mc(correct = 2)
```


--- type:NormalExercise lang:r xp:100 skills:1 key:cd73744d94
## Assumptions of the t test (2)

**Assumption 2: Normal distribution**

The t test assumes the underlying population has a normal distribution. Remember, that this refers to the population, rather than your sample. If your sample appears normally distributed, this is a good indication that the population is too.

The simplest way to assess normality, is to look at a histogram of the data.
*** =instructions
Draw a histogram of the `heights` data you used for the one sample t test.
*** =hint

*** =pre_exercise_code
```{r}
set.seed(967)
heights <- rnorm(n = 20, mean = 163.1548 + 4, sd = 6.5409)
```

*** =sample_code
```{r}
# Histogram of heights

```

*** =solution
```{r}
# Histogram of heights
hist(heights)
```

*** =sct
```{r}
test_function("hist", args = "x")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:e1591a53fc
## Assumptions of the t test (3)

As you can see, the data appear to follow a roughly normal distribution, with most values clustered around the mean and fairly symmetrical tails.

A normal quantile-quantile plot (Q-Q plot) is slightly more complicated but gives a clearer indication. This compares the quantiles (another name for percentiles) of your data with the theoretical quantiles from a normal distribution.

If that sounds like gobbledygook, don't worry. All you have to do, is see how well the data fall along a straight line.

*** =instructions
Use the `qqnorm()` and `qqline()` functions to test whether the `heights` data appear normally distributed.
*** =hint

*** =pre_exercise_code
```{r}
set.seed(967)
heights <- rnorm(n = 20, mean = 163.1548 + 4, sd = 6.5409)
hist(heights)
```

*** =sample_code
```{r}
# Normal Q-Q plot of heights


# Add line to Q-Q plot of heights

```

*** =solution
```{r}
# Normal Q-Q plot of heights
qqnorm(heights)

# Add line to Q-Q plot of heights
qqline(heights)

```

*** =sct
```{r}
test_function("qqnorm", args = "y")
test_function("qqline", args = "y")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:73bcc6232e
## Assumptions of the t test (4)

**Assumption 3: Equal variance**

The t test *usually* assumes that the two populations from which the samples have been taken have equal variance. In other words, the spread or dispersion of the values should be similar. You can check this by looking at the variance using summary statistics. (You could also check the standard deviation, since this is just the square root of the variance.)

*Actually* by default R uses the Welch's t test, which does not assume equal variance. If you are confident that the variance of your two samples are equal, you can specify this with argument `var.equal = TRUE`. This will increase the power of the test a little, but is most situations there's little advantage.
*** =instructions

*** =hint

*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_6314/datasets/STAT5_1.RData"))
# boxplot(weight ~ treatment, data = data1)
```

*** =sample_code
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

# t test of weight grouped by treatment - unequal variance test
t.test(weight ~ treatment, data = data1)

# t test of weight grouped by treatment - equal variance test

```

*** =solution
```{r}
# Boxplot of weight grouped by treatment
boxplot(weight ~ treatment, data = data1)

# t test of weight grouped by treatment - unequal variance test
t.test(weight ~ treatment, data = data1)

# t test of weight grouped by treatment - equal variance test
t.test(weight ~ treatment, data = data1)
```

*** =sct
```{r}

```
