```python
# /home/capric/data/yqjr/Python/trunk/dcs/rest/signals.py

from celery.signals import task_failure

@task_failure.connect
def send_error_message(*args, **kwargs):
    logger.debug(args)
    logger.debug(kwargs)
```
