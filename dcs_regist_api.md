## 1. dict定义直接赋值，不需要逐个赋值
```python
class WebSite(object):
    def __init__(self, param, order=None):
        self.param = param
        self.result = {}
        self.result['phone'] = param
        self.result['order'] = order
        self.count = 0
```

```python
class WebSite(object):
    def __init__(self, param, order=None):
        self.param = param
        self.result = {'phone': param, 'order': order}
        self.count = 0
```


## 2. 如果抓取某个站点的信息，方法命名可参照其url
```python
    def bai_cai(self):
        logger.debug('---------- enter 贝才网----------------')
        self.result['url'] = 'http://www.thebetterchinese.com/register/toregister.html'
        self.result['name'] = u'贝才网'
        session = get_session()
```

```python
    def the_better_chinese(self):
        logger.debug('---------- enter 贝才网----------------')
        self.result['url'] = 'http://www.thebetterchinese.com/register/toregister.html'
        self.result['name'] = u'贝才网'
        session = get_session()
```


## 3. 省掉if...else...
```python
# /home/capric/data/yqjr/Python/trunk/dcs/regist/api.py
            if msg['ret']['success'] == False:
                msg = {'msg': 'true'}

            elif msg['ret']['success'] == True:
                msg = {'msg': 'false'}
                
            else:
                logger.info('requests is sucess, msg is %s' % msg)
                msg = {'msg': 'fail'}
```

```python
            msg = {'msg': str(msg['ret']['success']).lower()}
```


