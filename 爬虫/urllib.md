## 爬虫的工作流程

**模拟浏览器**向服务器发送请求 服务器返回所以的网页源码
我们要的是网页源码的部分数据

1 urllib
​	获取网站的所以数据

2 解析
	将网页的源码解析 获取部分数据
​		正则
​		xpath
		beatutiful soup bs4
		jsonpath

3 selenium
	驱动**真实浏览器** 发送请求

4 request 和urllib是作用一样的

5 scrapy 框架

6 scrapy+redis 框架 分布式爬虫

7 多线程爬虫 + docker + splush



## 爬虫分类

通用爬虫： 访问网页—》抓取数据—》数据存储—》数据处理—》提供检索服务

聚焦爬虫：确定要爬取的url—》模拟浏览器通过http协议访问url，获取服务器返回的html代码—》解析html字符串



## 爬虫语言分类

- php：多进程和多线程支持不好
- java：代码臃肿，代码量大，重构成本高，而爬虫需要经常修改，所以Java开发爬虫不
- C\C++：性能和效率高，停留在研究层
- python：语法简洁优美，对新手友好，支持模块多，有scrapy爬虫框架



## 爬虫的用途

- 数据分析/人工数据集
- 社交软件冷启动
- 舆情控制
- 竞争对手监控

## 反爬手段

1 user-Agent(用户代理)

​	User Agent中文名为用户代理，简称 UA，它是一个特殊字符串头，使得服务器能够识别客户使用的操作系统及版本、CPU 类型、浏览器及版本、浏览器渲染引擎、浏览器语言、浏览器插件等。

2 代理IP：西次代理(免费)、快代理(付费)

​	什么是高匿名、匿名和透明代理？它们有什么区别？
​	1.使用透明代理，对方服务器可以知道你使用了代理，并且也知道你使用了真实IP
​	2.使用匿名代理，对方服务器知道你使用了代理，但不知道你的真实IP
​	3.使用高匿名代理，对方服务器不知道你使用了代理，更不知道你的真实IP

3 验证码访问：打码平台、云打码平台、超级鹰

4 动态加载网页
​	网站返回的是js数据，并不是网页的真实数据。而selenium驱动真实的浏览器发送请求

5 数据加密：分析js代码



Http协议

http和https的区别？

什么是SSL？





urllib的基本使用

```python
import urllib.reequest
url = 'http://www.baidu.com'
response = urllib.request.urlopen(url=url)
print(response)#<http.client.HTTPResponse object at 0x7f880959b710>
print(type(response))#<class 'http.client.HTTPResponse'>
```

response的六个方法

```python
import urllib.request
url= 'http://www.baidu.com'
response = urllib.requset.urlopen(url=url)

#2）read
print(response.read())#以二进制的格式来获取网站源码
print(response.read(5))#读取前五个字节
#编码 编写成二进制的格式 字符串--》二进制 encode
#解码 编写成字符串格式 二进制--》字符串 decode

print(response.read().decode('utf-8))#以字符串的格式读取网站源码

#2）readline
a = response.readline()#以二进制的格式读取一行

#3）readlines 一行一行的读取 直到读取完为止


#4) getcode 获取响应的状态码
print(response.getcode())#200

#5) geturl 获取url
print(response.geturl())#http://www.baidu.com  
     
#6) getheaders 获取headers
print(response.getheaders())
```

下载网页、图片、音频

```python
import urllib.request

# url 是访问路径 filename是下载后保存到的文件
#下载网页
url = 'http://www.baidu.com'
urllib.request.urlretrieve(url=url,filename='bd.html')

#下载图片
url = '图片的url'
urllib.request.urlretrieve(url=url,filename='tupian.jpg')

#下载视频
url = '视频的url'
urllib.request.urlretrieve(url=url,filename='')
```

请求对象的定制

```python
import urllib.request
#默认情况下 urllib.request.urlopen方法 访问服务器携带的是ua是python得到ua 那么很多网站会检测ua的真实性 如果是一个爬虫程序 那么将不会给你返回数据
url ='http://www.baidu.com'

headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11'}


#urlopen方法中是没有headers的属性的 所以不可以直接在该方法中添加ua
#response=urllib.request.urlopen(url=url,headers=headers)


request = urllib.request.Request(url=url,headers=headers)
response = urllib.request.urlopen(request)
print(response.getcode())
```

get请求的编解码（单个参数）

```python
#默认情况下 浏览器会自动的进行编解码 当汉语复制到pycharm的时候 pycharm不会自动编解码

import urllib.request
import urllib.parse

#url = 'http://www.baidu.com/s?wd=遮天'

url = 'http://www.baidu.com/s?wd='
name = '遮天'
name = urllib.request.quote(name)#将name进行编码
url = url + name
response = urllib.request.urlopen(url=url)

t = response.read().decode('utf-8')
print(t)

```

get请求编解码+请求对象的定制

```
import urllib.request
import urllib.parse

url ='http://www.baidu.caom/s?wd='

data = '王者荣耀'
data = urllib.parse.quote(data)
url = url+data

headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11'}

request = urllib.request.Request(url=url,headers=headers)

response = urllib.request.urlopen(request)
```

get请求方式多个参数的编解码

```python
import urllib.request
import urllib.parse

#url ='http://www.baidu.com/s?name=鞠婧祎&sex=女'


url ='http://www.baidu.com/s?'

data = {
    'wd':'鞠婧祎',
    'sex':'女',
}

data = urllib.parse.urlencode(data)
url = url + data#拼接url

headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11'}

request = urllib.request.Request(url=url,headers=headers)
reponse = urllib.request.urlopen(request)
print(response.read().decode('utf-8'))
```

post请求

```python
#eg1百度翻译

import urllib.request
import urllib.parse

url = 'https://fanyi.baidu.com/sug'

data = {
    'kw':'lemon'
}
#post 请求必须编码 而get请求不需要后面的encode进行在编码
data = urllib.parse.urlencode(data).encode('utf-8')

headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11'}

request = urllib.request.Request(url=url,headers=headers,data=data)

response = urllib.request.urlopen(request)

content = response.read().decode('utf-8')
print(context)#


import json
obj = json.loads(content)
s = json.dumps(obj,ensure_ascii=False)
print(s)
```

```python
#eg2百度翻译详细翻译
import urilib.request
import urllib.parse

url = 'https://fanyi.baidu.com/v2transapi?from=en&to=zh'

data = {
    'from': 'en',
    'to': 'zh',
    'query': 'lemon',
    'transtype': 'realtime',
    'simple_means_flag': '3',
    'sign': '98384.353121',
    'token': 'b53bf7493df35a11a4db21060c945d81',
}

data = urllib.parse.urlencode(data).encode('utf-8')

headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11'}

request = urllib.request.Request(url=url,headers=headers,data=data)
response = urllib.request.urlopen(request)

content = response.read().decode('utf-8')

import json
obj = json.loads(content)
s = json.dumps(obj,ensure_ascii=False)
print(s)
```



get 请求和post 请求的区别
​	get 请求将参数编码之后需要和url进行拼接
	post 请求将参数编码之后需要调用encode，而get 请求不需要



ajax的get请求

```python
eg1爬取豆瓣电影
import urllib.request
url = 'https://movie.douban.com/j/chart/top_list?type=13&interval_id=100%3A90&action=&start=0&limit=20'

headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11'}

request = urllib.request.Request(url=url,headers=headers)
response = urllin.request.urlopen(request)
content = response.read().decode('utf-8')

with open('douban.json','w',ecoding='utf-8') as fp:
    fp.write(content)
```

```python
eg2 豆瓣电影多页下载
import urllib.request
import urllib.parse
start_page = int(input('请输入起始页码：'))
end_page = int(input('请输入结束页码：'))
for page in range(start_page,end_page+1):
    url = 'https://movie.douban.com/j/chart/top_list?'
    data = {
        'type': '25',
        'interval_id': '100:90',
        'action': '',
        'start': (page - 1) * 20,#此处不能加单引号
        'limit': '20',
    }

    data = urllib.parse.urlencode(data)
    url = url + data
    headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11'}

    request = urllib.request.Request(url=url,headers=headers)
    response = urllib.request.urlopen(request)
    content = response.read().decode('utf-8')
    with open('douban_'+str(page)+'.json','w',encoding='utf-8')as fp:
        fp.write(content)
```



ajax的POST请求 

```python
eg1 KFC官网
#写法一
import urllib.request
import urllib.parse

def create_request(page):
    url = 'http://www.kfc.com.cn/kfccda/ashx/GetStoreList.ashx?op=cname'
    data = {
        'cname': '上海',
        'pid': '',
        'pageIndex': page,
        'pageSize': '10',
    }
	data = urllib.parse.urlencode(data).encode('utf-8')
    headers = {
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11'
    }
    
    request = urllib.request.Request(url=url,headers=headers,data=data)
    return request

def get_content(request):
    response = urllib.request.urlopen(request)
    content = response.read().decode('utf-8')
    return content
    
def down_load(page,content):
    with open('kfc_'+str(page)'.json','w',encodeing='utf-8')as fp:
        fp.write(content)


if __name__ == '__main__':
    start_page = int(input('请输入起始页码'))
    end_page = int(input('请输入结束页码'))
    for page in range(start_page,end_page+1):
    	request = create_request(page)
        content = get_content(request)
        down_load(page,content)
        
        
        
        
        
 #写法二       
import urllib.request
import urllib.parse

start_page = int(input('请输入起始页码'))
end_page = int(input('请输入结束页码'))
for page in range(start_page,end_page+1):
    url = 'http://www.kfc.com.cn/kfccda/ashx/GetStoreList.ashx?op=cname'
    data = {
        'cname': '上海',
        'pid': '',
        'pageIndex': page,
        'pageSize': '10',
    }

    data = urllib.parse.urlencode(data).encode('utf-8')
    headers = {
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11'
    }

    request = urllib.request.Request(url=url, headers=headers, data=data)

    response = urllib.request.urlopen(request)
    content = response.read().decode('utf-8')

    with open('kfc_'+str(page)+'.json','w',encoding='utf-8')as fp:
        fp.write(content)
```

复杂get-百度贴吧

```python
import urllib.request

def create_request(page):
    url = 'http://tieba.baidu.com/f?kw=python&ie=utf-8&pn='
    url = url + str((page-1)*50)
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36'
    }
    request = urllib.request.Request(url=url,headers=headers)
    return request


def get_content(request):
    response = urllib.request.urlopen(request)
    content = response.read().decode('utf-8')
    return content


def down_load(page, content):
    with open('tieba_' + str(page) + '.html','w',encoding='utf-8')as fp:
        fp.write(content)


if __name__ == '__main__':
    start_page = int(input('请输入起始页码'))
    end_page = int(input('请输入结束页码'))
    for page in range(start_page,end_page+1):
        request = create_request(page)
        content = get_content(request)
        down_load(page,content)
```

异常

HTTPError

URLError

HTTPError是URLError的子类

```python

import urllib.request
import urllib.error
url = 'https://blog.csdn.net/ityard/article/details/102646738'

# url = 'http://www.goudan11111.com'

headers = {
        # 'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3',
        # 'Accept-Encoding': 'gzip, deflate, br',
        # 'Accept-Language': 'zh-CN,zh;q=0.9',
        # 'Cache-Control': 'max-age=0',
        # 'Connection': 'keep-alive',
        'Cookie': 'uuid_tt_dd=10_19284691370-1530006813444-566189; smidV2=2018091619443662be2b30145de89bbb07f3f93a3167b80002b53e7acc61420; _ga=GA1.2.1823123463.1543288103; dc_session_id=10_1550457613466.265727; acw_tc=2760821d15710446036596250e10a1a7c89c3593e79928b22b3e3e2bc98b89; Hm_lvt_e5ef47b9f471504959267fd614d579cd=1571329184; Hm_ct_e5ef47b9f471504959267fd614d579cd=6525*1*10_19284691370-1530006813444-566189; __yadk_uid=r0LSXrcNYgymXooFiLaCGt1ahSCSxMCb; Hm_lvt_6bcd52f51e9b3dce32bec4a3997715ac=1571329199,1571329223,1571713144,1571799968; acw_sc__v2=5dafc3b3bc5fad549cbdea513e330fbbbee00e25; firstDie=1; SESSION=396bc85c-556b-42bd-890c-c20adaaa1e47; UserName=weixin_42565646; UserInfo=d34ab5352bfa4f21b1eb68cdacd74768; UserToken=d34ab5352bfa4f21b1eb68cdacd74768; UserNick=weixin_42565646; AU=7A5; UN=weixin_42565646; BT=1571800370777; p_uid=U000000; dc_tos=pzt4xf; Hm_lpvt_6bcd52f51e9b3dce32bec4a3997715ac=1571800372; Hm_ct_6bcd52f51e9b3dce32bec4a3997715ac=1788*1*PC_VC!6525*1*10_19284691370-1530006813444-566189!5744*1*weixin_42565646; announcement=%257B%2522isLogin%2522%253Atrue%252C%2522announcementUrl%2522%253A%2522https%253A%252F%252Fblogdev.blog.csdn.net%252Farticle%252Fdetails%252F102605809%2522%252C%2522announcementCount%2522%253A0%252C%2522announcementExpire%2522%253A3600000%257D',
        # 'Host': 'blog.csdn.net',
        # 'Referer': 'https://passport.csdn.net/login?code=public',
        # 'Sec-Fetch-Mode': 'navigate',
        # 'Sec-Fetch-Site': 'same-site',
        # 'Sec-Fetch-User': '?1',
        # 'Upgrade-Insecure-Requests': '1',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36',
    }


try:
    request = urllib.request.Request(url=url,headers=headers)

    response = urllib.request.urlopen(request)

    content = response.read().decode('utf-8')
    print(content)
except urllib.error.HTTPError:
    print(1111)
#当资源路径存在 但有细微差别 会报错111 是HTTPError错误
except urllib.error.URLError:
    print(2222)
    #整个域名就不存在的情况下 会报222 是URLError错误
```

cookie登录

```python
eg1 人人网
import urllib.request


url = 'http://www.renren.com/305523888/profile'
headers = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11',
    'Cookie': 'anonymid=jix3nuu4-498h3n; _de=BF83005E46A2ACDF72FFEFECAA50653A696BF75400CE19CC; ln_uact=595165358@qq.com; ln_hurl=http://hdn.xnimg.cn/photos/hdn521/20170509/0940/main_5crY_aee9000088781986.jpg; _r01_=1; jebe_key=b8a3f973-563c-4e6a-ac8f-99deef080f20%7Ccfcd208495d565ef66e7dff9f98764da%7C1565664618046%7C0%7C1565664616181; wp_fold=0; depovince=SH; jebecookies=dd7a7840-774a-44e8-89ab-36942629e3af|||||; JSESSIONID=abc61vSCzpF2xhumYp33w; ick_login=f9f873c2-206c-4c17-9cb9-ec4c7e3044d9; p=b178623a64102cc30833baf87c1c33f28; first_login_flag=1; t=ec055348320811e3b0b3345d15afe18c8; societyguester=ec055348320811e3b0b3345d15afe18c8; id=305523888; xnsid=8bff41c; loginfrom=syshome; jebe_key=b8a3f973-563c-4e6a-ac8f-99deef080f20%7Cdca572dcc866b00768c874af75fd79ec%7C1571811553654%7C1%7C1571811557213'
}
request = urllib.request.Request(url=url,headers=headers)
response = urllib.request.urlopen(request)
content = response.read().decode('utf-8')
with open('renrenwang.html','w',encoding='utf-8') as fp:
    fp.write(content)
```

```python
eg2 微博 注意防跨站攻击
import urllib.request
import urllib.parse

url = 'https://passport.weibo.cn/sso/login'
data = {
    'username': '18642820892',
    'password': 'lijing1150501',
    'savestate': '1',
    'r': 'https://weibo.cn/',
    'ec': '0',
    'pagerefer': 'https://weibo.cn/pub/?vt=',
    'entry': 'mweibo',
    'wentry': '',
    'loginfrom': '',
    'client_id': '',
    'code': '',
    'qq': '',
    'mainpageflag': '1',
    'hff': '',
    'hfp':'',
}
data = urllib.parse.urlencode(data).encode('utf-8')
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36',
'Referer': 'https://passport.weibo.cn/signin/login?entry=mweibo&r=https%3A%2F%2Fweibo.cn%2F&backTitle=%CE%A2%B2%A9&vt='# 此处判断用户是否从上一级页面跳转过来 不加上去则认为你提供了一个虚假的用户 从而防跨站攻击 不返数据
}

request = urllib.request.Request(url=url,headers=headers,data=data)
response = urllib.request.urlopen(request)
content = response.read().decode('utf-8')
print(content)
```

handler的基本使用

```python 
import urllib.request
url = 'http://www.baidu.com'
headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36'
    }
request = urllib.request.Request(url=url,headers=headers)

handler = urllib.request.HTTPHandler()
opener = urllib.request.build_opener(handler)
response = opener.open(request)
content = response.read().decode('utf-8')
print(content)
```

西次代理

```python
import urllib.request
url = 'http://www.baidu.com/s?wd=ip'
headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36'
    }

request = urllib.request.Request(url=url,headers=headers)
proxies = {'https':'218.22.7.62:53281'}
handler = urllib.request.ProxyHandler(proxies=proxies)
opener = urllib.request.build_opener(handler)
response = opener.open(request)
content = response.read().decode('utf-8')
with open('dali.html','w',encoding='utf-8')as fp:
    fp.write(content)
```

快代理

```python
import urllib.request
url = ''

response = urllib.request.urlopen(url)

content_ip = response.read().decode('utf-8')

```

动态获取cookie

```python 
eg 全书网
import urllib.request
import urllib.parse

url_post = ''

data = {}
data = urllib.parse.urlencode(data).encode('gbk')
headers = {}

request_post = urllib.request.Request(url=url_post,header=headers,data=date)

cookiejar = http.cookiejar.CookieJar()
handler = urllib.request.HTTPCookieProcessor(cookiejiar=cookiejiar)
opener = urllib.request.build_opener(handler)
response = opener.open(request_post)

url_get = ''
request_get = urllib.request.Request(url=url_get,headers=headers)
response = opener.open(request_get)
content = response.read().decode('gbk')
print(content)
```

