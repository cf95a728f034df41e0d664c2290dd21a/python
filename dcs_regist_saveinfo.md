```python
def update_regist_info(name, phone, msg, pubtime, count, order):
    if msg == 'fail':
        registinfo = RegistInfo.objects.filter(name=name, phone=phone).update(
                pubtime=pubtime, count=count, order=order)
        return registinfo
    else:
        registinfo = RegistInfo.objects.filter(name=name, phone=phone).update(
                msg=msg, pubtime=pubtime, count=count, order=order)
        return registinfo
```


```python
def update_regist_info(name, phone, msg, pubtime, count, order):
    kwargs = {'pubtime': pubtime, 'count': count, 'order': order}
    if msg != 'fail':
        kwargs['msg'] = msg

    return RegistInfo.objects.filter(name=name, phone=phone).update(**kwargs)
```
