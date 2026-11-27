# Data Cleaning Cheatsheet (Python / Pandas)

## 1. Handling Missing Values
* **Check missing counts:** `df.isnull().sum()` returns a Series of missing values per column.
* **Calculate missing percentage:**
  ```python
  total_cells = np.product(df.shape)
  percent_missing = (df.isnull().sum().sum() / total_cells) * 100
  ```
* **Drop missing data:**
  * `df.dropna()` drops rows with any missing value (can lose too much data).
  * `df.dropna(axis=1)` drops columns with any missing value.
* **Fill missing data:**
  * `df.fillna(0)` replaces `NaN` with `0`.
  * `df.fillna(method='bfill', axis=0).fillna(0)` fills `NaN` with the value directly below it in the same column, then fills any remaining `NaN` with `0`.
* **Axes & Attributes:** `.shape` is an attribute (no `()`); `.sum()` is a method. In `(Rows, Columns)`, `axis=0` operates down rows (collapsing them into a per-column result), while `axis=1` operates across columns.

---

## 2. Scaling vs. Normalization
* **Scaling (Range):** Changes the numeric range (e.g., `0` to `1`) without changing the distribution shape.
  ```python
  scaled = minmax_scaling(data, columns=[0])
  ```
* **Normalization (Shape):** Reshapes skewed data into a bell-curve (normal) distribution.
  ```python
  normalized = stats.boxcox(data)  # Access transformed values via normalized[0]
  ```
* **Side-by-Side Plotting:**
  ```python
  fig, ax = plt.subplots(1, 2, figsize=(15, 3))
  sns.histplot(data, ax=ax[0], kde=True)
  ```

---

## 3. Parsing Dates
Convert date strings into `datetime` objects so Python recognizes their components:
* **Explicit format (faster):** `df['date_parsed'] = pd.to_datetime(df['date'], format="%m/%d/%y")`
* **Auto-detect format:** `df['date_parsed'] = pd.to_datetime(df['Date'], infer_datetime_format=True)`
* **Extract parts:** Use `.dt` accessors like `df['date_parsed'].dt.day`.

---

## 4. Character Encodings
* **UTF-8:** Standard Python text encoding.
* **Encode & Decode:**
  * `.encode("utf-8", errors="replace")` converts strings to raw bytes.
  * `.decode("utf-8")` converts bytes back to strings (must match the encoding used).
  * Converting to `ascii` with `errors="replace"` permanently destroys unsupported characters (like `€`).
* **Detect unknown file encoding:**
  ```python
  with open("file.csv", "rb") as f:
      print(charset_normalizer.detect(f.read(10000)))
  ```

---

## 5. Inconsistent Text Entry & Helpers
* **Inspect unique values:** `vals = df['Col'].unique()` (returns a 1D NumPy array; sort with `vals.sort()`).
* **Standardize strings:**
  * `df['Col'].str.lower()` converts to lowercase.
  * `df['Col'].str.strip()` removes leading/trailing whitespace.
  * `df['Col'].str.replace(old, new)` replaces substrings.
* **General Python syntax:**
  * `np.where(condition)` returns a tuple of index arrays `(row_indices, col_indices)` where the condition is `True`.
  * `isinstance(val, (type1, type2))` checks data types.
  * `obj.method()` calls a method on an object; `Class.attr` accesses a class attribute directly.
