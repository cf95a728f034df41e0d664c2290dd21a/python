# from threading import Thread
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
        

if __name__ == '__main__':
    # create
    threads = [MyThread(i) for i in range(10)]

    # start
    for t in threads:
        t.start()
    
    # wait
    for t in threads:
        t.join() 
```

# from multiprocessing import Process
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
        

if __name__ == '__main__':
    # create
    processes = [MyProcess(i) for i in range(10)]

    # start
    for p in processes:
        p.start()
    
    # wait
    for p in processes:
        p.join() 
```

# from multiprocessing.dummy import Pool as ThreadPool
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
        

if __name__ == '__main__':
    MyThreadPool(10).start()
```

# from multiprocessing.pool import Pool as ProcessPool
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
        

if __name__ == '__main__':
    MyProcessPool1(10).start()
```

```python
import time


def f(i):
    time.sleep(1)
    return i * 2


if __name__ == '__main__':
    g = map(f, [i for i in range(10)])
    print(g)
    print(list(g))
    print(list(g))
    next(g)
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
        

if __name__ == '__main__':
    MyProcessPool2(10).start()
```


```python
import time
import itertools


def f(i, j):
    time.sleep(1)
    return i, j


if __name__ == '__main__':
    g = itertools.starmap(
        f,
        zip([i for i in range(10)], [i ** 2 for i in range(10)])
    )
    print(g)
    print(list(g))
    print(list(g))
    next(g)
```
