Package for data procesing:
	-Read data sheet (Excel, CSV, ...)
	- Create and access a data
	- Select row and column
	- Make maths operations inside of the data
	- Make simple stadistics analitycs based on the data

# Functions
## DataFrame
	-  pd.DataFrame (df) -> Allow to create and handle files or arrays
	Ex:
```python
a= np.array([1,2,3])
b= np.array([-4,-5,-6])
c= pd.DataFrame({'Numeros Positivos':a,'Numeros Negativos':b})
->    Numeros Positivos  Numeros Negativos
   0         1                  -4
   1         2                  -5
   2         3                  -6
```

### ILOC

		* .iloc[ ]-> Return the info about the row and column, doens't get a specific or exact value
		Ex:
```python
df.iloc[1]
->    
	Numeros Positivos  2  
	Numeros Negativos -5
```
		Also this allow to put:
		['Name Col'],[:,2],[0:2,:]
### LOC

		* .loc[] -> Allow to make a specific search of values, that can work with column, row and conditions. This will return the exact number
```python
df.loc[,]   #[row(s),column(s)]
			#[0:2,'Name']
			#[df['Name']=='Name']
```

### TYPES

	- df.dtypes -> Show the kind of data of each column

### DESCRIBE

	-df.describe() -> Show the resume about the stadistics baesd. If we wish to show all include for string data:
```python
df.describe(include='all')   # all/object
```
		This options show the values as: 
			- unique: # of differents objects
			- top: Similar of Moda
			- Freq: Frequency of Moda(Top)

### INFO 

	- df.info() -> Show a summary pf the dtypes and values no-null

### REPLACE
	-df.replace(missing_value,new_value) -> This functions allow replace a value for other.

### DROPNA

	Delete the NaN values inside of the DF,this can be making with row, column.
```python
df.dropna(subset=[], #Name column if its for specific column/row
		  axis= , #0 - row, 1 - Column
		  inplace =	 #True/False 	  
		  )   
```
	Inplace save the changes in the original df

### RENAME

	Allow to make rename in the columns

```python
df.rename(columns={'old name':'new name'},inplace=True/False)
```

### ASTYPES

	Sometimes the kind of data doesn't recognized succesful. This method is used for change the dtype of the column

```python
df[" "].astype("int") # int/float/sting,...
```

### CUT

	Help to do segments and organized the data in ranges (Binning)

	First, its need to specific the range for make a proportional range/number

```python
bins = np.linspace(min(df[""]),max(df[""]),
				   # -> Number of ranges
				)
```

	Give names to the ranges

```python
names = ["Low","Medium","High"]
```

	Add new columns

```python
df["Bins"] = df.cut(df[""], #Column for make the classification
				   bins,  #Ranges
				   labels = names #Names
				   include_lowest=True
				   )
```

### GET DUMMIES (ONE-HOT-ENCODING)

	Convert categorical variable in numerical variable

```python
pd.get_dummies(df[""])
```

### VALUE COUNT

	Return the categorical and the count of everyone

```python
df[" "].value_count()
```

### GROUP BY

	Allow make a groups of values, generally categorical. This has a better vision of the data for make classication

```python
df.groupby([" "," "," "], # One or more categories
		  as_index=False # Do for no show the categories in columns or row without for columns
		  )
```

	This method allow to put more function 

### PIVOT

	It's similar to GROUPBY, however, this does a dynamic table of contingency between the index and the columns and in the middle can have the 3th variable as result. This allow to make a heatmap, because return a binaria table

```python
df.pivot(index='',columns='')
```

### CORR

	Determined the relation between the variables

```python
df.corr() 
```

### UNIQUE

	Return the variables in the column select in the DF
```python
df[" "].unique()
```

### FILLNA

	Replace the values NaN for the value that is assigned
```python
df.fillna(value)
df.fillna(
		  method='' # backfill/bfill/pad/ffill
					# /choice the value next to the Null/choice the value above of the Null
)
```