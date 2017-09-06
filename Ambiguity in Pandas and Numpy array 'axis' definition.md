# Ambiguity in Pandas Dataframe / Numpy Array “axis” definition

It's perhaps simplest to remember it as 0=down and 1=across.

This means:

* Use `axis=0` to apply a method down each column, or to the row labels (the index).
* Use `axis=1` to apply a method across each row, or to the column labels.

Here's a picture to show the parts of a DataFrame that each axis refers to:

![](https://i.stack.imgur.com/DL0iQ.jpg)

It's also useful to remember that Pandas follows NumPy's use of the word axis. The usage is explained in NumPy's glossary of terms:

> Axes are defined for arrays with more than one dimension. 
> A 2-dimensional array has two corresponding axes: the first running vertically downwards across rows (axis 0), 
> and the second running horizontally across columns (axis 1). 

So, concerning the method in the question, `df.mean(axis=1)`, seems to be correctly defined. 
It takes the mean of entries horizontally across columns, that is, along each individual row. 
On the other hand, df.mean(axis=0) would be an operation acting vertically downwards across rows.

Similarly, `df.drop(name, axis=1)` refers to an action on column labels, because they intuitively go across the horizontal axis. Specifying axis=0 would make the method act on rows instead.
