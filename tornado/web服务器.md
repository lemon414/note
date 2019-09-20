0.0.0.0 保留地址 是一个地址集合，指本机所拥有的使用地址



HTML 超文本标记语言

HTTP 超文本传输协议

​	-构建在长连接基础上的短连接协议

TCP ：

​	-建立连接：三次握手

​	-断开连接：四次挥手

​	-可靠

​	-长连接协议

UDP 短连接协议 在通信开始之前不需要建立相关的连接



# 最简单的HTML Server

```python
import socket

addr=('127.0.0.1',8000)
sock=socket.socket(socket.AF_INET,socket.SOCK_STREAM)#创建socket对象
sock.bind(addr)#绑定服务器地址
sock.listen(100)#设置监听队列大小100

# 定义响应报文
html=b'''
HTTP/1.1 200 OK#发给客户端的格式正确(下面空行不能省略)

<html>
	<head>
		<title>title</title>
	</head>
	<body>hello world</body>
</html>
'''
while True:
    print(‘服务器已运行，正在等待客户端连接’)
    cli_sock,cli_addr=sock.accept()#等待接受客户端连接,两个返回值，一个是客户端socket对象，第二个是客户端的地址。
    print('接收到来自客户端的 %是:%s 的连接' % cli_sock)

    cli_data=cli_sock.recv(1024)#接受客户端传来的数据,1024是接收缓冲区的大小
    print('接收到来自客户端发送来的请求报文：\n%s' % cli_data.decode('utf8'))
    
    cli_sock.sendall(html)#向客户端发送数据

    cli_sock.close()#断开与客户端的连接
```





# URL（统一资源定位符）

基本URL包含模式（或称协议）、服务器名称（或IP地址）、路径和文件名，如“协议：//授权/[路径](https://baike.baidu.com/item/%E8%B7%AF%E5%BE%84)查询”。完整的、带有授权部分的普通统一[资源](https://baike.baidu.com/item/%E8%B5%84%E6%BA%90)标志符语法看上去如下：协议：//用户名:密码@子域名.域名.顶级域名:[端口号](https://baike.baidu.com/item/%E7%AB%AF%E5%8F%A3%E5%8F%B7)/目录/文件名.文件后缀参数=值#标志。



# Web 框架

动态页面技术，所谓“动态”，并不是指放在网页上的GIF图片，动态网页技术有以下几个特点：

1. "交互性"，即网页会根据用户的要求和选择而动态改变和响应，将浏览器作为客户端界面,这将是今后WEB发展的大势所趋.
2. "自动更新"，即无须手动地更新HTML文档,便会自动生成新的页面，可以大大节省工作量.
3. "因时因人而变"，即当不同的时间，不同的人访问同一网址时会产生不同的页面。

常见的web框架：**Django、Flask、Tornado、**Bottle、web.py、Falcon、Quixote、Sanic

# tornado

```python
脚本文件
#!/usr/bin/env python
import tornado.web
class MainHandler(tornado.web.RequestHandler):
	def get(self):
		self.write("Hello, world")
def make_app():
	return tornado.web.Application([
		(r"/", MainHandler),
	])
	
if __name__ == "__main__":
	app = make_app()
	app.listen(8888,"127.0.0.1")
	loop = tornado.ioloop.IOLoop.current()
	loop.start()
```

```python
启动参数
from tornado.options import parse_command_line,define,options

define("host",default='0.0.0.0',help="主机地址",type=str)
define("port",default=8888,help="主机端口",type=int)

parse_command_line()
print('你传入的host：%s' % options.host)
print('你传入的port：%s' % options.port)
```



```python
路由处理
import tornado.ioloop
from tornado.web import RequestHandler,Application

class HomeHandler(tornado.web.RequestHandler):
    def get(self):
        self.write('欢迎进入主页')
        
class BookHandler(tornado.web.RequestHandler):
	def get(self):
		self.write('can i help you ')

app = Application([
    ('/',HomeHandler),
    ('/',BookHandler),
])

app.listen(8000)
tornado.ioloop.IOLoop.current().start()
```

```python
处理GEThernetPOST请求
class StoryHandler(tornado.web.RequestHandler):
    storise={1:'喜羊羊',2:'懒羊羊',3:'灰太狼'}
    
    def get(self):
        story_id=self.get_argument('story_id')
        story=self.stories[story_id]
        self.write("你喜欢%s这个人物" % story)
    def post(self):
        pass
```

HTTP的请求方法

| Method | Description|
| ------ | ------|
|POST |向指定资源提交数据进行处理请求, 数据被包含在请求体中。|
|GET |请求指定的页面信息,并返回实体主体。|
|PUT |从客户端向服务器、器传送的数据取代指定的文档的内容。|
|DELETE |请求服务器删除指定的⻚面。|
|HEAD |类似于GET请求只不过返回的响应中没有具体的内容,用于获取报头。|
|PATCH |是对PUT 法的补充,用来对已知资源进行局部更新 。|
|OPTIONS |允许客户端查看服务器的性能。|

# 总demo

```python
#!/usr/bin/env python

import tornado.ioloop
import tornado.web
from tornado.options import parse_command_line,define,options

define("host",default='localhost',help="主机地址",type=str)
define("port",default=8000,help="主机端口",type=int)

class MainHandler(tornado.web.RequestHandler):
    def get(self):
        self.write("hello world")  
        
class LemonHandler(tornado.web.RequestHandler):
    def get(self):
        self.write("我是一直柠檬精，嘤嘤嘤")        
        
class JiangpangpangHandler(tornado.web.RequestHandler):
    def get(self):
        self.write("姜伟老师爱跑步 ，每晚十公里")
        
class TestGetHandler(tornado.web.RequestHandler):
    def get(self):
        #接收URL中的参数
        name=self.get_argument('name')
        self.write("%每晚宝山体育馆约跑" % name)

class TestPostHandler(tornado.web.RequestHandler):
    def get(self):
        html='''
        	<forma action="/test/post" method="post">
        	姓名:<input type="text" name="name">
        	<br>
        	城市:<input type="submit">
        '''
        self.write(html)
        
    def post(self):
    	name=self.get_argument('name')
        city=self.get_argument('city')
        self.write('%s生活在%s' %(name,city))
        
 class make_japp():
    return tornado.web.Application([
        (r"/",MainHandler)
        (r"/foo",LemonHandler)
        (r"/test/get",JiangpangpangHandler)
        (r"/test/post",TestGetHandler)
    ])

if __name__=="__main__":
    parse_command_line()
    
    app=make_app()
    print('server running on %s:%ss' % (options.host,options.port))
    app.listen(options.port,options.host)
    
    loop = tornado.ioloop.IOLoop.current()
    loop.start()
```

