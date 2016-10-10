```python
import time
import calendar as cal


def getMonths():
    now = time.localtime()
    monthlist = [time.localtime(time.mktime((now.tm_year, now.tm_mon - n, 1, 0, 0, 0, 0, 0, 0)))[:2] for n in range(6)]
    months = []
    for i in monthlist:
        year = i[0]
        month = i[1]
        d = cal.monthrange(year, month)
        if month  < 10:
            month = '0' + str(month)
            start_time = '%d-%s-%s' %(year, month, '01')
            end_time = '%d-%s-%d' %(year, month, d[1])
            current_month = str(year) +'-'+ str(month)
        else:
            start_time = '%d-%d-%s' %(year, month, '01')
            end_time = '%d-%d-%d' %(year, month, d[1])
            current_month = str(year) +'-'+str(month)
        t = (year, month, current_month, start_time, end_time)
        months.append(t)
    return months
```


```python
import calendar
import datetime


# list(get_last_months())
def get_last_months(n=6):
    month_first_day = datetime.date.today().replace(day=1)
    month_last_day = month_first_day.replace(day=calendar.monthrange(month_first_day.year, month_first_day.month)[-1])
    yield (
        month_last_day.year, month_last_day.month, month_last_day.strftime('%Y-%m'),
        month_first_day.strftime('%Y-%m-%d'), month_last_day.strftime('%Y-%m-%d')
    )

    for _ in range(n - 1):
        month_last_day = month_last_day.replace(day=1) - datetime.timedelta(days=1)
        month_first_day = month_last_day.replace(day=1)
        yield (
            month_last_day.year, month_last_day.month, month_last_day.strftime('%Y-%m'),
            month_first_day.strftime('%Y-%m-%d'), month_last_day.strftime('%Y-%m-%d')
        )
```
