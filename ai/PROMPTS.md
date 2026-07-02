# AI Generation Prompts

This folder was built with Cursor. The prompts below are the user requests used to generate the notebooks here.

## Input data (not generated)

- `../data/iris.csv` — Fisher iris measurements by species
- `../data/wages.csv` — 1985 CPS wage determinants (534 workers)
- `../data/brain_size.csv` — brain size and IQ measures by gender

All analysis uses data from `assignment4/data` only. Files in `assignment4/manual` and other directories were not referenced.

---

## `stats_python.ipynb`

### Prompt 1: Notebook setup

> Make a python jupyter notebook in assignment4/ai that is setup for statistical analysis using scipy, pandas, statsmodels and seaborn. Do not ever reference the files in assignment4/manual. The data that will be analyzed is in assignment4/data. Do not reference files in any other directory.

**Generated:**

- `stats_python.ipynb` — imports, `DATA_DIR` config, loaders for iris, wages, and brain_size

---



### Prompt 2: Remove exploratory analysis

> Get rid of the exploratory analysis section and cells.

**Updated:** Removed preview/summary/plot/test cells; kept setup and data loaders only.

---



### Prompt 3: Brain size — groupby means

> First we will run analysis on the brain size data. Use groupby to split the dataframe and calculate the mean values using .mean()

**Added:** `## Brain size analysis` — `brain_size.groupby("Gender")[numeric_cols].mean()`

---



### Prompt 4: Brain size — box plots and summary stats

> Now add code to graph box plots by gender of fsiq, viq and piq. Then calculate the mean value of VIQ for the full population. Then calculate how many males and females were included in the study. Then calculate the average value of mri counts in log units for males and females

**Added:** Box plots for FSIQ/VIQ/PIQ by gender; population VIQ mean; gender counts; mean log(MRI_Count) by gender

---



### Prompt 5: Brain size — scatter matrices

> Now plot scatter matrix of weight, height and mri count

> Now plot scatter matrix of piq viq and fsiq

**Added:** Two `sns.pairplot` cells (body measures and IQ measures), both with `hue="Gender"`

---



### Prompt 6: Statistics section — hypothesis tests

> Start a new section of the notebook called statistics. Compute the 1 sample t test of viq being equal to 0

> Now conduct a wilcoxon test on viq vs 0

> Now compute a two sample t-test comparing female viq to male viq

> Now compute with mannwhitney test

> Now compute both an unpaired and paired t-test on fsiq vs piq

> Now plot a boxplot of the difference between fsiq and piq (fsiq-piq)

**Added:** `## Statistics` — one-sample t-test and Wilcoxon on VIQ; two-sample t-test and Mann-Whitney on VIQ by gender; unpaired/paired t-tests on FSIQ vs PIQ; boxplot of FSIQ − PIQ

---



### Prompt 7: Linear models — simulated data

> Now plan to create a new section called linear models. Generate simulated data using a seed value to get reproducible data with normal distributed noise. Create a dataframe with the generated x and y values and then plot the data. Then fit a statsmodels ols model to the generated data

> Add to notebook

**Added:** `## Linear models` — `np.random.default_rng(42)`, simulated `sim_data`, scatter plot, `smf.ols("y ~ x")`

---



### Prompt 8: Linear models — brain size OLS

> Now using the brain size data again, compare the VIQ of males and females using a old model

*(Clarified as OLS.)*

**Added:** `smf.ols("VIQ ~ C(Gender)", data=brain_size)`

---



### Prompt 9: Linear models — FSIQ vs PIQ long format

> Convert the fsiq and piq data in the brain sizes data to a long form data set with two columns- iq and type. Then fit an ols model to compare iq by type

**Added:** `pd.melt` to `iq_long`; `smf.ols("iq ~ C(type)", data=iq_long)`

---



### Prompt 10: Multiple regression — iris

> Start a new section of the notebook called multiple regression. Import the iris dataset and create a categories variable using pd.Categorical of the name column. Plot the scatter matrix of the data with the categories as c

> Now fit a linear model to sepal length as a function of name and petal length

> Now run an f-test to test if petal length is different between versicolor and virginica after removing effect of sepal width

> Write a vector of contrast to test the difference between the coefficient associated to versicolor and virginica in the linear model estimated above

**Added:** `## Multiple regression` — reload iris, `pd.Categorical`, pairplot by `categories`; `smf.ols("sepal_length ~ C(name) + petal_length")`; partial F-test via nested models; contrast vector `[0, 1, -1, 0]` on species coefficients

---



### Prompt 11: Wages section — load and visualize

> Now plan to import the wages data and assign the following column names: education south sex experience union wage age race occupation sector marr

> Now use the wages data and make a pairplot of the wage, age and education variables, with hue as sex

> Add kind=reg to the pairplot you just made

> Now make an lmplot with y=wage and x=education

> Add hue = sex to lmplot

**Added:** `## Wages` — reload wages; pairplots (`kind="reg"`) with and without `hue="sex"`; `sns.lmplot` of wage vs education by sex

---



### Prompt 12: Wages — loader and model updates

> Change the wages import function so that the sex column values are imported as strings not numbers

> Now fit an ols model to the wages data to determine how education and sex separately contribute to wage

> Change the wages import function to log10 transform the wage data when it is imported

**Updated:** `load_wages()` maps sex to `"Male"` / `"Female"` strings and applies `np.log10` to wage

**Added:** `smf.ols("wage ~ education + C(sex)", data=wages)`

---



### Prompt 13: Wages — interaction model

> Now formulate an ols model that tests whether wages increase more with education for males than females using an interaction

> Add in individual sex and education variables to the wage interaction model as well as the interaction term

**Added:** `smf.ols("wage ~ education + C(sex) + education:C(sex)", data=wages)`

---



### Prompt 14: Annotate notebook

> Add comments to explain the code and markdown cells to separate sections in the stats_python.ipynb notebook

**Updated:** `stats_python.ipynb` — added `## Setup` and subsection markdown headers (e.g. group means, hypothesis tests, simulated data, wage models); added brief explanatory comments in code cells; consolidated related cells and removed empty cells

---



## `stats_extension.ipynb`



### Prompt 15: Extension notebook plan

> In a new notebook called stats_extension.ipynb copy over the imports, wages file import function, and the wage model ols model code from the stats_python.ipynb notebook. Then write code to make a robust regression model of the same variables as the wage model

> Implement the plan as specified

**Generated:**

- `stats_extension.ipynb` — copied imports, `load_wages()`, OLS `wage ~ education + C(sex)`, robust `smf.rlm("wage ~ education + C(sex)")`

---



### Prompt 16: Compare OLS and RLM on one plot

> Now add code to graph both the ols and rlm models on the same plot

**Added:** Scatter of wage vs education by sex with solid OLS and dashed RLM fitted lines for each sex group

---

### Prompt 17: Annotate extension notebook

> Add comments to explain the code and markdown cells to separate sections in the stats_extension.ipynb notebook

**Updated:** `stats_extension.ipynb` — added `## Setup`, `## Load data`, and `## Compare OLS and RLM` section headers with subsections for OLS, RLM, and the overlay plot; added brief explanatory comments in code cells; removed empty trailing cell