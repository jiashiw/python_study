需求：爬取指定页面下面的品牌及公司名，并保存至本地
下一步优化：爬取详情页中的京东店铺和官网地址

```
from selenium import webdriver
from lxml import etree
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.common.exceptions import TimeoutException
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from time import sleep
import xlwt

# 实例化一个浏览器对象（传入浏览器的驱动）
s = Service(r'/Users/js/PycharmProjects/爬虫课程/第六章：动态加载数据处理/chromedriver')
bro = webdriver.Chrome(service=s)
rowdata_bn = []
rowdata_cn = []

# 获得指定品类下的指定品牌信息
bro.get('https://www.maigoo.com/brand/search/?catid=207')

bottom = True
while bottom:
    try:
        wait = WebDriverWait(bro, 15)
        btn = wait.until(EC.element_to_be_clickable((By.CLASS_NAME, "morebtn")))
        btn.click()
        sleep(1)
        # 判断底部按钮文案，若是'加载更多'则继续执行循环，若是其他文案，则停止循环开始爬取数据
        locator = ('class name','morebtn')
        text = '加载更多'
        btn_text = wait.until(EC.text_to_be_present_in_element(locator, text))
        if btn_text:
            bottom = True
        else:
            bottom = False
    except TimeoutException:
        break

page_text = bro.page_source
tree = etree.HTML(page_text)
li_list = tree.xpath('//*[@id="pos_resultlist"]/div[1]/div/ul/li')
for li in li_list:
    brand_name = li.xpath('./div[2]/div[1]/a[1]/text()')[0]
    company_name = li.xpath('./div[2]/div[1]/span/text()')[0]
    rowdata_bn.append(brand_name)
    rowdata_cn.append(company_name)

# 创建excel文件并写入数据
f = xlwt.Workbook(encoding="utf-8")
sheet1 = f.add_sheet('品牌信息',cell_overwrite_ok=True)
rowtitle = ['品牌名','企业名']

# 遍历向表格写入标题行信息
for i in range(0,len(rowtitle)):
    sheet1.write(0,i,rowtitle[i])

# 遍历向表格写入品牌信息
for j in range(1,len(rowdata_bn)):
    sheet1.write(j,0,rowdata_bn[j-1])

for k in range(1,len(rowdata_cn)):
    sheet1.write(k,1,rowdata_cn[k-1])

f.save('/Users/js/PycharmProjects/爬虫课程/自己实践操作/maigoo.xls')
bro.quit()
```
