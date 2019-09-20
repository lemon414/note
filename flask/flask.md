200 两层判断正常
301 重定向
302 永久重定向
403 防跨站攻击 forbidden
404 路径错误
405 请求方式错误
500 服务器错误 业务逻辑错误 （你代码写错了）



常见一些默认端口号
mongodb:27017 mysql:3306 oracle:1521 redis:6379
ftp:21 ssh:22 http:80 https:443 



数据库和页面之间的数据的交互---web后端开发

核心代码的多少---重量级轻量级框架

flask轻量级框架，依赖两个外部库jinjia2(模板引擎)、Werkzeug (WSGI工具集)、Itsdangerous(签名模块)

```
  pip python专用的包管理工具
       pip install xxx 安装某一个软件
       pip uninstall xxx 卸载某一个软件
       pip list 列出所有的依赖包
       pip freeze 列出自己安装的所有的依赖包
       
  pip freeze 不列出pip本身依赖的包，而pip list会列出，所以比freeze多几个包。
```



## flask 流行的原因：

1.微型框架的形式给了开发者很大的空间
2.有非常好的扩展机制和第三方扩展环境，需要什么借什么
3.齐全的官方文档



 ## BS/CS的区别：

| 对象 | 网端   | 硬件环境                                     | 客户端要求                   | 软件安装                                    | 升级和维护                        | 安全性                                                       |
| ---- | ------ | -------------------------------------------- | ---------------------------- | ------------------------------------------- | --------------------------------- | ------------------------------------------------------------ |
| C/S  | 局域网 | 用户固定,处于相同区域,要求拥有相同的操作系统 | 客户端的计算机电脑配置要求高 | 客户端需要安装和配置软件                    | 每个客户端都要升级程序,可自动升级 | 面向相对固定的用户群，程序更加注重流程，可以对权限进行多层校验。提供更安全的存取模式。高度机密的信息系统采用 |
| B/S  | 广域网 | 要有操作系统和浏览器,与操作系统平台无关      | 客户端的计算机电脑要求较低   | 可以在任何地方进行操作,不需要安装专门的软件 | 不必安装及维护                    |                                                              |

## MVC（解耦合）

MVC将M(业务模型)和V(用户界面)实现代码分离，使同一个程序有不同的表现形式，C(控制器)存在的目的则是确保M和V的同步，一旦M改变，V应该同步更新。

高内聚 低耦合

Model  --模型 封装数据的交互操作
View --视图 用来将数据呈现给用户
Controller --控制器 接受用户输入输出 协调model和view的关系，对数据进行操作、删选

**MVC流程图**：
用户请求——>控制器 ——Model(调用模型，从数据库获取数据)—— View (展示数据) ——用户获得反馈  


## MTV(MVT)

M --模型,相当于MVC中的模型
T --模板，相当于MVC中的V视图
V --视图函数，相当于MVC中的C控制器



## 创建Flask项目

```
1.创建flask虚拟环境
virtualenv .虚拟环境名
source ~/项目文件地址/.虚拟环境名/bin/activate
pip install flask
pip install falsk-script
---------------------------------------------------
2.查看虚拟环境
	pip freeze
	pip list
---------------------------------------------------
3.虚拟环境迁移
	pip freeze > requirements.txt
		迁出
	pip install -r requirements.txt
		迁入
```

Flask项目创建

```python
Flask基本结构

from flask import Flask
         app = Flask(__name__)

        @app.route("/")
        def index():
            return "Hello"
        app.run()
```

   启动 python 文件名.py  默认端口5000 只允许本机连接

启动服务器参数修改

```
run方法中添加参数
	在启动的时候可以添加参数  在run（）中
	debug
		是否开启调试模式，开启后修改过python代码自动重启
		如果修改的是html/js/css 那么不会自动重启
	host
		主机，默认是127.0.0.1 指定为0.0.0.0代表本机ip
	port
		指定服务器端口号
	threaded
		是否开启多线程
```

**命令行参数**

```
	1.安装
		pip install flask-script
		作用
			启动命令行参数
	2.初始化
		修改  文件.py为manager.py
		manager = Manager(app=app)
		修改 文件.run()为manager.run()
	3.运行
		python manager.py runserver -p xxx -h xxxx -d -r
          参数
          - p  端口 port
          - h  主机  host
          - d  调试模式  debug
          - r  重启（重新加载） reload（restart）
```

**视图函数返回值**（字符串  render_template make_response() redirect Response ）

```
返回字符串
@app.route('/index/')
         def index():
            return 'index'
------------------------------------
模板渲染
@app.route('/first/')
         def hello():
            return render_template("test.html")
            
静态文件css
    <link rel="stylesheet" href="/static/css/hello.css">
```



## Flask基础结构

```
App
 	templates 里放模板
 	static 里放静态资源
 	views
 	models
```



## 蓝图

蓝图的创建和使用必须要在views视图文件里
蓝图是一种规划，主要用来规划urls(路由)
```
pip install flask-blueprint            --安装
blue=Blueprint('蓝图名',__name__)       --初始化蓝图
app.register_blueprint(blueprint=blue) --调用蓝图进行路由注册

```
## Flask请求流程（核心功能:路由分发）

浏览器请求路由——》route——》views(视图函数)——》models(视图函数和models交互)——》views(模型返回数据到视图函数)——》template(视图函数渲染模板)——》模板返回给用户



### 反向解析

概念：获取请求资源路径

语法格式：`url_for(蓝图的名字.方法名字)`

应用场景：

- redirect(url_for('blue.方法名'))  重定向的时候解决硬编码的问题而使用
- 页面中依然解决硬编码问题

```
redirect('/index/')------->redirect(url_for('blue.方法名'))
在重定向到index中，万一index的路径变了就无法重定向到了，这是使用反向解析来解决index的硬编码问题
```

# 视图函数

## 路由参数
路由参数没有变量名只有变量值，没有问号。
路由参数 `http://www.baidu.com/s/1/`
请求资源路径参数 `https://www.baidu.com/s?wd=韩红`

路由参数的类型默认是字符串

类型有：`string  path  int  float  uuid  any`

- 路由参数的基本结构 /资源路径/<变量>/
- 路由参数的访问路径 http://127.0.0.1:5000/testroute/id/  其中这个id是字符串类型
- 路由参数的名字一定要和视图函数的参数一致
- 路由参数传到视图函数，是一个字符串类型

```
# -------------------string--------------------
@blue.route('/testroute1/<string:name>/')
def testroute1(name):
    print(name)
    return 'testroute1'


# --------------------path---------------------
@blue.route('/testroute2/<path:name>/')
def testroute2(name):
    print(name)
    return 'testroute2'


# --------------------int---------------------
@blue.route('/testroute3/<int:money>/')
def testrooute3():
    return 'testroute3'

# --------------------float-------------------
@blue.route('/testroute4/<float:money>/')
def testroute4(money):
    return '1'


# --------------------uuid--------------------
@blue.route('/testuuid/')#----生成uuid
def testuuid():

    uid = uuid.uuid4()
    print(uid)

    return 'testuuid'

@blue.route('/testRoute5/<uuid:uid>/')
def testRoute5(uid):
    print(uid)
    print(type(uid))
    return 'testRoute5'

# ---------------------any-------------------
@blue.route('/testroute6/<any(a,b):p>/')
def testroute6(p):
    return 'testroute6'
```

string和path的区别：string遇见/就会结束，而path会将/只当做一个字符串处理

## 请求方式

请求方式又叫做http方法

get(获取) post(添加) delete(删除) put(修改全部属性) patch(修改部分属性)

路由默认只支持 get head options请求方式 不支持post delete put patch 
如果想让路由支持post delete put patch 可以在route方法中添加一个参数 methods['post','delet','put']

```
@blue.route('/toLogin/')
def toLogin():
    return render_template('login.html')

@blue.route('/login/',methods=['post','delete'])
def login():
    return '欢迎光临红浪漫,拖鞋手牌拿好,楼上二楼左转,男宾3位'
```



## 路由路径







## request及其属性

request是一个内置对象

`method  base_url host_url url remote_addr files headers path cookies session`

```
（1）request是一个内置对象
	内置对象：不需要创建就可以直接使用的对象
（2）属性
	1.method      （请求方法）
	2.base_url    （去掉get参数的url）	
	3.host_url    （只有主机和端口号的url）	
	4.url         （完整的请求地址）
	5.remote_addr （请求的客户端地址）  
	6.request.args.get('name')
      args  **
           - args
           - get请求参数的包装，args是一个ImmutableMultiDict对象，类字典结构对象
           - 数据存储也是key-value
           - 外层是大列表，列表中的元素是元组，元组中左边是key，右边是value
           注意： 一般情况下  get请求方式都是在浏览器的地址栏上显示
                 eg：http：//www.baiduc.com/s?name=zs&age=18
                 结果：zs
                 获取get请求方式的参数的方式：
                 
     7.request.form.get('name')
       form   **
           - form
           - 存储结构个args一致
           - 默认是接收post参数
           - 还可以接收 PUT，PATCH参数
           - 一般情况下 post请求方式都是通过表单形式使用的
           注意：eg：
                    <form action='xxx' method='post'>
                        <input type='text' name='name'>
                     获取post请求方式的参数的方式
	 8.files       (文件上传)	
	 9.headers	   (请求头)
	 10.path       (路由中的路径)	
	 11.cookies    (请求中的cookie)
	 12.session	   (与request类似  也是一个内置对象  可以直接打印 print（session）)
```



```
@blue.route('/testRequest/')
def testRequest():
    print(request.method)  # 获取请求方式/http方法
    print(request.base_url) # 去掉请求参数后的请求资源路径
    print(request.host_url)  # 只有主机和端口号的url
    print(request.url)  # 完整的请求地址url路径（请求资源路径 请求参数）
    print(request.remote_addr)  # 主机地址、客户端地址，反爬虫
    print(request.files)  # 文件上传
    print(request.headers)  # 请求头
    print(request.path)  # 请求资源路径，路由中的路径
    print(request.cookies) #获取请求的cookies
    return 'testrequest'
```

```
 # http://127.0.0.1:5000/testRequest/?name=zs&age=18
    # 怎么获取name的值
    print(request.args)
    
    name = request.args.get('name')
    print(name)
    
    age = request.args.get('age')
    print(age)

    age1 = request.args.getlist('age')
    print(age1)
-------------------------------------------------------
 # http://127.0.0.1:5000/testRequest/?name=zs&age=18
    # 获取post请求的参数
    name2 = request.form.get('name')
    print(name2)

    age2 = request.form.get('age')
    print(age2)

    age3 = request.form.getlist('age')
    print(age3)

    return 'testRequest'
```



## response（视图函数返回值）

两大类 字符串 和 response

- 字符串
- render_template
- make_response()
- redirect
- Response

```python 

from flask import Blueprint, render_template, url_for, request, make_response, redirect, Response,
#-------返回字符串-------------
@blue.route('/testResponse1/')
def testResponse1():
    return 'hello world'

#-------返回一个模板----------
@blue.route('testResponse2')
def testResponse2():
    s = render_template('文件名.html')
    print(type(s))#是一个方法
    return s

#------返回make_response()--------
@blue.rooute('/testResponse3/')
def testResponse3():
    return = make_response('<h1>hahahaha</h1>')


#------返回redirect------------
# 视图函数返回redirect
@blue.route('/index/')
def index():
    return 'welcome to BeiJing'

@blue.route('/testResponse4/')
def testResponse4():
    r = redirect(url_for('blue.index'))
    return r 
    
#-------返回Response--------------
#视图函数返回response()
@blue.route('/testResponse5/')
def testResponse5():
    r = Response('阿丑')
    return r
```



## 异常

```
@blue.route('/testAbort/')
def testAbort():
    abort(404)
    return 'testAbort'


@blue.errorhandler(404)
def testAbort1(Exception):
    return '系统正在升级，请稍后再试'
```



## 会话技术

1.请求过程Request开始，到Response结束
2.连接都是短连接
3.延长交互的生命周期
4.将关键数据记录下来
5.Cookie是保存在浏览器端/客户端的状态管理技术
6.Session是服务器端的状态管理技术

### cookies（客户端会话技术）

所有数据存储在客户端，以key-value进行数据存储，服务器不做任何存储
支持过期时间

**cookies**
设置cookie：response.set_cookie('username',)

删除cookie：response.delete_cookie('username')

获取cookie：username=request.cookies.get('usernamae','游客')

```
cookie的使用
需求：执行一个视图函数tologincookie  跳转到一个页面logincookie.html
     输入一个用户名字xxx  点击提交  跳转到welcomecookie.html
     该页面的内容是 欢迎xxx光临red romance。。。。
     如果没有经过登录  直接跳转到welcomecookie.html 会显示 欢迎游客光临
     如果已经登录然后跳转到welcomecookie.html 那么在欢迎xxx的下面
     还有一个退出  然后退出  跳转到welcomecookie.html页面
     显示 欢迎游客。。。
```

```python
view.py文件内容
@blue.route('/tologincookie/')
def tologincookie():
    return render_template('logincookie.html')

@blue.route('/logincookie/',methods=['post'])
def logincookie():
    # ‘name’ 是input标签的name的属性值
    name = request.form.get('name')

    response = redirect(url_for('blue.welcomecookie'))
    # response = redirect('/welcomecookie/')
    # 设置cookie必须要有response对象   那么response对象的获取有三种方式
    # 分别为make_response，redirect,Response()
    # 如果我们选择make_response方法  那么make_response('<>')  x
    # 如果我们选择Response方法      那么Reseponse('fdffdf')   x
    # ‘name’  key值  可以随便定义
    #  name   在前端获取的name值
    response.set_cookie('name',name) --设置cookie必须有response，因此上面是获取response来为此句cookie的创建。

    return response

@blue.route('/welcomecookie/')
def welcomecookie():

    # 获取cookie中的name
    # ‘name’ cookie的key值
    name = request.cookies.get('name','游客')

    return render_template('welcomecookie.html',name=name)



@blue.route('/logoutcookie/')
def logoutcookie():

    response = redirect(url_for('blue.welcomecookie'))

    response.delete_cookie('name')
    return response
```

### session(服务端会话技术)

**所有数据以键值对的形式默认存储在服务器的内存中**
单纯的使用session会报错，需要在__init__方法中配置`app.config['SECRET_KEY']='110'`

设置 `session['username']=username`

获取 `session.get('username')`

删除 `session.pop('username')`

```
session持久化,因为session默认存储在内存中，关机就消失。所以要持久化
1.安装插件  pip install flask-session
2.初始化session对象
	(1)持久化的位置
		配置init中
		app.config['SECRET_KEY']='110'#赋予持久化所需权限
		app.config['SESSION_TYPE']='redis'#持久化的位置
		app.config['SESSION_KEY_PREFIX']='xxxx'#设置前缀
	(2)初始化创建session对象的两种方式 --Sessiona(app=app)
					               --se=Session()  se.init_app(app=app)
	(3)安装redis 
		pip install redis
        启动redis redis-server
	(4)需要配置SECRET_KEY='110'
		注意：flask把session的key存储在客户端的cookie中，通过这个key可以从flask的内存中获取用户的session信息，出于安全性考虑，使用secret_key进行加密处理。所以需要先设置secret_key的值。
	(5)查看redis的内容
		启动redis redis-server
		redis-cli
		key *
		ttl session :xxxxxxxxxxxxx  --查看session生存时间
		
```

flask的session的生存时间是31天，django的session生存时间是15天