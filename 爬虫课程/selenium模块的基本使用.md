#### 问题1：selenium模块和爬虫之间具有怎样的关联？
* 便捷的获取网站中动态加载的数据
* 便捷实现模拟登录工
#### 问题2：什么是selenium模块？
* 基于浏览器自动化的一个模块。

```
from selenium import webdriver
from lxml import etree
from time import sleep
from selenium.webdriver.chrome.service import service
# 实例化一个浏览器对象（传入浏览器的驱动）

bro = webdriver.Chrome(executable_path='/Users/js/PycharmProjects/爬虫课程/第六章：动态加载数据处理/chromedriver')
# 让浏览器发起一个指定url对应的请求
bro.get('http://scxk.nmpa.gov.cn:81/xk/')
# 获取浏览器当前页面的页面源码数据
page_text = bro.page_source

# 解析企业名称
tree = etree.HTML(page_text)
li_list = tree.xpath('//*[@id="gzlist"]/li')
print(li_list)

for li in li_list:
    name = li.xpath('./dl/@title')[0]
    print(name)

sleep(5)
bro.quit()
```
