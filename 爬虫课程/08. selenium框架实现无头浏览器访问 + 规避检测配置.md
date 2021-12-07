```
from selenium import webdriver
from time import sleep
from selenium.webdriver.chrome.service import Service

# 实现无可视化界面
from selenium.webdriver.chrome.options import Options

# 实现规避检测
from selenium.webdriver import ChromeOptions

# 实现无可视化界面
options = Options()
options.add_argument('--headless')
options.add_argument('--disable-gpu')

# 实现规避检测
chromeOptions = ChromeOptions()
chromeOptions.add_experimental_option('excludeSwitches', ['enable-automation'])

if __name__ == '__main__':
    s = Service(r'/Users/js/PycharmProjects/爬虫课程/第六章：动态加载数据处理/chromedriver')
    browser = webdriver.Chrome(service=s, chrome_options=options, options=chromeOptions)

    # 无可视化界面（无头浏览器） phantomJs
    browser.get('https://www.baidu.com')

    print(browser.page_source)

    sleep(2)
    browser.quit()
```
