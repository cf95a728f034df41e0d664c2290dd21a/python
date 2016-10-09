```python
import threading
def background(func):
    def run(*args, **kwargs):
        threading.Thread(target=func, args=args, kwargs=kwargs).start()
    return run
```



```python
import threading
import functools


def thread(method):
    @functools.wraps(method)
    def _thread(*args, **kwargs):
        threading.Thread(target=method, args=args, kwargs=kwargs).start()
    return _thread
```
