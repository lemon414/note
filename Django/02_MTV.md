# MTV--M

django会为表增加自动增长的主键列，每个模型只能有一个主键列，如果使用选项设置某属性为主键列后，则django不会再生成默认的主键列

## 数据级联

一对多模型关系

隐性属性

显性属性

```python
一对多模型关系：
	class Grade(models.Model):
      g_name = models.CharField(max_length=32)

    class Student(models.Model):
          s_name =models.CharField(max_length=16)
          s_grade=models.ForeignKey(Grade) 
案例：(1).多方获取一方，根据学生找班级名字
	  显性属性：就是你可以在中直接观察到的属性---》通过多方获取一方  那么可以使用多方调用显性属性直接获取一方数据
      student = Student.objects.get(pk=2)
	  grade = student.s_grade
	  return HttpResponse(grade.g_name)
	 (2).一方获取多方，根据班级  找所有的学生
      隐性属性：就是我们在类中观察不到的，但是可以使用的属性---》通过一方获取多方 那么可以使用一方数据的隐性属性 获取多方数据
	  grade = Grade.objects.get(pk=2)
	  students = grade.sutdent_set.all()
	  content = {
			'students':students
			}
	  return render(request,'students_list.html',content)
```



## 定义字段

### 1)字段类型

- AutoField  自增长。如果不指定，Django里主键字段将自动添加到模型中

- CharField(max_length=32)  字符串，默认的表单样式是 TextInput

- TextField  大文本字段，一般超过4000使用，默认的表单控件是Textarea

- IntegerField  整数

- DecimalField(max_digits=None, decimal_places=None)  十进制浮点数参数1位数总数 参数2小数点后的数字位数

- FloatField  浮点数

- BooleanField  true/false

- NullBooleanField  支持null、true、false三种值

- DateField([auto_now=False, auto_now_add=False])

  - DateField.auto_now:每次保存对象时，自动设置该字段为当前时间，用于"最后一次修改"的时间戳，它总是使用当前日期，默认为false
  - DateField.auto_now_add:当对象第一次被创建时自动设置当前时间,用于创建的时间戳，它总是使用当前日期，默认为false

  注意：auto_now_add, auto_now, and default 这些设置是相互排斥的，他们之间的任何组合将会发生错误的结果

- TimeField  使用Python的datetime.time实例表示的时间，参数同DateField

- DateTimeField  使用Python的datetime.datetime实例表示的日期和时间，参数同DateField

- FileField  一个上传文件的字段

- ImageField  继承了FileField的所有属性和方法，但对上传的对象进行校验，确保它是个有效的image

### 2)字段选项(约束)

- null  如果为True，Django 将空值以NULL 存储到数据库中，默认值是 False
- blank  如果为True，则该字段允许为空白，默认值是 False

注意：null是数据库范畴的概念，blank是表单验证证范畴的

- db_colunm  字段的名称，如果未指定，则使用属性的名称
- de_index  若值为 True, 则在表中会为此字段创建索引
- default  ·默认值
- primary_key  主键
- unique  唯一值

## 创建对象

```python
----models.py文件中先创建模型然后迁移成数据库中的表----
class Person(models.Model):
    name=models.CharField(max_length=16)
    age=models.IntegerField()
```

在表的基础上，对这个表进行对象的创建的四种创建方式举例

```python
----------views.py中定义视图函数-----------
def addPerson(request):
#第一种创建方式
    person=Person()
    person.name='lucy'
    person.age=18
    person.save()
    
#第二种创建方式
	person=Person(name='tom',age=19)
    person.save()
    
#第三种创建方式
	person=Person.objects.create(name='chris',age=20)
    person.save()
	
    return HttpResponse('添加person成功')
```







## 查询(返回QuerySet类型数据)

查询集：表示从数据库获取的对象集合，查询集可以有多个过滤器。
过滤器：过滤器就是一个函数，基于所给的参数限制查询集结果，返回查询集的方法称为过滤器。

## 查询集

1.**all**  查询所有 格式： `模型.objects.all()`

2.**filter**  返回符合筛选条件的数据集  `模型.objects.filter(条件)`

3.**exclude**  返回符合条件以外的数据集  `模型.objects.exclude(条件)`

4.**order_by** 默认根据id排序  `模型.objects.order_by('id')`

5.**values**

6.**切片**  限制查询集 利用下标的方法 左闭右开区间 下标没有负数 相当于limit offset

  `eg：studentList = Student.objects.all()[0:5]  第一个参数是offset  第二个参数是limit`

7.**懒查询/缓存集**
查询集的缓存：每个查询集都包含一个缓存，来最小化对数据库的访问,在新建的查询集中，缓存首次为空，第一次对查询集求值，会发生数据缓存，django会将查询出来的数据做	一个缓存，并返回查询结果，以后的查询直接使用查询集的缓存。**都不会真正的去查询数据库.**
懒查询:只有我们在迭代结果集，或者获取单个对象属性的时候，它才会去查询数据,为了优化我们结果和查询.

链式调用：多个filter和exclude可以连接在一起查询
`eg:Person.objects.filter().filter().xxxx.exclude().exclude().yyyy`

## 查询
#### 获取单个对象

```
获取单个对象：
	get
		不存在会抛异常  DoesNotExist
		存在多于一个 MultipleObjectsReturned
		使用这个函数 记得捕获异常
	last
		返回查询集种的最后一个对象
	first
		需要主动进行排序
		persons=Person.objects.all().first()
	内置函数：框架自己封装得方法 帮助我们来处理业务逻辑
		count
			返回当前查询集中的对象个数
				eg：登陆
		exists
			判断查询集中是否有数据，如果有数据返回True没有反之
```



#### 字段查询

```
字段查询：
	对sql中where的实现，作为方法filter(),exclude(),get()的参数
	语法:属性名称__比较运算符=值
		Person.objects.filter(p_age__gt=18)
	条件
		属性__操作符=临界值
		gt
			great than
		gte
			great than equals
		lt
			less than
		lte
			less than equals
		gt,gte,lt,lte：大于，大于等于，小于小于等于filter(sage__gt=30)
		in
			in：是否包含在范围内,filter(pk__in=[2,4,6,8])
				单引号可以使用
		exact*******
			exact：判断，大小写不敏感，filter(isDelete = False)
		startswtith
			类似于 模糊查询 like
		endswith
			以 xx 结束  也是like
		contains
			contains：是否包含，大小写敏感，filter(sname__contains='赵')
		isnull,isnotnull
			isnull,isnotnull：是否为空，filter(sname__isnull=False)
		ignore 忽略大小写
			iexact********************
			icontains
			istartswith
			iendswith
			以上四个在运算符前加上 i(ignore)就不区分大小写了 iexact...
```



#### 时间





#### 聚合函数



#### 跨关系查询

两个表只要有联系，其中一个表就可以直接调用另一张表的属性

```python
class Grade(models.Model):
    g_name=models.CharField(max_length=16)
    
class Student(models.Model):
    s_name=models.CharField(max_length=16)
    s_grade=models.ForeignKey
    
应用：查询名字为zs所在的班级
    普通查询
    student=Student.objects.filter(s_name='zs')[0]
    name=student.s_grade.g_name
    print(name)

    跨关系查询
    grade=Grade.objects.filter(student__s_name='zs')[0]
    print(grade.id,grade.g_name)
    return HttpResponse('hello world')
这里在筛选班级的条件里直接调用了学生表里面的属性


```

 

#### F对象(表内比较)

```
F对象 eg：常适用于表内属性的值的比较
	模型：
		class Company(models.Model):
              c_name = models.CharField(max_length=16)
              c_gril_num = models.IntegerField(default=5)
              c_boy_num = models.IntegerField(default=3)
	F：
		获取字段信息，通常用在模型的自我属性比较，支持算术运算
	eg:男生比女生少的公司
	companies = Company.objects.filter(c_boy_num__lt=F('c_gril_num'))
	eg:女生比男生多15个人
	companies = Company.objects.filter(c_boy_num__lt=F('c_gril_num')-15)
```



#### Q对象(支持逻辑运算)

```
Q对象 eg：常适用于逻辑运算 与或或
		年龄小于25：
            Student.objects.filter(Q(sage__lt=25))
        eg:男生人数多余5 女生人数多于10个：
             companies = Company.objects.filter(c_boy_num__gt=1).filter(c_gril_num__gt=5)
             companies = Company.objects.filter(Q(c_boy_num__gt=5)|Q(c_gril_num__gt=10))
        支持逻辑运算：与或非、&、|、~
        年龄大于等于的：
					Student.objects.filter(~Q(sage__lt=25))
```




# MTV--T  templates模板

## Templates(加载 渲染)







##  模板语法

### 1）变量

视图传递给模板的数据，获取视图函数传递的数据使用{{ var }}接收。如果变量不存在，则插入空字符串。

变量的来源：视图中传递过来的或者标签中，逻辑创建出来的。

### 2）模板中的点语法

### 3）标签

分为单标签和双标签，双标签必须闭合。

```html
eg:{% for 变量 in 列表 %}
        语句1 
        	{% empty %} --判断之前的代码有没有数据 如果没有显示empty下面的代码
        语句2
        {% endfor %}
```

```
注释：
          单行注释
              {#  被注释掉的内容  #}
          多行注释
              {% comment %}
              内容
          	  {% endcomment %}
```



### 4）过滤器

```
	|
	将前面的输入作为后面的输出
	add：
		<h4>{{ count|add:2 }}</h4>
		<h4>{{ count|add:-2 }}</h4>
	upper：
	lower：
	safe
		确认安装
		进行渲染
		eg:
              code = """
                  <h2>睡着了</h2>
                  <script type="text/javascript">
                      var lis = document.getElementsByTagName("li");

                      for (var i=0; i< lis.length; i++){
                          var li = lis[i];
                          li.innerHTML="日本是中国领土的一部分!";
                      }
                  </script>
                   """
	endautoescape：
		{% autoescape off%}
			code
		{% endautoescape %}
```



### 5）结构标签

### 6）加载静态资源





# MTV--V  view视图函数

概念：视图函数MTV中的View，相当于MVC中的Controller作用，控制器 接收用户输入（请求）。

## 视图函数返回值

- (1)Josn数据 应用于前后端分离
- (2)网页形式
  - HttpResponse
  - render
  - redirect







## 路由参数(见day03笔记)

### 1）基本使用

### 2）路由位置参数

### 3）路由关键字参数

### 4）内置函数



  





## 反向解析

获取请求资源路径，避免硬编码

### 1）实现步骤

​	1.在根路由上添加namespace参数
	2.在子路由中添加name参数
	3.在模板中使用 调用的时候 反向解析的路径不能有编译错误  格式是  {% url 'namespace:name%}'

### 2）基本应用

### 3）反向解析的位置参数

### 4）反向解析的关键字参数



## Request对象

是Django框架根据http请求报文自动生成的一个对象，包含了各种请求信息。

request的一些属性：

​	- path 请求的完整路径
	- method 获取请求的方式 
	- encoding 编码
	- META 应用反爬虫	
	-request.GET.get() 获取get请求参数的方法，返回的结构<QueryDict {'name': ['zs']}>如果是重复的变量  那么会接受后面的那个数据

​	-request.POST.get() 获取post请求参数的方法

 ```
   queryDict 和Dict的区别？
   dict是字典对象，没有urlencode()方法；
    QueryDict对象，有urlencode()方法，作用是将QueryDict对象转换为url字符串；
    queryDict默认的value值是一个列表
    dict的默认value值是一个字符串

 ```

```
def testRequest(request):
--# 请求完整资源路径
    # 应用场景： 判断某请求是否在某请求列表下
    #  REQUEST_LIST = ['/cart/']
    #  if request.path in REQUEST_LIST:
    print(request.path)

--# 获取请求方式
    print(request.method)
```



## HttpResponse对象

### html响应
render  redirect 

### JsonResponse

