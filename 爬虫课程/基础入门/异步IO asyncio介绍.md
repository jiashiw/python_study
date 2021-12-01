#### 代码语法

```
import asyncio
＃ 获取事件循环
loop = asyncio.get_event_loop()
＃定义协程
async def myfunc(url):
[await get_url(url)
＃创建task列表
tasks = lloop.create_ task( myfunc(url) for url in urls]
＃ 执行爬虫事件列表
loop.run_until_complete(asyncio.wait(tasks))
```
**注意：**   
* 要用在异步IO编程中,依赖的库必须支持异步IO特性  
* 爬虫引用中：requests不支持异步,需要用aiohttp


