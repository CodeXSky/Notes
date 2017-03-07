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

### Group
* Group by a specific column and count: `df.groupby('columnName').count()`
* You can also group and then print the size of each group:
```python
grouped_df = df.groupby('columnName')
grouped_df.size()
```

### Plotting
* Looking at [this](http://pandas.pydata.org/pandas-docs/stable/visualization.html#visualization-barplot) and [this](http://pbpython.com/simple-graphing-pandas.html) very basic tutorials.
* Do this first to plot inline: `%matplotlib inline`
* For a simple bar chart: `my_plot = df.plot(kind='bar')` or `my_plot = df.plot.bar()` (this will plot every column in your dataset).
* For a one column plot do: `my_plot = df.plot.bar(y='columnName', legend=None)`

### Delete
* Delete column: `del df['columnName']`

### List
* List unique values in a column: `df['columnName'].unique()`

### Sort
* Sort a dataframe based on values in a column: `df.sort_values('columnName', ascending=False)`

### Rename
* Rename columns: `df.columns['newColumnNameA', 'newColumnNameB']`
* Replace values in a column: `baseData['columnName'] = baseData['columnName'].replace(['valueToReplaceA', 'valueToReplaceB'], ['newValueNameA', 'newValueNameB'])`
* Replace values in a column that contain: `baseData.loc[baseData['columnName'].str.contains('stringToReplace', case=False), 'columnName'] = 'newString'`

### Export
* Export dataframe to csv: `baseData.to_csv('newFileName.csv')`
