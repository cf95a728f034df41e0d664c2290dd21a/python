```python
# /home/capric/data/yqjr/Python/trunk/dcs/jd/utils.py @line 83
def getYearList():
	thisYear= int(str(datetime.datetime.now())[0:4])
	list=[thisYear-1,thisYear-2,thisYear-3]
	return list
```


```python
# list(get_last_years())
def get_last_years(n=3):
    year = datetime.datetime.now().year
    for _ in range(n):
        year -= 1
        yield year
```

```python
# 也是可以通过yield重构的
def getMainUrlList():
	#今年订单url
	orderList=['http://order.jd.com/center/list.action?search=0&d=2&s=4096&t=']
	yearList=getYearList()
	#向前三年内的订单url
	for year in yearList:
		url='http://order.jd.com/center/list.action?search=0&d={0}&s=4096&t='.format(year)
		orderList.append(url)
	#添加三年前订单url
	# orderList.append('http://order.jd.com/center/list.action?search=0&d=3&s=4096&t=')
	return orderList
```
