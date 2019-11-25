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


## MTV()

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


