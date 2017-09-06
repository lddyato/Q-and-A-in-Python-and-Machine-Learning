# Boxplots in matplotlib: Markers and outliers

```python
df.boxplot(x, notch=False, sym='r+', showmeans=True, vert=True, whis=1.5,positions=None, 
widths=None, patch_artist=False, bootstrap=None, usermedians=None, conf_intervals=None)
```
> whis : [ default 1.5 ]    
> Defines the length of the whiskers as a function of the inner quartile range. They extend to the most extreme data point within ( whis*(75%-25%) ) data range.

A picture is worth a thousand words. Note that the outliers (the + markers in your plot) are simply points outside of the wide [(Q1-1.5 IQR), (Q3+1.5 IQR)] margin below.

<img src="https://i.stack.imgur.com/ZN8N6.png" width=60%>

However, the picture is only an example for a normally distributed data set. It is important to understand that matplotlib does not estimate a normal distribution first and calculates the quartiles from the estimated distribution parameters as shown above.

Instead, the median and the quartiles are calculated directly from the data. Thus, your boxplot may look different depending on the distribution of your data and the size of the sample, e.g., asymmetric and with more or less outliers.

# Suppress Scientific Notation from Pandas Results

`pd.set_option('display.float_format', lambda x: '%.3f' % x)`

# select all the columns which dtypes='object'

* `df.select_dtypes(include=['object']).columns` returns the column names which dtype is object
* `df.select_dtypes(include=['object'])` returns the dataframe containing all the object-type columns
* `df.select_dtypes(exclude=['object']).columns` returns the column names which dtype is not object
