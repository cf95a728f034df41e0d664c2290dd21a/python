# 继承进程类

[multiprocessing](https://docs.python.org/3/library/multiprocessing.html)

[list-comprehensions](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions)

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
