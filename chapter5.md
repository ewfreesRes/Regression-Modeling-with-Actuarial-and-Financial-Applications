---
  title: "Chapter 5. Interpreting Regression Results"
  description: "An application, determining an individual's characteristics that influence its health expenditures, illustrates the regression modeling process from start to finish. Subsequently, the chapter summarizes what we learn from the modeling process, underscoring the importance of variable selection."

---
## Case study: MEPS health expenditures

```yaml
type: VideoExercise

xp: 50

key: 04ae7f9572



```

`@projector_key`
9f660c963794c20e534c811dcee7577e

---
## Summarizing data

```yaml
type: NormalExercise

xp: 100

key: 8b8b4db5e8



```

With a complex dataset, you will probably want to take a look at the structure of the data. You are already familiar with taking a *summary* of a dataset which provides summary statistics for many variables. You will see that several variables in this dataset are categorical, or factor, variables. We can use the `R` [table()](https://www.rdocumentation.org/packages/base/versions/3.5.0/topics/table) function to summarize them.

After getting a sense of the distributions of explanatory variables, we want to take a deeper dive into the distribution of the outcome variable, `expendop`. We will do this by comparing the histograms of the variable to that of its logarithmic version.

To examine relationships of the outcome variable visually, we look to scatterplots for continuous variables (such as `age`) and boxplots (such as `phstat`).

`@instructions`
- Examine the structure of the `meps` dataset using the [str()](https://www.rdocumentation.org/packages/utils/versions/3.5.0/topics/str/) function.
- Examine the distribution of the `race` variable using the [table()](https://www.rdocumentation.org/packages/base/versions/3.5.0/topics/table) function.
- Compare the expenditures distribution to its logarithmic version visually via histograms plotted next to another. `par(mfrow = c(1, 2))` is used to organize the plots you create.
- Examine the distribution of logarithmic expenditures in terms of levels of `phstat` visually using the 
[boxplot()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/boxplot/) function.
- Examine the relationship of age versus logarithmic expenditures using a scatter plot. Superimpose a local fitting line using the [lines()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/lines) and
[lowess()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/lowess) functions.

`@hint`









