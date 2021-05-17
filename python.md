# 爬虫知识

http协议

```
 -概念：就是服务器和客户端进行数据交互的一种形式

常用请求头信息：

​  -User-Agent ：请求载体的身份标识

​  -Connection：请求完毕后，是断开连接还是保持连接

 常用响应头信息

​  -Content-Type：服务器响应回客户端的数据类型
```

https协议：---安全的超文本传输协议

  加密方式：

​        -对称秘钥加密

​        -非对称秘钥加密

​        -证书秘钥加密



requests模块

​      -urllib模块

​      -requests模块

requests模块：Python中原生的一款基于网络请求的模块，功能强大，简单

​               作用：模拟浏览器发送请求。

requests模块的编码流程：

​              -指定url

​              -发起请求

​              -获取响应数据

​              -持久化存储

```
#需求：爬取淘宝官网的页面上数据
import requests
def askUrl():
    #1.指定url
    url = "https://www.taobao.com/"
    #2.发起请求，get方法会返回一个响应对象
    req = requests.get(url=url)
    #3.获取响应数据，text返回的是字符串形式的响应数据
    page_text = req.text
    #4.持久化存储数据
    with open("./taobao.html",'w',encoding="utf-8") as f:
        f.write(page_text)
if __name__ == '__main__':
    askUrl()
    print("爬取数据完毕")
```

​      爬取搜狗指定词条对应的搜索结果界面（建业网页采集器）

```
#UA:User-Agent（请求载体的身份标识）
#UA检查：门户网站的服务器会检测对应请求的载体身份标识，如果检测到请求的载体身份标识是浏览器，
#说明该请求是一个正常的请求。但是如果检测到请求的载体身份标识不是基于某一款浏览器则为不正常的请求（爬虫），
#则服务器端就很有可能拒绝该次请求。

#UA伪装：让爬虫对应的请求载体身份标识伪装成某一款浏览器。

def askSoGou():
    url = "https://www.sogou.com/web"
    #处理url携带的参数：封装到字典中
    kw = input("请输入查询的关键字：")
    params = {
        'query':kw
    }
    headers = {
        'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.212 Safari/537.36'
    }
    #对指定的url发起的请求对应的url是携带参数的，并且请求处理过程中处理了参数
    response = requests.get(url,params=params,headers = headers)
    page_text = response.text
    filename = kw+'.html'
    with open(filename,'w',encoding='utf-8') as f:
        f.write(page_text)
```

 破解百度翻译

​     爬虫分类：通用爬虫、聚焦爬虫、增量爬虫

bs4进行数据解析

​      -数据解析的原理

​                  -1.标签定位

​                  -2.提取标签、标签属性中存储的数据值

​       -bs4数据解析的原理

​                  -1.实例化一个BeautifulSoup对象，并且将页面源码数据加载到该对象中

​                 -2.通过调用BeautifulSoup对象中相关的属性或者方法进行标签定位和数据提取。

​      -环境安装

​			pip  install bs4

​			pip  install  lxml

​	-提供用于数据分析的属性和方法：（soup是创建的BeautifulSoup对象）

​			1.soup.tagName(标签名称)：返回HTML中第一次出现的tagName

​			2.soup.find():

​					-find('tagName'):等价于soup.tagName

​					-属性定位

​						find（'tagName',class_/id/attrs='属性值'）

​			 3.find_all('tagName'):返回符合要求的所有标签（列表）

​			4.select

​					-select('某种选择器（id，select，标签选择器）')：返回的是一个列表

​					-层级选择器

​								-select('.tang>ul>li>a') ：>表示的是一个层级

​								-select('.tang>ul a'):空格表示多个层级

​		5.如何获取标签之间的文本数据

​						-soup.a.text/string/get_text()

​							-text/get_text():可以获取某一标签中所有的文本内容

​							-string：只可以获取该标签下面直系的文本内容

​		6.如何获取标签中的属性值

​							-soup.tagName['属性名']



