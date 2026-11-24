# NumPy Quick Reference

``` python
import numpy as np
```

## 1. Array Basics

``` python
a = np.array([[1,2,3],[4,5,6]])

a.ndim    # dimensions
a.shape   # (rows,columns)
a.size    # total elements
a.dtype   # data type
```

  Shape       Meaning
  ----------- ---------------------------
  `(n,)`      1D
  `(r,c)`     2D: rows, columns
  `(d,r,c)`   3D: layers, rows, columns

## 2. Create Arrays

``` python
np.array(data)
np.zeros((r,c))
np.ones((r,c))
np.empty((r,c))          # uninitialized values
np.arange(start,stop,step)
np.linspace(start,stop,num) # num equally spaced values; endpoints included
```

## 3. Index, Slice & Filter

``` python
a[0]          # first item/row
a[-1]         # last
a[1:4]        # indices 1,2,3 (stop excluded)
a[::2]        # every 2nd
a[::-1]       # reverse
a[0,:]        # first row
a[:,1]        # second column
a[:2,:]       # first 2 rows
a[:,1:3]      # columns 1 and 2
```

Single integer index drops that dimension; slices preserve it (`a[0,:]`
vs `a[0:1,:]`).

### Boolean indexing

``` python
a[a<10]                   # values satisfying condition
a[(a>2)&(a<10)]            # AND
a[(a<3)|(a>10)]            # OR
a[~(a<5)]                  # NOT
a[a<5] = 0                 # conditional assignment
```

Use `&`, `|`, `~` instead of `and`, `or`, `not`; put each condition in
parentheses.

``` python
np.where(condition)                  # indices
np.where(condition,if_true,if_false) # conditional values
np.nonzero(condition)                # indices (tuple per axis)
```

## 4. Shape & Axis

``` python
a.reshape(2,3)
a.reshape(-1,2)       # infer one dimension
a.T                  # transpose (2D)
a.flatten()           # 1D copy
a.ravel()             # 1D view if possible
a[np.newaxis,:]       # add row dimension
a[:,np.newaxis]       # add column dimension
np.expand_dims(a,axis)
```

**Axis (2D):** `axis=0` operates down rows (column-wise); `axis=1`
across columns (row-wise). Reduction removes that axis from output.

``` python
np.sum(a,axis=0)  # column sums
np.sum(a,axis=1)  # row sums
```

For 3D: axis 0 = layers, 1 = rows, 2 = columns. `axis=-1` = last axis.

## 5. Combine / Split

``` python
np.concatenate((a,b),axis=0) # join along existing axis
np.vstack((a,b))             # add rows
np.hstack((a,b))             # add columns (2D)
np.vsplit(a,n)               # split rows
np.hsplit(a,n)               # split columns
```

Non-joining dimensions must match. Equal splits require divisibility;
`hsplit(a,(2,5))` uses split indices.

## 6. Views vs Copies

-   Basic slicing usually returns a **view**; changing it changes the
    original.
-   `.copy()` makes an independent copy.
-   Boolean/fancy indexing generally returns copies.
-   `.flatten()` always copies; `.ravel()`/`.reshape()` usually view if
    possible.

``` python
b = a[0:3].copy()  # safe independent array
```

## 7. Math & Broadcasting

Elementwise:

``` python
a+b
a-b
a*b
a/b
a**2
np.square(a)
np.sqrt(a)
```

Matrix multiplication: `a @ b` (inner dimensions must match).

**Broadcasting:** shapes match from right to left; each pair must be
equal or one must be 1 (missing dimensions act as 1).

Examples: `(3,4)+(4,)` works; `(3,4)+(3,)` fails.

## 8. Statistics & Useful Functions

``` python
np.sum(a)       # sum
np.prod(a)      # product
np.min(a)
np.max(a)
np.mean(a)
np.median(a)
np.std(a)
np.var(a)
np.argmax(a)    # index of max (flattened by default)
np.argmin(a)
np.any(a>0)     # any True?
np.all(a>0)     # all True?
np.count_nonzero(a)
```

## 9. Unique, Sort, Flip

``` python
np.sort(a,axis=-1)           # sort along last axis
np.unique(a)                 # unique values, sorted
np.unique(a,axis=0)          # unique rows
np.unique(a,axis=1)          # unique columns
np.unique(a,return_counts=True)
np.unique(a,return_index=True)

np.flip(a)                   # reverse all axes
np.flip(a,axis=0)             # reverse rows
np.flip(a,axis=1)             # reverse columns
```

## 10. Save / Load

``` python
np.save("a.npy",a)           # one array; preserves dtype/shape
np.load("a.npy")

np.savez("data.npz",a=a,b=b) # multiple arrays
data = np.load("data.npz")
data["a"]

np.savetxt("a.csv",a,delimiter=",")
np.loadtxt("a.csv",delimiter=",")
```

## 11. Pandas & Plotting

``` python
import pandas as pd
df = pd.DataFrame(a)
pd.read_csv("file.csv")
df.to_csv("file.csv",index=False)
df.head()
df.shape
df.describe()
```

``` python
import matplotlib.pyplot as plt
plt.plot(x,y)
plt.scatter(x,y)
plt.xlabel("x")
plt.ylabel("y")
plt.show()
```

## Common Reminders

-   Check `.shape` when an operation fails.
-   `np.empty()` contains uninitialized values.
-   `reshape` must preserve total `size`.
-   Use parentheses around Boolean conditions.
-   `axis=0` = down rows; `axis=1` = across columns (2D).
-   `*` is element-wise; `@` is matrix multiplication.
-   Use `.copy()` if you don't want to change the original through a
    view.
