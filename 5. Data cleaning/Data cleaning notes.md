*\# get the number of missing data points per column*  
missing\_values\_count \= nfl\_data.isnull().sum()  
*\# look at the \# of missing points in the first ten columns*  
Missing\_values\_count\[0:10\]  
Returns a series with index of column names  
*\# how many total missing values do we have?*

total\_cells \= np.product(nfl\_data.shape)  
total\_missing \= missing\_values\_count.sum()  
*\# percent of data that is missing*  
percent\_missing \= (total\_missing/total\_cells) \* 100  
print(percent\_missing)

\#different reasons of missing values: examples: Not recorded, being 0, doesn't exist… for each we have different strategies to deal with them

*\# remove all the rows that contain a missing value*  
nfl\_data.dropna()  
\#bad because it removes a lot of important info. Maybe useful depending on situation

\# remove all columns with at least one missing valuecolumns\_with\_na\_dropped \= nfl\_data.dropna(axis=1)  
columns\_with\_na\_dropped.head()  
\#axis=1:dropping along horizontal axis:changing length of horizontal :changing number of columns.

*\# get a small subset of the NFL dataset*  
subset\_nfl\_data \= nfl\_data.loc\[:, 'EPA':'Season'\].head()  
subset\_nfl\_data  
Using the first 5 of all rows, and columns of only epa to season

*\# replace all NA's with 0*  
subset\_nfl\_data.fillna(0)  
\#automatically fill all nas with 0

*\# replace all NA's the value that comes directly after it in the same column,*   
*\# then replace all the remaining na's with 0*  
subset\_nfl\_data.fillna(method\='bfill', axis\=0).fillna(0)  
\#doing backfill on axis 0: changing R in (R,C)  
\#meaning looking under the next row, which is the same column

\#Shape is an attribute, while sum is a function

General rule for AXIS: axis \= 0; then in (R,C), R is the one being operated.  
Say sum(axis=0), then it becomes a series with(C)

in **scaling**, you're changing the *range* of your data, while 

in **normalization**, you're changing the *shape of the distribution* of your data.

Scaling: on a scale of 0-100 or 0-1. Each varying of “1” is the same across all data

*\# generate 1000 data points randomly drawn from an exponential distribution*  
original\_data \= np.random.exponential(size\=1000)  
*\# mix-max scale the data between 0 and 1*  
scaled\_data \= minmax\_scaling(original\_data, columns\=\[0\])  
Columns is the index of columns we want to scale  
*\# plot both together to compare*  
fig, ax \= plt.subplots(1, 2, figsize\=(15, 3))  
\# Make 1 row of 2 side by side figures  
sns.histplot(original\_data, ax\=ax\[0\], kde\=True, legend\=False)  
ax\[0\].set\_title("Original Data")  
sns.histplot(scaled\_data, ax\=ax\[1\], kde\=True, legend\=False)  
ax\[1\].set\_title("Scaled data")  
plt.show()

normalized\_data \= stats.boxcox(original\_data)  
*\# plot both together to compare*  
fig, ax\=plt.subplots(1, 2, figsize\=(15, 3))  
sns.histplot(original\_data, ax\=ax\[0\], kde\=True, legend\=False)  
ax\[0\].set\_title("Original Data")  
sns.histplot(normalized\_data\[0\], ax\=ax\[1\], kde\=True, legend\=False)  
\# the \[0\] is required. Normalized data have 2, which the boxcox function return  
ax\[1\].set\_title("Normalized data")  
plt.show()

Now that we know that our date column isn't being recognized as a date, it's time to convert it so that it is recognized as a date. This is called "parsing dates" because we're taking in a string and identifying its component parts.

*\# create a new column, date\_parsed, with the parsed dates*  
landslides\['date\_parsed'\] \= pd.to\_datetime(landslides\['date'\], format\="%m/**%d**/%y")

landslides\['date\_parsed'\] \= pd.to\_datetime(landslides\['Date'\], infer\_datetime\_format=True)  
\#also available: inferring

*\# get the day of the month from the date\_parsed column*  
day\_of\_month\_landslides \= landslides\['date\_parsed'\].dt.day  
day\_of\_month\_landslides.head()

np.where(condition) returns a tuple of NumPy arrays (ndarray) storing the index locations where condition is True—one array per dimension.  
np.where(true): (x loc, y loc)  
xloc=\[x1,x2,x3,.....\]  
yloc=\[y1,y2,y3…\]  
Each x1y1….in the original thing satisfies the condition

Encoding stuff to make them a string of binary digit. UTF-8: standard encoding for python.  
*\# encode it to a different encoding, replacing characters that raise errors*  
after \= before.encode("utf-8", errors\="replace")  
*\# check the type*  
type(after)  
print(after.decode("utf-8"))  
Decode can only decode it using the same way that it’s encoded

*\# start with a string*  
before \= "This is the euro symbol: €"

*\# encode it to a different encoding, replacing characters that raise errors*  
after \= before.encode("ascii", errors \= "replace")  
*\# convert it back to utf-8*  
print(after.decode("ascii"))  
*\# We've lost the original underlying byte string\! It's been*   
*\# replaced with the underlying byte string for the unknown character :(*  
*Converting it automatically loose all data that can’t be handled*  
*\# look at the first ten thousand bytes to guess the character encoding*  
with open("../input/kickstarter-projects/ks-projects-201801.csv", 'rb') as rawdata:  
    result \= charset\_normalizer.detect(rawdata.read(10000))  
*\# check what the character encoding might be*  
print(result)

*\# get all the unique values in the 'Country' column*  
countries \= professors\['Country'\].unique()  
*\# sort them alphabetically and then take a closer look*  
countries.sort()  
Countries  
.unique returns a 1d numpy array

*\# convert to lower case*  
professors\['Country'\] \= professors\['Country'\].str.lower()  
*\# remove trailing white spaces*  
professors\['Country'\] \= professors\['Country'\].str.strip()  
str.Lower(): convert to lower  
str.Strip(): strip all leading/trailing stuff of the string(if there are)  
str.replace(old, new)  
isinstance(value,(type1,type2….))

class.function(data)/data.function()  
Class.thing for directly accessing stuff

Yes, pandas DataFrames and Series automatically ignore NaN values by default in almost all statistical methods (max(), min(), mean(), median(), sum(), std(), count(), mode(), idxmax(), idxmin()).

Cross-Library NaN Cheat Sheet

| Library / Context | Ignores NaN by Default | Does NOT Ignore NaN (Propagates or Crashes) | How to Ignore NaN |
| ----- | ----- | ----- | ----- |
| **Pandas Aggregations** | .mean(), .sum(), .min(), .max(), .median(), .std(), .count(), .mode(), .value\_counts(), .groupby() | .sum() on an *all-NaN* column returns 0.0 | Already ignores (skipna=True / dropna=True) |
| **Pandas Element-Wise** | .fillna(), .isna(), .notna() | \+, \-, \*, /, \==, \!=, \>, \<, .strmethods | Use .add(other, fill\_value=0) or .str.contains(..., na=False) |
| **NumPy (np)** | *None* (standard NumPy never ignores NaN by default) | np.mean(), np.sum(), np.min(), np.max(), np.median(), np.std(), \+, \- | Use np.nanmean(), np.nansum(), np.nanmin(), np.nanmax(), np.nanmedian() |
| **Built-in Python & statistics** | None (no built-in NaN skipping) | sum(), statistics.mean(), statistics.median() return nan; min()/max() give unpredictable results | Filter first: \[x for x in lst if not math.isnan(x)\] |
| **Plotting (sns/ plt)** | sns.lineplot(), sns.scatterplot(), sns.barplot(), sns.heatmap()(leaves blank gaps or skips missing points) | plt.plot() breaks the line into disconnected segments at NaNs | Drop/interpolate NaNs first if you want a continuous line |

