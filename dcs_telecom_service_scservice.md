```python
# /home/capric/data/yqjr/Python/trunk/dcs/telecom/service/scservice.py
def get_basic_info(token):
	name = root.xpath('//div[@class="datacon"]//div[1]//span//text()')[0].encode('utf-8')

	create_datetime = time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time()))
	modify_datetime = time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time()))
```


```python
def get_basic_info(token):
	name = (root.xpath('//div[@class="datacon"]//div[1]//span//text()') or [''])[0].encode('utf-8')

	dt = datetime.now().strftime('%Y-%m-%d %H:%M:%S')
    	create_datetime = dt
	modify_datetime = dt
```



```python
def check_code(token,code,name,id_card):
	url = "http://sc.189.cn/service/billDetail/detailQuery.jsp?startTime="+startTime+"&endTime="+endTime+"&qryType=21&randomCode="+ code
```

```python
from urllib.parse import urlencode


def check_code(token,code,name,id_card):
	url = 'http://sc.189.cn/service/billDetail/detailQuery.jsp?' + \
        urlencode({
            'startTime': startTime,
            'endTime': endTime,
            'qryType': 21,
            'randomCode': code
        })
```
