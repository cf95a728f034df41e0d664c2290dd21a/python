```python
# /home/capric/data/yqjr/Python/trunk/dcs/telecom/service/cqservice.py

def fetch_each_bill(cookies, setup):

                items = {}
                items['user'] = user
                items['host_phone'] = phone
                items['call_len'] = row.get(u'通话时长（秒）', '')
                items['call_time'] = row.get(u'起始时间', '')
                items['call_location'] = row.get(u'起始时间', '')
                items['call_phone'] = row.get(u'对方号码', '')
                items['call_type'] = row.get(u'呼叫类型', '')
                items['roma_type'] = row.get(u'通话类型', '')
                items['amount'] = row.get(u'费用（元）', '')
```


```python
items = {
    'user': user,
    'host_phone': host_phone
}
```


```python
def fetch_detail(self, token, code, **kwargs):

                kwargs['current_month'] = months[2]
                kwargs['start_time'] = months[3]
                kwargs['end_time'] = months[4]

```


```python
def fetch_detail(self, token, code, **kwargs):

                kwargs.update({
                    'current_month': months[2]
                    'start_time': months[3]
                    'end_time': months[4]
                })
```
