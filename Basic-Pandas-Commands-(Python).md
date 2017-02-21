### Importing Excel Data Into Pandas
```python
import pandas as pd
xlFile = pd.ExcelFile('path/to/file.xlsx')
print (xlFile.sheet_names)
baseData = xlFile.parse('SheetName')
baseData.head()
```

### Other
* Group by a specific column and count: `df.groupby('columnName').count()`
* Delete column: `del df['columnName']`
* List unique values in a column: `df.['columnName'].unique()`
* Rename columns: `df.columns['newColumnNameA', 'newColumnNameB']`
* Replace values in a column: `baseData['columnName'] = baseData['columnName'].replace(['valueToReplaceA', 'valueToReplaceB'], ['newValueNameA', 'newValueNameB'])`
* Replace values in a column that contain: `baseData.loc[baseData['columnName'].str.contains('stringToReplace', case=False), 'columnName'] = 'newString'`
* Export dataframe to csv: `baseData.to_csv('newFileName.csv')`
