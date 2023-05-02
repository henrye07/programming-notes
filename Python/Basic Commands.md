# Install libreries

```python
!pip install #Libreria
```
# Import Libreries
```python
import [library name] as [alias]
from [library name] import [specific method] # Import a specific method from a library
```

# Commun functions

```python
.format -> Allow replace space in the content inside. Example: 
name = 'Hola {}'
name.format('Name')
-> Hola Name

.strip -> Remove specific characteristies. Example:
txt = '..+.. Hola mundo '
txt.strip('.')
-> '+.. Hola mundo '

.round -> Redefine the number inside, reduce the digits. Example:
round([number],[number of digits])

.sorted -> Organized the array
sorted([0,1,2],reversed=True)
->2,1,0
```

# Module & Package

	For make use of a module outside of the folder or in another folder, we need to add the file __init__.py This allow to make the import from another folder

```
->Folder 1
	->__init__.py
	->file.py
->file2.py
```