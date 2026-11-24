At the core of the NumPy package, is the ndarray object. This encapsulates n-dimensional arrays of homogeneous data types, with many operations being performed in compiled code for performance. 

NumPy arrays have a fixed size at creation, unlike Python lists (which can grow dynamically). Changing the size of an ndarray will create a new array and delete the original.

NumPy arrays facilitate advanced mathematical and other types of operations on large numbers of data. 

DATA MUST BE HOMOGENEOUS

* All elements of the array must be of the same type of data.  
* Once created, the total size of the array can’t change.  
* The shape must be “rectangular”, not “jagged”; e.g., each row of a two-dimensional array must have the same number of columns.

ndim-Dimensions  
a.shape-Exact shape of it  
a.size-Number of stuff in it  
a.dtype-Type of data in it  
`np.zeros()`, `np.ones()`, `np.empty()`, `np.arange()`, `np.linspace()`

* **1D Array — Shape: (columns,)**  
  * axis=0: **Horizontal** (across columns)  
* **2D Array — Shape: (rows, columns)**  
  * axis=0: **Vertical** (across rows)  
  * axis=1: **Horizontal** (across columns)  
* **3D Array — Shape: (depth, rows, columns)**  
  * axis=0: **Depth** (across blocks/layers)  
  * axis=1: **Vertical** (across rows)  
  * axis=2: **Horizontal** (across columns)

`np.sort()`, `np.concatenate()`  
arr.reshape()  
`np.newaxis`, `np.expand_dims`  
`Conditionals inside a[a<10]`  
`MUST USE & for and, | for or, ~ for not`  
`A[true]--all a[false]--None`  
`True means to output, false means to not.`   
`Vstack, Hstack`  
`Vsplit, Hsplit`  
Views–-Modifying view changes the original  
Use .copy to get make it safe from modifying original  
Eligible for all computations. Cell wise()  
np.Sum(list/array) either whole/from an axis  
Broadcasting-Scaler operation  
Sum, prod, min, max, mean(available- axiswise)  
Integer slicing such as data\[0,:\]drops the dimension  
Remember to use .copy() to not change the original: either view or pointing to the storage  
\-RULES: Operations: 1\. Same dimensions–YES 2\. ROW/COLUMN matching to dimension-YES 3\. smaller/multiple rows \-NO 4\. Scaler-YES, to Each element 5.\[1\]or\[\[1\]\]--Yes, COunts as Scaler  
Unique: can choose which way: lets say 2d: axis=1–going horizontally-changing length of horizontal axis-deleting identical columns-no identical columns(analogous for axis=0/more dimensions)  
`arr.reshape()`, `arr.transpose()`, `arr.T`  
`Transpose: from r1 to c1`  
`np.flip()--Flatten it into 1d, reverse all numbers, rearrange it`  
`np.flatten() flatten to 1d`  
`np.ravel() flatten to 1d, but it’s a view`  
`Square–np.square`  
`np.save`, `np.savez`, `np.savetxt`, `np.load`, `np.loadtxt`  
`Save for single array-.npy`  
`Savez for multiple-. Npz`  
`Savetxt for readable- .csv/.txt`  
`Pandas: read_csv, DataFrame…`  
