# 传统并发方式：多线程、多进程，线程池、进程池，map

```python
from datetime import datetime


def elapsed(method):
    def _elapsed_seconds(*args, **kwargs):
        dt_begin = datetime.now()
       
        result = method(*args, **kwargs)
        
        print('{0} {1} {2}s elaples. {0}'.format('-' * 20, repr(method), (datetime.now() - dt_begin).seconds))
        
        return result
        
    return _elapsed_seconds
```

## 1. 继承线程类
```python
import time
from threading import Thread

        
class MyThread(Thread):
    def __init__(self, i):
        Thread.__init__(self)
        self.i = i

    def run(self):
        self.task()
        
    def task(self):
        print('<{}>'.format(self.i))
        time.sleep(3)
        print('</{}>'.format(self.i))
        
@elapsed
def main():
    dt = datetime.now()
    
    # create
    threads = [MyThread(i) for i in range(10)]

    # start
    for t in threads:
        t.start()
    
    # wait
    for t in threads:
        t.join() 
        
  
  
if __name__ == '__main__':
    main()
```

## 2. 继承进程类
```python
import time
from multiprocessing import Process


class MyProcess(Process):
    def __init__(self, i):
        Process.__init__(self)
        self.i = i

    def run(self):
        self.task()
        
    def task(self):
        print('<{}>'.format(self.i))
        time.sleep(3)
        print('</{}>'.format(self.i))
        

@elapsed
def main():
    # create
    processes = [MyProcess(i) for i in range(10)]

    # start
    for p in processes:
        p.start()
    
    # wait
    for p in processes:
        p.join() 


if __name__ == '__main__':
    main()
```

## 3. 使用线程池
```python
import time
from multiprocessing.dummy import Pool as ThreadPool


class MyThreadPool:
    def __init__(self, threads):
        self.threads = threads
    
    def _thread(self, i):
        print('<{}>'.format(i))
        time.sleep(3)
        print('</{}>'.format(i))

    def start(self):
        threads_pool = ThreadPool(processes=self.threads)
        threads_pool.map(self._thread, [i for i in range(self.threads * 3)])
        threads_pool.close()
        threads_pool.join()
        
        
@elapsed
def main():
    MyThreadPool(10).start()
        

if __name__ == '__main__':
    main()
```

## 4. 使用进程池
### 4.1. 单个参数
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

### 4.2. 单个参数可用map简写
```python
import time


def f(i):
    time.sleep(1)
    return i * 2


@elapsed
def main():
    g = map(f, [i for i in range(10)])
    print(g)
    print(list(g))
    print(list(g))
    # next(g)
    
    
if __name__ == '__main__':
    main()
```

### 4.3. 多个参数
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

### 4.4. 多个参数可用itertools.starmap简写
```python
import time
import itertools


def f(i, j):
    time.sleep(1)
    return i, j


@elapsed
def main():
    g = itertools.starmap(
        f,
        zip([i for i in range(10)], [i ** 2 for i in range(10)])
    )
    print(g)
    print(list(g))
    print(list(g))
    # next(g)
    
    
if __name__ == '__main__':
    main()
```
