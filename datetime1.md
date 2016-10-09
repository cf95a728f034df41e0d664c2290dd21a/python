```python
# /home/capric/data/yqjr/Python/trunk/dcs/jd/utils.py @line 83
def getYearList():
	thisYear= int(str(datetime.datetime.now())[0:4])
	list=[thisYear-1,thisYear-2,thisYear-3]
	return list
```


```python
# [x for x in get_last_years()]
def get_last_years(n=3):
    year = datetime.datetime.now().year
    for _ in range(n):
        year -= 1
        yield year
```
