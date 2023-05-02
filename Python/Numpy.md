It's used for numerical computation as:
	- Matriz handler (1D,2D,3D)
	- List compress
	- Data cleaning
	- Search elements
	- Read and rewrite file

# Functions

	-  np.array -> Allow to create a matriz with specific values
	Ex:
```python
array1= np.array([1,2,3,4])
print(array1)
-> 1,2,3,4
```
	-  np.arange -> Create a matriz with a start and end, with specific increment
	Ex:
```python
array1= np.arange(1,50,5) #(start,end,increment)
print(array1)
-> 1,6,11,16,21,26,31,36,41,46
```
	-  np.linspace -> Create a matriz with start and end, but a specific number of values
	Ex:
```python
array1= np.linspace(1,100,9) # (start,end,nume of data) --- increment is 1+8x=100
print(array1)
-> 1,13.375,25.75,38.125,50.5,...,100
```
	-  np.sort -> Organized the values in ascendent or decendent
	Ex:
```python
array1= np.array([10,4,9,3,7])
array2= np.sort(array1)
print(array2)
-> 3,4,7,9,10
```
	-  np.nan -> Created a "NaN" value
	Ex:
```python
array1= np.array([10,np.nan,9,3,np.nan])
print(array1)
-> 10,NaN,9,3,NaN
```
		* np.isnan -> Allow to know if the array contain -NaN-
		Ex
```python
np.isnan(array1).any()
-> True
```
		For remove a "NaN" value, we can use this:

```python
b = array1[~np.isnan(array1)]
-> 10,9,3
```
		For change a "NaN" value for other value:
```python
b=np.array(array1)
b[np.isnan(b)]=0 # We can put whatever value there
-> 10,0,9,3,0
```
	-  np.any -> Search the exist about a element in an array
	Ex:
```python
array1= np.array([20,15,41,30,23,70]) 
np.any(array1==23)
-> True
```
	-  np.where -> Know the position of a element
	Ex:
```python
np.where(array1==23)[0] # [row for search]
-> 4
```
		For change the values we need to use the 
			>,<,>=,<=,!=,== in the position/s
```python
c=np.array(array1)
c[np.where(c<23)]=1
-> 1 1 1 1 23 70
```
	-  np.shape -> Define the shape of the matriz (row, column)
	Ex:
```python
np.shape(array1)
-> (0,6)
```
	-  np.loadtxt -> Read a text file
	Ex:
```python
d= np.loadtxt(file) 
-> Array(...)
```