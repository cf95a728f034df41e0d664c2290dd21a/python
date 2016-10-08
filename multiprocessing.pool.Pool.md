# 使用进程池

[multiprocessing](https://docs.python.org/3/library/multiprocessing.html#using-a-pool-of-workers)

## map
```python
map(self, func, iterable, chunksize=None)
'''
Apply `func` to each element in `iterable`, collecting the results
in a list that is returned.
'''
```

```python
import time
from multiprocessing.pool import Pool as ProcessPool


class MyProcessPool1:
    def __init__(self, processes):
        self.processes = processes
    
    def _process(self, i):
        print('<{}>'.format(i))
        time.sleep(3)
        print('</{}>'.format(i))

    def start(self):
        process_pool = ProcessPool(processes=self.processes)
        process_pool.map(self._process, [i for i in range(self.processes * 3)])
        process_pool.close()
        process_pool.join()
    
    
@elapsed
def main():
    MyProcessPool1(10).start()
        

if __name__ == '__main__':
    main()
```

## starmap
```python
starmap(func, iterable, chunksize=None)
'''
Like `map()` method but the elements of the `iterable` are expected to
be iterables as well and will be unpacked as arguments. Hence
`func` and (a, b) becomes func(a, b).
'''
```

```python
import time
from multiprocessing.pool import Pool as ProcessPool


class MyProcessPool2:
    def __init__(self, processes):
        self.processes = processes
    
    def _process(self, i, j):
        print('<{},{}>'.format(i, j))
        time.sleep(3)
        print('</{},{}>'.format(i, j))

    def start(self):
        process_pool = ProcessPool(processes=self.processes)
        process_pool.starmap(
            self._process,
            zip([i for i in range(self.processes * 3)], [i ** 2 for i in range(self.processes * 3)])
        )
        process_pool.close()
        process_pool.join()
        

@elapsed
def main():
    MyProcessPool2(10).start()
    
    
if __name__ == '__main__':
    main()
```

## apply
```python
apply(self, func, args=(), kwds={}):
'''
Equivalent of `func(*args, **kwds)`.
'''
```


## 状态共享
[sharing-state-between-processes](https://docs.python.org/3/library/multiprocessing.html#sharing-state-between-processes)
### Value, Array
### Manager
### ctypes


## 状态同步
[synchronization-between-processes](https://docs.python.org/3/library/multiprocessing.html#synchronization-between-processes)
### Lock
### RLock
