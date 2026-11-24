# Pandas Cheatsheet

```python
import pandas as pd
df=pd.read_csv("data.csv")
```

## Select
```python
df["col"]                 # column
df[["a","b"]]             # multiple columns
df.loc[0,"col"]           # by label
df.iloc[0,1]              # by position
df.head(); df.tail()
```

## Filter
```python
df[df["age"]>15]
df[(df["age"]>15)&(df["score"]>80)]
df[df["name"].isin(["A","B"])]
```
**Remember:** parentheses with `&` (AND), `|` (OR), `~` (NOT).

## Assign / Map
```python
df["new"]=df["score"]*2
df["col"].map(lambda x:x+1)
df["col"].apply(func)
```

## Summary
```python
df.describe()
df.shape; df.columns; df.dtypes
df["col"].mean(); df["col"].max(); df["col"].min()
df["col"].value_counts(); df["col"].unique()
```

## Group / Sort
```python
df.groupby("group")["value"].mean()
df.groupby("group")["value"].agg(["min","max","mean"])
df.sort_values("col",ascending=False)
```

## Missing values / Types
```python
df.isna().sum()
df.dropna()
df.fillna(0)
df["col"].astype("int")
```

## Combine / Rename
```python
pd.concat([df1,df2])
pd.merge(df1,df2,on="id",how="left")
df.rename(columns={"old":"new"})
```

## Reminders
- `Series` = one column; `DataFrame` = table.
- `.loc` = labels; `.iloc` = positions.
- `map()` transforms values in a Series.
- `groupby()` calculates per group.
- Most operations return a new object unless assigned.
