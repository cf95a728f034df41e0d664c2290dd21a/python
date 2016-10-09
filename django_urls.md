```python
# /home/capric/data/yqjr/Python/trunk/dcs/dcs/urls.py

urlpatterns = [
 	url(r'^chinamobile/', include('chinamobile.urls')),
	url(r'^jd/', include('jd.urls')),
]
```

```python
# /home/capric/data/yqjr/Python/trunk/dcs/jd/urls.py

urlpatterns = [

  #测试京东服务
	url(r'^jdLoginPrepare',login_get_picture_codes),     #预登陆---判断是否需要图形码
	url(r'^jdLoginNeedCode',login_need_picture_codes),   #登录-----需要图形码
	url(r'^jdLogin',login_nos),                          #登录-----不需要图形码
	url(r'^jdGetOrders',get_order),                      #获取用户订单
]
```


## 1. 混用space, tab缩进
## 2. 注释
## 3. typo
## 4. url
