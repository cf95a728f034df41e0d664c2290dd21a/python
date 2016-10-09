```python
# /home/capric/data/yqjr/Python/trunk/dcs/rest/middleware.py


class TokenRequireMiddleware(object):

    def process_request(self, request):
        if reverse('getToken') == request.path:
            setattr(request, 'permit', {})
            setattr(request, 'token', str(token))
            
```


```python
class TokenRequireMiddleware(object):

    def process_request(self, request):
        if reverse('getToken') == request.path:
            request.permit = {}
            setattr.token = str(token)
      
```
