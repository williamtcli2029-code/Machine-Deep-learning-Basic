# Pandas + Seaborn Quick Cheatsheet

## Load and inspect data

``` python
import pandas as pd

df = pd.read_csv("file.csv", index_col="Date", parse_dates=True)
df.head(n)       # first n rows (default 5)
df.tail(n)       # last n rows
df.shape         # (rows, columns)
df.columns       # column names
```

-   `index_col` makes a column the DataFrame index.
-   `parse_dates=True` parses the index column as dates.

## Select data

``` python
df["col"]              # one column -> Series
df[["a", "b"]]         # multiple columns -> DataFrame
df.loc["row"]          # select by index label -> usually Series
df.index               # index values
```

Use `df.index` when you need the index as an x- or y-value.

## Plot setup

``` python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(14, 6))
plt.title("Chart title")
sns.set_style("whitegrid")
```

-   `plt.figure()` creates a new figure.
-   Seaborn (`sns`) draws the statistical plot; Matplotlib (`plt`)
    controls the figure, labels, and display.
-   Styles: `"darkgrid"`, `"whitegrid"`, `"dark"`, `"white"`, `"ticks"`.

## Common Seaborn plots

``` python
sns.lineplot(data=df)                         # trends over time
sns.lineplot(data=df["col"], label="Name")    # one series
sns.barplot(x=df.index, y=df["col"])          # category averages
sns.heatmap(data=df, annot=True)              # matrix; show cell values
sns.scatterplot(x=df["a"], y=df["b"])         # relationship
sns.regplot(x=df["a"], y=df["b"])             # scatter + regression line
sns.lmplot(x="a", y="b", hue="group", data=df) # regression by group
sns.swarmplot(x="group", y="value", data=df)  # separated individual points
sns.histplot(data=df, x="col")                # frequency distribution
sns.kdeplot(data=df, x="col", fill=True)      # smoothed density
sns.jointplot(x=df["a"], y=df["b"], kind="kde") # 2D density + marginals
```

-   `hue` colors/separates data by a categorical variable.
    `scatterplot`, `swarmplot`, `kdeplot`, `histplot`, and `lmplot`
    support it; `regplot` does not.
-   `barplot` needs `x` and `y`; by default it shows an estimate (mean)
    for each category.
-   `heatmap(annot=True)` writes values in the cells.
-   KDE is a smoothed density estimate; its total area is 1.

## Choosing a plot

  Goal                                         Plot
  -------------------------------------------- ----------------------
  Trend over time                              `lineplot`
  Frequency / distribution                     `histplot`
  Smoothed distribution                        `kdeplot`
  Relationship between two numeric variables   `scatterplot`
  Relationship + fitted line                   `regplot` / `lmplot`
  Compare category averages                    `barplot`
  Values in a matrix                           `heatmap`
  Show individual observations by category     `swarmplot`

## Missing values (NaN)

-   Most Pandas aggregations skip missing values by default: `mean`,
    `median`, `min`, `max`, `sum`, `std`, `count`.
-   Use `df.isna()` / `df.notna()` to find missing values and
    `df.dropna()` or `df.fillna(value)` to handle them.
-   NumPy functions such as `np.mean()` propagate NaN; use
    `np.nanmean()` to skip them.
-   Seaborn generally omits missing observations; Matplotlib line plots
    show gaps where values are NaN.

## Notebook setup

``` python
import pandas as pd
pd.plotting.register_matplotlib_converters()
import matplotlib.pyplot as plt
import seaborn as sns

# In Jupyter:
%matplotlib inline
```
