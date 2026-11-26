fifa\_data \= pd.read\_csv(fifa\_filepath, index\_col\="Date", parse\_dates\=True)  
Using index\_col to specify index

df.head(x) (tail is last x rows)first x lines

import matplotlib.pyplot as plt  
*\# Set the width and height of the figure*  
plt.figure(figsize\=(16,6))  
*\# Line chart showing how FIFA rankings evolved over time*   
sns.lineplot(data\=fifa\_data)  
\#sns:seaborn. Gets directly a dataframe  
\#In the course, all code will start with sns except figure(creating the original frame)  
We use plt because Seaborn is only a styling and statistical wrapper, whereas Matplotlib (plt) is the underlying engine that actually owns the figure window, axes, and display lifecycle.

*\# Set the width and height of the figure*  
plt.figure(figsize\=(14,6))  
*\# Add title*  
plt.title("Daily Global Streams of Popular Songs in 2017-2018")  
*\# Line chart showing daily global streams of each song*   
sns.lineplot(data\=spotify\_data)

\#Seaborn is only for plotting actual data / creating the actual graph.  
every plt.figure() creates a brand-new, empty figure canvas and sets it as the active target for all subsequent plt and sns commands.

*\# Set the width and height of the figure*  
plt.figure(figsize\=(14,6))  
*\# Add title*  
plt.title("Daily Global Streams of Popular Songs in 2017-2018")  
*\# Line chart showing daily global streams of 'Shape of You'*  
sns.lineplot(data\=spotify\_data\['Shape of You'\], label\="Shape of You")  
*\# Line chart showing daily global streams of 'Despacito'*  
\*\*sns.lineplot(data\=spotify\_data\['Despacito'\], label\="Despacito")  
*\# Add label for horizontal axis*  
plt.xlabel("Date")  
Double brackets for selecting particular columns:\[\[“a”,”b”\]\]

*\# Set the width and height of the figure*  
plt.figure(figsize\=(10,6))  
*\# Add title*  
plt.title("Average Arrival Delay for Spirit Airlines Flights, by Month")  
*\# Bar chart showing average arrival delay for Spirit Airlines flights by month*  
\*\*sns.barplot(x\=flight\_data.index, y\=flight\_data\['NK'\])  
*\# Add label for vertical axis*  
plt.ylabel("Arrival delay (in minutes)")  
Bar requires a x and y  
MUST USE .index for index if we want to use it as x/y on bar chart or just simply referring to it

*\# Set the width and height of the figure*  
plt.figure(figsize\=(14,7))  
*\# Add title*  
plt.title("Average Arrival Delay for Each Airline, by Month")  
*\# Heatmap showing average arrival delay for each airline by month*  
\*\*sns.heatmap(data\=flight\_data, annot\=True)  
*\# Add label for horizontal axis*  
plt.xlabel("Airline")

annot=True \- This ensures that the values for each cell appear on the chart. (*Leaving this out removes the numbers from each of the cells\!*) if it’s false, heatmap only show colors

Doing df\[col\] or df.loc\[row\] first one converts to a series with name col and index of original index. Second one converts to a series with the name of the row index and index of column name

\*\*sns.scatterplot(x\=insurance\_data\['bmi'\], y\=insurance\_data\['charges'\])  
Similar to barplot..

\*\*sns.regplot(x\=insurance\_data\['bmi'\], y\=insurance\_data\['charges'\])  
Adding a regression line  
No for hue

\*\*sns.scatterplot(x\=insurance\_data\['bmi'\], y\=insurance\_data\['charges'\], hue\=insurance\_data\['smoker'\])  
Yes for hue

\*\*sns.lmplot(x\="bmi", y\="charges", hue\="smoker", data\=insurance\_data)  
Designed to pass data into it and look over the values  
Yes for hue

Hue: separation. Only 1 hue per graph

sns.swarmplot(x\=insurance\_data\['smoker'\],  
              y\=insurance\_data\['charges'\])  
Separates by values of smoker. Clear separation

\*\*sns.swarmplot(data=insurance\_data, x="smoker", y="charges", hue="sex")  
it comes to 2 pile of smoker/nonsmoker with their charges colored based on sex

\*\*sns.histplot(data=iris\_data\['Petal Length (cm)'\])  
Data range and its frequency  
sns.kdeplot(data\=iris\_data\['Petal Length (cm)'\], shade\=True)  
Smoothed hist plot (density graph so it’s from 0-1, with area of 1\)  
sns.jointplot(x\=iris\_data\['Petal Length (cm)'\], y\=iris\_data\['Sepal Width (cm)'\], kind\="kde")  
Join 2 2dkeds, forms a plot that should be 3d. Shows which combos are the most likely

*\# Histograms for each species*  
sns.histplot(data\=iris\_data, x\='Petal Length (cm)', hue\='Species')  
*\# Add title*  
plt.title("Histogram of Petal Lengths, by Species")  
Sorting by species

*\# KDE plots for each species*  
sns.kdeplot(data\=iris\_data, x\='Petal Length (cm)', hue\='Species', shade\=True)  
*\# Add title*  
plt.title("Distribution of Petal Lengths, by Species")

When to use which model?  
\-Trends(over time):lineplot  
\-Distribution(frequency):histogram, kdeplot  
\-Relationship: Barplot, Heatmap, sactter, swarm, regline, lmplot

sns.set\_style("dark")--Setting style…not very useful

Seaborn has five different themes: (1)"darkgrid", (2)"whitegrid", (3)"dark", (4)"white", and (5)"ticks", and you need only use a command similar to the one in the code cell above (with the chosen theme filled in) to change it.

 

pd.DataFrame(data=None, index=None, columns=None, dtype=None, copy=None)  
Yes, pandas DataFrames and Series automatically ignore NaN values by default in almost all statistical methods (max(), min(), mean(), median(), sum(), std(), count(), mode(), idxmax(), idxmin()).

Cross-Library NaN Cheat Sheet

| Library / Context | Ignores NaN by Default | Does NOT Ignore NaN (Propagates or Crashes) | How to Ignore NaN |
| ----- | ----- | ----- | ----- |
| **Pandas Aggregations** | .mean(), .sum(), .min(), .max(), .median(), .std(), .count(), .mode(), .value\_counts(), .groupby() | .sum() on an *all-NaN* column returns 0.0 | Already ignores (skipna=True / dropna=True) |
| **Pandas Element-Wise** | .fillna(), .isna(), .notna() | \+, \-, \*, /, \==, \!=, \>, \<, .strmethods | Use .add(other, fill\_value=0) or .str.contains(..., na=False) |
| **NumPy (np)** | *None* (standard NumPy never ignores NaN by default) | np.mean(), np.sum(), np.min(), np.max(), np.median(), np.std(), \+, \- | Use np.nanmean(), np.nansum(), np.nanmin(), np.nanmax(), np.nanmedian() |
| **Built-in Python & statistics** | None (no built-in NaN skipping) | sum(), statistics.mean(), statistics.median() return nan; min()/max() give unpredictable results | Filter first: \[x for x in lst if not math.isnan(x)\] |
| **Plotting (sns/ plt)** | sns.lineplot(), sns.scatterplot(), sns.barplot(), sns.heatmap()(leaves blank gaps or skips missing points) | plt.plot() breaks the line into disconnected segments at NaNs | Drop/interpolate NaNs first if you want a continuous line |

import pandas as pd  
pd.plotting.register\_matplotlib\_converters()  
import matplotlib.pyplot as plt  
%matplotlib inline  
import seaborn as sns  
print("Setup Complete")  
Setups..

