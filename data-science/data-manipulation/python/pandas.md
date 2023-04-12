
## `expand.grid` on pandas


```python
  
from itertools import product 

def expand_grid(dictionary): 
	return pd.DataFrame([row for row in product(*dictionary.values())], columns=dictionary.keys()) 

dictionary = {'color': ['red', 'green', 'blue'], 
			  'vehicle': ['car', 'van', 'truck'], 
			  'cylinders': [6, 8]}
```