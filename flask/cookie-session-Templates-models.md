# Templates

MVT中的Templates，MVC中的View
主要用来做数据展示的
模板处理过程分为两个阶段  加载和渲染

jinjia2模板引擎的优点：速度快，被广泛使用、HTML设计和后端Python分离、减少Python复杂 度、非常灵活，快速和安全、提供了控制，继承等高级功能。



## 模板之间的操作（day03/test）

基模块和子模块之间的继承和包含、宏定义、循环控制、过滤。

extends 继承

include 包含，将一个指定的模板包含进来



```html
#宏定义 对应testMacro.html
@blue.route('/testMacro/')
def testMacro():
    return render_template('testMacro.html')


{#无参的macro#}
    {% macro say() %}
        德玛西亚
    {% endmacro %}

    {{  say() }}
    <br>
    {{  say() }}

{#有参数的macro#}
    {% macro getUser(name,skill) %}
        {{ name }}的技能是{{ skill }}
    {% endmacro %}

    {{ getUser('无极剑圣','阿尔法突袭') }}
---------------------------------------------------------------------------


#循环控制
@blue.route('/testFor/')
def testFor():
    score_list = [59, 67, 85, 40, 100]
    return render_template('testFor.html', score_list=score_list)


#过滤器
语法格式：{{ var|xxx|yyy|zzz }}
lower  upper  trim  reverse  striptags  safe
{% for c in config %}
                    <li>{{ loop.index0 }}:{{ loop.index}}:{{ c|lower|reverse }}</li>
    		{% endfor %}
    
```

# models

可以有效减少重复SQL、设计灵活，可以轻松实现复杂查询、性能损耗少、移植性好

## sqlalchemy（通过操作对象来操作数据）

基本配置

1.	pip install flask-sqlalchemy

	创建sqlalchemy对象：

- models文件里面：db=SQLALchemy()

- __init__文件里面：

  - app.config[‘SQLALCHEMY_TRAKE_MODIFICATIONS’]=False

  - db.init_app(app=app)

  - app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://zcg:zcg1110@localhost:3306/已经创建的数据库名'

`config中配置  SQLALCHEMY_DATABASE_URI 数据库 + 驱动 :// 用户:密码@ 主机:端口/数据库`
3.执行

​	view 中db.create_all()

4.使用

```
# 通过模型创建表 --db.create_all()
@blue.route('/createTable/')
def createTable():
    db.create_all()
    return '创建成功'

# 通过模型删除表--db.drop_all()
@blue.route('/dropTable/')
def dropTable():
    db.drop_all()
    return '删除成功'

# 通过模型添加数据-- db.session.add(对象)、db.session.commit()
@blue.route('/addanimal/')
def addanimal():
    a = Animal()
    a.name = 'hen'
    a.color = 'yellow'
    db.session.add(a)
    db.session.commit()
    return '添加成功'

@blue.route('/findall/')--模型.query.all()
def findall():
    animal_list = Animal.query.all()

    for animal in animal_list:
        print(animal.name)
    return '查询成功'
```













# 模型迁移

模型——》表

1.pip install flask-migrate

2.ext
	migrate=Magrate()
	migrate.init_app(app=app,db=db)
	
3.manager
	manager.add_command('db',MigrateCommand)

4.如果之前没有migrations的文件夹 那么必须先init，但是如果有这个文件夹 那么就不需要init了
	python manager.py db init
	python manager.py db migrate
	python manager.py db upgrade
	python manager.py db downgrade







# DML

DDL 数据定义语言 针对表操作 create alter drop

DML 数据操纵语言 针对数据操纵 insert delete update

DQL 数据查询语言 select

TCL 事务 commit   rollback

```python
db.session.add()--增加一个对象
db.session.add_all()--增加多个对象
db.seesion.delete()--删除一个对象

----------修改一个对象
@blue.route('/updateStudent/')
def updateStudent():
    s=Student.query.first()
    s.name='红方小兵'

    db.session.add(s)
    db.session.commit()
    return '修改成功'
先查询出来然后对修改的名字重新定义，然后直接重新添加这个对象就行了


xxx.query.get(主键属性)--通过主键来查询获取单个数据
xxx.query.first()--获取第一个主键的值
xxx.query.all()--获取所有结果集
xxx.query.filter(过滤条件)--通过筛选出所想要的结果集

xxx.query.order_by('属性名')--通过排序
limit(num)--选取前num个数据
offset(num)--跳过num个数据
limit(num).offset(num2)--跳过num2条获取接下来的num1条数据
limit offset 优先级offset先生效
```

先排序后分页



