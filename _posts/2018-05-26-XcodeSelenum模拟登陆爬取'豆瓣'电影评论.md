---
layout:     post
title:      Selenum模拟登陆爬取'豆瓣'电影评论
subtitle:   Selenum模拟登陆爬取'豆瓣'电影评论
date:       2018-05-26
author:     BOBO
header-img: img/post-bg-kuaidi.jpg
catalog: true
tags:
    - 爬虫
---
﻿## 开始
```python

#首席那安装selinium
from selenium import webdriver
import time
from lxml import etree
import json
#添加显示等待
from selenium.webdriver.support.ui import WebDriverWait
#根据条件寻找对应节点
from selenium.webdriver.support import expected_conditions as EC
import requests
import re
import urllib.parse
import urllib
import csv
import os
# from w3lib.html import remove_tags
# birth_weight_file = 'birth_weight.csv'
header = {
    "User-Agent":"Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36",
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate, br",
    "Accept-Language": "en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7",
    "Connection": "keep-alive",
    "Cookie": 'll="108293"; bid=ZhBAGA3s9Z4; __utmc=30149280; __utmz=30149280.1558788663.1.1.utmcsr=wx.qq.com|utmccn=(referral)|utmcmd=referral|utmcct=/; _vwo_uuid_v2=DC2C59F1AAFB62E6AC80AE2F5138E05E0|2f9fdfd8614610d60cd2be061072faa7; push_noty_num=0; push_doumail_num=0; dbcl2="186705531:tdt3UnU/3+8"; ck=g3On; _pk_ref.100001.8cb4=%5B%22%22%2C%22%22%2C1558790349%2C%22https%3A%2F%2Faccounts.douban.com%2Fpassport%2Flogin%22%5D; __utmv=30149280.18670; _pk_id.100001.8cb4=1ce6ca18acd029a1.1558790349.1.1558792701.1558790349.; ap_v=0,6.0; __utma=30149280.1804237607.1558788663.1558795739.1558798475.3; __utmb=30149280.0.10.1558798475',
    "Host": "www.douban.com",
    "Referer": "https://movie.douban.com/subject/30170448/collections?start=0",
    "User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.131 Safari/537.36",
    
}


#设置无头浏览器
# options=webdriver.ChromeOptions()
# options.set_headless()
#创建浏览器驱动





driver = webdriver.Chrome(
    executable_path='/home/lbc/Documents/chromedriver',
    )
    # options=options 
# driver.get('https://www.douban.com/')
driver.get('https://accounts.douban.com/passport/login')
#获取cookie
cookies = driver.get_cookies()

cookie_dict = {}
for cookie in cookies:
    cookie_dict[cookie['name']] = cookie['value']
# print(cookie_dict)

#导入鼠标移入
from selenium.webdriver import ActionChains
# 用xpath解析并拖拽鼠标进行点击
# 点击登录
element = driver.find_element_by_xpath('//*[@id="account"]/div[2]/div[2]/div/div[1]/ul[1]/li[2]')
# element = driver.find_element_by_xpath('/html/body/div[1]/div[1]/ul[1]/li[2]')
#将鼠标移动到指定的节点
ActionChains(driver).move_to_element(element).perform()
#将鼠标移动到指定的节点并且点击该节点(单击)
ActionChains(driver).move_to_element(element).click(element).perform()
# # 手机号登录
# element = driver.find_element_by_xpath('//*[@id="alert-action-login"]/div/div/div/div[1]/div[2]/p[2]/a[1]')
# #将鼠标移动到指定的节点
# ActionChains(driver).move_to_element(element).perform()
# #将鼠标移动到指定的节点并且点击该节点(单击)
# ActionChains(driver).move_to_element(element).click(element).perform()

driver.find_element_by_name('username').send_keys('1532624****')
#隐式等待
driver.find_element_by_name('password').send_keys('****')
# 输入账号密码点击登录
element = driver.find_element_by_xpath('//*[@id="account"]/div[2]/div[2]/div/div[2]/div[1]/div[4]/a')
# element = driver.find_element_by_xpath('/html/body/div[1]/div[2]/div[1]/div[6]/a')
#将鼠标移动到指定的节点
ActionChains(driver).move_to_element(element).perform()
#将鼠标移动到指定的节点并且点击该节点(单击)
ActionChains(driver).move_to_element(element).click(element).perform()






# driver.get('https://movie.douban.com/')
# #获取cookie
# cookies = driver.get_cookies()

# cookie_dict = {}
# for cookie in cookies:
#     cookie_dict[cookie['name']] = cookie['value']
# driver.find_element_by_name('search_text').send_keys('何以为家')
# element = driver.find_element_by_xpath('//*[@id="db-nav-movie"]/div[1]/div/div[2]/form/fieldset/div[2]/input')
#     #将鼠标移动到指定的节点
# ActionChains(driver).move_to_element(element).perform()
#     #将鼠标移动到指定的节点并且点击该节点(单击)
# ActionChains(driver).move_to_element(element).click(element).perform()





driver.get('https://www.douban.com/')
#获取cookie
cookies = driver.get_cookies()

cookie_dict = {}
for cookie in cookies:
    cookie_dict[cookie['name']] = cookie['value']
driver.find_element_by_id('inp-query').send_keys('何以为家')
element = driver.find_element_by_xpath('//*[@id="db-nav-sns"]/div/div/div[2]/form/fieldset/div[2]/input')
    #将鼠标移动到指定的节点
ActionChains(driver).move_to_element(element).perform()
    #将鼠标移动到指定的节点并且点击该节点(单击)
ActionChains(driver).move_to_element(element).click(element).perform()




driver.get('https://www.douban.com/search?source=suggest&q=%E4%BD%95%E4%BB%A5%E4%B8%BA%E5%AE%B6')
#获取cookie
cookies = driver.get_cookies()

cookie_dict = {}
for cookie in cookies:
    cookie_dict[cookie['name']] = cookie['value']
# driver.find_element_by_id('inp-query').send_keys('何以为家')
element = driver.find_element_by_xpath('//*[@id="content"]/div/div[1]/div[3]/div[2]/div[1]/div[2]/div/h3/a')
    #将鼠标移动到指定的节点
ActionChains(driver).move_to_element(element).perform()
    #将鼠标移动到指定的节点并且点击该节点(单击)
ActionChains(driver).move_to_element(element).click(element).perform()



# for gg in range(0,180):
    # asdf = 'https://movie.douban.com/subject/30170448/collections?start=gg'%(gg)
driver.get('https://movie.douban.com/subject/30170448/collections?start=0')
#获取cookie
cookies = driver.get_cookies()

cookie_dict = {}
for cookie in cookies:
    cookie_dict[cookie['name']] = cookie['value']
# driver.find_element_by_id('inp-query').send_keys('何以为家')
element = driver.find_element_by_xpath('//*[@id="collections_tab"]/div[2]')
    #将鼠标移动到指定的节点
ActionChains(driver).move_to_element(element).perform()
    #将鼠标移动到指定的节点并且点击该节点(单击)
ActionChains(driver).move_to_element(element).click(element).perform()


data=driver.page_source
abc=etree.HTML(data)
d = abc.xpath('//*[@id="collections_tab"]/div[2]')
# print(d)
for i in d:
    time = i.xpath('./table/tbody/tr/td[2]/p/text()')
    # times = remove_tags(time)
    # for times in time:
    #     a = times
    star = i.xpath('./table/tbody/tr/td[2]/p/span/@title')
    # for stars in star:
    #     b = stars
    pic = i.xpath('./table/tbody/tr/td[1]/a/img/@src')
    # for pics in pic:
    #     c = pics
    name = i.xpath('./table/tbody/tr/td[1]/a/img/@alt')
    # for names in name:
    #     d = names
    content = i.xpath('./table/tbody/tr/td[2]/p[2]/text()')
    # for contents in content:
    #     e = contents
    userurl = i.xpath('./table/tbody/tr/td[1]/a/@href')
    # for userurls in userurl:
    #     f = userurls
    print(time,star,pic,name,content,userurl)

```
![](https://camo.githubusercontent.com/bc30f861eaf3fdafa7f40d8755928133a9c71ba3/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139303532363131313630393133392e706e673f782d6f73732d70726f636573733d696d6167652f77617465726d61726b2c747970655f5a6d46755a33706f5a57356e6147567064476b2c736861646f775f31302c746578745f6148523063484d364c7939696247396e4c6d4e7a5a473475626d56304c334678587a51784e5441774d6a49792c73697a655f31362c636f6c6f725f4646464646462c745f3730)
