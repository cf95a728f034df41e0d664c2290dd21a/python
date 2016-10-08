```python
import asyncio
import datetime


async def display_date(loop):
    end_time = loop.time() + 5.0
    while True:
        print(datetime.datetime.now())
        if (loop.time() + 1.0) >= end_time:
            break
        await asyncio.sleep(1)


if __name__ == '__main__':
    loop = asyncio.get_event_loop()
    loop.run_until_complete(display_date(loop))
    loop.close()
```


```python
import asyncio

async def compute(x, y):
    print('Compute %s + %s ...' % (x, y))
    await asyncio.sleep(1.0)
    return x + y

async def print_sum(x, y):
    result = await compute(x, y)
    print('%s + %s = %s' % (x, y, result))


if __name__ == '__main__':
    loop = asyncio.get_event_loop()
    loop.run_until_complete(print_sum(1, 2))
    loop.close()
```


```python
import sys  
import json
import signal  
import asyncio  
import aiohttp  

loop = asyncio.get_event_loop()  
client = aiohttp.ClientSession(loop=loop)


async def get_json(client, url):  
    async with client.get(url) as response:
        assert response.status == 200
        return await response.read()


async def get_reddit_top(subreddit, client):  
    data1 = await get_json(client, 'https://www.reddit.com/r/' + subreddit + '/top.json?sort=top&t=day&limit=5')

    j = json.loads(data1.decode('utf-8'))
    for i in j['data']['children']:
        score = i['data']['score']
        title = i['data']['title']
        link = i['data']['url']
        print(str(score) + ': ' + title + ' (' + link + ')')

    print('DONE:', subreddit + '\n')


def signal_handler(signal, frame):  
    loop.stop()
    client.close()
    sys.exit(0)


if __name__ == '__main__':
    signal.signal(signal.SIGINT, signal_handler)

    asyncio.ensure_future(get_reddit_top('python', client))  
    asyncio.ensure_future(get_reddit_top('programming', client))  
    asyncio.ensure_future(get_reddit_top('compsci', client))  
    loop.run_forever()  
```
