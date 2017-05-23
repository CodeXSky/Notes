### Importing Excel Data Into Pandas
```python
import pandas as pd
xlFile = pd.ExcelFile('path/to/file.xlsx')
print (xlFile.sheet_names)
baseData = xlFile.parse('SheetName')
baseData.head()
```

### Description
* Basic description of a dataframe: `df.shape`
* Description of dataframe: `df.describe()`
* List column types: `df.dtypes`
* List unique values in a column: `df['columnName'].unique()`

### Group
* Group by a specific column and count: `df.groupby('columnName').count()`
* You can also group and then print the size of each group:
```python
grouped_df = df.groupby('columnName')
grouped_df.size()
```
* To group by multiple columns you can use the `pd.Grouper` function: `df.groupby([pd.Grouper(freq='MS', key='date'), 'column2']).count().unstack()`
* Here's the dictionary for the `frequency`:
  * `B`	business day frequency
  * `C`	custom business day frequency (experimental)
  * `D`	calendar day frequency
  * `W`	weekly frequency
  * `M`	month end frequency
  * `SM`	semi-month end frequency (15th and end of month)
  * `BM`	business month end frequency
  * `CBM`	custom business month end frequency
  * `MS`	month start frequency
  * `SMS`	semi-month start frequency (1st and 15th)
  * `BMS`	business month start frequency
  * `CBMS`	custom business month start frequency
  * `Q`	quarter end frequency
  * `BQ`	business quarter endfrequency
  * `QS`	quarter start frequency
  * `BQS`	business quarter start frequency
  * `A`	year end frequency
  * `BA`	business year end frequency
  * `AS`	year start frequency
  * `BAS`	business year start frequency
  * `BH`	business hour frequency
  * `H`	hourly frequency
  * `T, min`	minutely frequency
  * `S`	secondly frequency
  * `L, ms`	milliseconds
  * `U, us`	microseconds
  * `N`	nanoseconds

### Converting a column to date_time type
* The standard way of doing this is: `df['columnName'] = pd.to_datetime(df['columnName'], dayfirst=True)` (the `dayfirst=True` is for dates where the first item is the day, not the month). However, this one takes a long time.
* Here's a much much faster approach based on [this](https://stackoverflow.com/questions/29882573/pandas-slow-date-conversion) post:
```python
def lookup(s):
    """
    This is an extremely fast approach to datetime parsing.
    For large data, the same dates are often repeated. Rather than
    re-parse these, we store all unique dates, parse them, and
    use a lookup to convert all dates.
    """
    dates = {date:pd.to_datetime(date) for date in s.unique()}
    return s.map(dates)
# You use it like this:
df['date-column'] = lookup(df['date-column'])
```
* After this you can `resample` the data to aggregate it by month, day or year. For example:
```python
# First you need to make the date the index of the dataframe.
newDataframe = df.set_index('columnName')
# Then you can resample, 'M' is month, and we are resampling based on the count. 'A' is year.
newDataframe.resample('M').count()
```

### Plotting
* Looking at [this](http://pandas.pydata.org/pandas-docs/stable/visualization.html#visualization-barplot) and [this](http://pbpython.com/simple-graphing-pandas.html) very basic tutorials.
* Do this first to plot inline: `%matplotlib inline`
* For a simple bar chart: `my_plot = df.plot(kind='bar')` or `my_plot = df.plot.bar()` (this will plot every column in your dataset).
* For a one column plot do: `my_plot = df.plot.bar(y='columnName', legend=None)`
* For a line plot based on data (resampled (see above)): `timeLinePlot = df.resample('A').count().plot(y='columnName', legend=None)`

### Delete
* Delete column: `del df['columnName']`

### Sort
* Sort a dataframe based on values in a column: `df.sort_values('columnName', ascending=False)`

### Creating subset
* Create a dataframe based on values in a column: `subset_df = df.loc[df['columnName'] == value]`

### Rename
* Rename columns: `df.columns['newColumnNameA', 'newColumnNameB']`
* Replace values in a column: `baseData['columnName'] = baseData['columnName'].replace(['valueToReplaceA', 'valueToReplaceB'], ['newValueNameA', 'newValueNameB'])`
* Replace values in a column that contain: `baseData.loc[baseData['columnName'].str.contains('stringToReplace', case=False), 'columnName'] = 'newString'`

### Merge
* To merge two datasets based on a common value do: `merged_df = pd.merge(df_1, df_2, on='columnName')`
* If they have different column names then: `merge_df = pd.merge(df_1, df_2, left_on='columnName1', right_on='columnName2')`
* Or if one of the 'key' columns is the index then: `merge_df = pd.merge(df_1, df_2, left_index=True, right_on='columnName')`
* [Here](http://pandas.pydata.org/pandas-docs/stable/merging.html) is a good explanation to more methods.

### Pivot tables
* To create a pivot table use the following: `pivotTable_df = df.pivot_table(index='columnName', columns=[pd.Grouper(freq='A', key='dateColumName'), 'columnName'], values='columnName', aggfunc='function_count_or_sum_etc')`

### Export
* Export dataframe to csv: `baseData.to_csv('newFileName.csv')`
