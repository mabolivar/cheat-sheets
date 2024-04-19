## Mapper classes

```python
class BonusTemplateMapper(Enum):  
	NONE = None  
	DOUBLE_PEAK_TEMPLATE: AbstractBonusTemplate = DoublePeakBonusTemplate  
  
def instantiate(self, *args, **kwargs):  
	if self.value:  
		return self.value(*args, **kwargs)  
	return None
```
