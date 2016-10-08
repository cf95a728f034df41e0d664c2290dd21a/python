# 使用进程池

## 单个参数
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

## 多个参数
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