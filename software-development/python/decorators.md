## singleton_function

Decorator to ensure a function behaves as a singleton.  
It will only execute once and cache the result; subsequent calls return the cached result.  

```python
import functools     
  
def singleton_function(fn):  
"""  
Decorator to ensure a function behaves as a singleton.  
It will only execute once and cache the result; subsequent calls return the cached result.  
"""  
cached_result = {}  
  
@functools.wraps(fn)  
def wrapper(*args, **kwargs):  
if wrapper not in cached_result:  
cached_result[wrapper] = fn(*args, **kwargs)  
return cached_result[wrapper]  
  
return wrapper  
  ```
## retry_with_backoff

A decorator for retrying a function with a specified number of retries and  
exponential backoff with random wait times between retries.  

```python
import functools  
import random  
import time

def retry_with_backoff(retry_count=10, initial_wait=30, max_wait=90):  
"""  
A decorator for retrying a function with a specified number of retries and  
exponential backoff with random wait times between retries.  
"""  
  
def decorator_retry(func):  
@functools.wraps(func)  
def wrapper(*args, **kwargs):  
retries_left = retry_count  
wait_time = initial_wait  
while retries_left > 0:  
try:  
return func(*args, **kwargs)  
except Exception as e:  
retries_left -= 1  
print(f"Error occurred: {e}")  
if retries_left > 0:  
sleep_time = random.randint(wait_time, max_wait)  
print(  
f"`{func.__name__}` - Retrying in {sleep_time} seconds... (Retries left: {retries_left})"  
)  
time.sleep(sleep_time)  
else:  
print(  
f"Maximum retries reached. Function failed. - `{func.__name__}`"  
)  
raise e  
  
return wrapper  
  
return decorator_retry
```
