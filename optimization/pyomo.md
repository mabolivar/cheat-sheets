## Inspect constraints

```python
from pyomo.core.base.constraint import Constraint, ConstraintList, ScalarConstraint  
sorted(
	   sum(
		   [
			   [str(c.expr) for c in con.itervalues()] 
			   if isinstance(con, ConstraintList) 
			   else [str(con.expr)]  
			   for con in 
			   model.component_map(Constraint).itervalues()
		   ], 
		   []
		)
)
```
