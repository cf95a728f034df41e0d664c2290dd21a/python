# 装饰器，计算方法耗时

```python
import functools
from datetime import datetime


def elapsed(method):
    @functools.wraps(method)
    def _elapsed_seconds(*args, **kwargs):
        dt_begin = datetime.now()
       
        result = method(*args, **kwargs)
        
        print('{0} {1} {2}s elapsed. {0}'.format('-' * 20, repr(method), (datetime.now() - dt_begin).seconds))
        
        return result
        
    return _elapsed_seconds
```
