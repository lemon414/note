# jQuery

一个开源的,优秀的javascript函数库(js框架),体积小,使用方便.方便对页面元素节点对象进行查找

Jquery=Javascript+Query(查询),意思是强大的DOM节点查询。

利用console.log(),js对象显示出来的是一个标签的样式,jquery单个对象显示出来的是init

jquery集合对象显示出来是 init(?),集合中存储的是js的单个对象,通过.get()方法获取标签

# jQuery中的选择器

## 1.基本选择器

- #id:根据元素的id属性获取指定的元素

- .class:根据元素的class属性获取指定的元素

- element：根据元素的名称获取指定的元素

- selector1,selector2：匹配所有满足条件的元素

~~~
<head>
<script src="./jquery-1.8.3.js"></script>
    <script>
        $(function(){
           $('#btn').click(function(){
           //id选择器
          $('#div').html('<h1>python</h1>');
           
           //根据元素名称选择
          $('div').html('<h1>python</h1>');

           //.class选择
          $('.style1').html('<h1>python</h1>')
     </script>
</head>
<body>
    <input id="btn" type="submit" value="点击">
    <div>
        <div id="div" class="style1"></div>
        <div>
            <p></p>
        </div>
        <a href=""></a>
        <b></b>
        <div></div>
        <div></div>
    </div>

</body>
~~~

## 2.层级选择器

- **ancestor (**空格**) descendant ：选取祖先元素下的所有后代元素(祖先与后代)**
- **parent > child**：选择父元素下的所有子元素（父子关系）
- **prev + next**：选取同级元素紧邻的下一个元素
- **prev~siblings**：选取同级元素所有的同级兄弟元素

~~~
//后代元素选择器
$('div p').html('<h1>python</h1>');
//子元素选择器
$('div>div>p').html('<h1>python</h1>');
~~~

## 3.简单选择器

- **:first**==>匹配第一个元素
- **:last**==>匹配最后一个元素
- **:even**==>匹配所有偶数,类似于下标,从0开始,0是偶数
- **:odd**==>匹配所有奇数
- **:eq(index)**==>匹配索引为index的元素(默认索引从0 开始)
- **:gt(index)**==>匹配索引大于index的元素
- **:lt(index)**==>匹配索引小于index的元素
- **:not(selector)**==>匹配除指定元素以外的其他元素

## 4.内容选择器

- **:contains(text)**:匹配内容包含指定文本的元素

- **:empty**:匹配内容指定为空的元素

- **:has(selctor)**:匹配具有指定元素的元素

- **:parent**:匹配具有子元素的元素(内容不为空的元素)

~~~
<head>
    <meta charset="UTF-8">
    <title>jquery02</title>
    <script src="./jquery-1.8.3.js"></script>
    <script>
        $(function(){
            var res= $('li:contains(魂)')
            var res =$('li:has(a)')
            var res =$('li:empty')
            var res =$(':not(:parent)')
            console.log(res)
        })
    </script>
</head>


<body>
    <ul>
        <li>咒怨</li>
        <li>午夜凶铃</li>
        <li><a >林中小屋</a></li>
        <li>招魂</li>
        <li></li>
    </ul>
    <ul></ul>
    <div></div>
    <span></span>
</body>
~~~

## 5.可见性选择器

- **hidden**-------->匹配所有隐藏元素(display:none,input type='hidden')
- **:visible**--------->匹配所有可见元素(display:block)

隐藏域不能使用show方法显示,只能通过修改type=''hidden''来实现显示

~~~
<script src="./jquery-1.8.3.js"></script>
<script>
        $(function(){
        //找到带有隐藏属性的标签
            var res=$(':hidden');
            console.log(res);
        //找到带有显示属性的标签
            var _res=$(':visible')
            console.log(_res)
        })
    </script>
</head>

<body>
    <input type="hidden" value="12345">
    <ul>
        <li style="display:none;">12345</li>
        <li>654321</li>
        <li>654321</li>
    </ul>
</body>
~~~

## 6.属性选择器

根据元素里面的属性进行选择

- **[attribute]**:匹配 具有指定属性的元素
- **[attribute=value]**:匹配属性值等于value的元素
- **[attribute!=value]**:匹配属性值不等于value的元素
- **[attribute^=value]**:匹配属性值以value开头的元素
- **[attribute$=value]**:匹配属性值以value结尾的元素
- **[attribute*=value]**:匹配属性值包含value的元素
- **[selectorN]**:匹配包含多个属性的元素

~~~
<head>
    <meta charset="UTF-8">
    <title>jquery03</title>
    <script src="./jquery-1.8.3.js"></script>
    <script>
        $(function(){   //当页面加载完成时
            $('[type=submit]')
            $('[type^=s][qwe=123]')
        })
    </script>
</head>

<body>
<form action="">
    <input type="text" name="account">
    <input type="text" name="pwd">
    <input type="radio" name="sex">
    <input type="checkbox" name="hobby">
    <input type="submit" value="点击" qwe='123'>
</form>
~~~

## 7.子元素选择器

## 8.表单选择器

- **:input**:匹配所有表单元素
- **:text**:匹配所有文本框
- **:password**:匹配所有密码框
- **:radio**: 匹配所有单选按钮
- **:checkbox**:匹配所有复选框
- **:submit**:匹配所有提交按钮
- **:reset**:匹配重置按钮
- **:image**:匹配图像域
- **:button**:匹配按钮
- **:file**:匹配文件域
- **:hidden**:匹配隐藏表单

## 9.表单属性选择器

- **-:enabled**:匹配所有可用元素

- **:disabled**:匹配所有不可用元素（即被禁用的元素）
- **:checked** :匹配复选框单选框所有选中元素(问题多)
- **:selected **:匹配下拉选框所有选中元素

~~~
<head>
	<script src="./jquery-1.8.3.js"></script>
	<script>
    $(function(){
        console.log($(':checked').get(0))
        console.log($(':selected').get(0))
        console.log($('：enabled').get(0))
        console.log($(':disabled').get(0))
    })
    </script>
</head>
<body>
 	<input type="checkbox" name="abc[]" value="1" checked>
    <input type="checkbox" name="abc[]" value="2" disabled>
    <input type="checkbox" name="abc[]" value="3">
    <input type="checkbox" name="abc[]" value="4">
    <input type="checkbox" name="abc[]" value="5">
    <select name="" id="">
        <option value="">1</option>
        <option value="">2</option>
        <option value="">3</option>
        <option value="">4</option>
        <option value="">5</option>
    </select>
</body>
~~~

# DOM对象与jQuery对象

使用document.getElementByIddocument.getElementsByTagName获取的对象就是dom对象。

使用$符号选择的元素就是jquery对象。

jQuery.get(0):将jQuery对象转成dom对象$('div')[0]或者$('div').get(0)

$():将括号里面的对象强制转换成jQuery对象

# jQuery中的属性

## 1.attr属性

只写参数不写值是获取值,又写参数又写值是赋值

- attr（name）:获取指定元素的属性
- attr（key，value）：设置元素的属性
- **attr（{key：‘value’，key：‘value，.....’}）**
- attr（key，fn）：通过函数的返回值设置元素属性
- **removeAttr（name）**：移除元素属性

## 2.class属性

- addClass（class）：为元素添加括号里的class属性

- removeClass(class)：删除括号里的属性

- **toggleClass(class)：切换样式**，如果元素不存在该属性则添加，存在则移除（类似与开关灯，如果本来是开着的，按一下就是关掉，如果开始是关着的，按一下则切换开。）
- hasClass(class)：判断某个元素是否具有某个css样式

## 3.css方法

- css(name):获取元素的样式属性    
- css(name,value):设置元素的样式属性
- css({name:'value',name:'value',.........}):同时设置多个样式属性

## 4.offset位置

- offset（）：获取元素的位置
- offset（{top：‘200px’，left：‘200px’}）设置元素的位置，离左边200px，上面200px

~~~
四种属性的运用案例
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jquery09</title>
    <style type="text/css">
        .one{width:100px;height:100px}
        .style1{width:200px;height:200px;background:blue;}
    </style>
    <script src="./jquery-1.8.3.js"></script>
    <script type="text/javascript">
        $(function t1(){
        //attr属性
            $('img').attr('src','2.jpg');
            alert($('img').attr('src'));
            $('img').attr('src','1.jpg');
            $('img').attr({src:'2.jpg',width:'300',height:'300'})
            $('img').removeAttr('src')

            //class属性
            $('#btn').addClass('one')
            $('#btn').removeClass('one')
            $('#btn').toggleClass('one')

            //css方法
            $('#two').css({width:'200px',height:'200px',background:'red',})

            //offset位置
            console.log($('#two').offset())//结果：{top: 412, left: 8}
            $('#three').addClass('style1')
            $('#three').offset({top:'200px',left:'200px'})

        })
    </script>
</head>
<body>
<input type="button" value="获取属性" id="btn" onclick="t1()" /><br />
<img src="1.jpg" width="300" />
<div id="two"></div>
<div id="three"></div>
</body>
</html>
~~~

## 5.元素的尺寸

- width（）：获取元素的宽度
- width（value）：设置元素的宽度
- height（）：获取元素的高度
- height（value）：设置元素的高度

## 6.文本域值

- **html（）**：获取元素的值（获取html标签里所有的元素值，如果里面有标签一样会被获取出来）
- html（val）：设置元素的值
- **text（）**：获取元素的值（与html不同的是，text值获取文本值，标签之类的不获取）
- text（val）：设置元素的值
- val（）：获取表单元素的值
- val（val）：设置表单元素的值

~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jquery10</title>
    <script src="./jquery-1.8.3.js"></script>
    <script>
        $(function(){
            console.log($('div').html())//获取元素的值，连标签一起获取 结果：<a>python 1905</a>
            $("#one").html("<p>你好</p>");//设置元素的值，覆盖了原先的python 1905
            console.log($('div').text())//获取元素的值，但只获取文本值 结果：python 1905
        })
    </script>
</head>
<body>
    <input type="button" value="获取元素文本内容">
    <p>12334556</p>
    <div id="one">
        <a>python 1905</a>
    </div>
</body>
</html>
~~~

# jquery中的事件

若没有引入jquery库，则会出现Uncaught ReferenceError: $ is not defined

## 1.页面载入事件

~~~
语法一
$(function(){      //当页面加载时
	//事件的处理程序
})

语法二
$().ready(function(){
	//事件的处理程序
})

语法三
$(document).ready(function(){
	//事件的处理程序
})
~~~

## 2.window.onload与ready的区别

## 3.一些常用的事件

~~~
blur(fn)：失去焦点时触发
change(fn)：状态改变时触发
click(fn)：点击时触发
dblclick(fn)：双击时触发
focus(fn)：获得焦点时触发
keydown(fn)：键盘按下时触发
keyup(fn)：键盘弹起时触发
keypress(fn)：键盘按下时触发
load(fn)：页面载入时触发，功能与ready类似
unload(fn)：页面关闭时触发
mousedown(fn)：鼠标按下时触发
mouseup(fn)：鼠标弹起时触发
mousemove(fn)：鼠标移动时触发
mouseover(fn)：鼠标悬浮时触发
mouseout(fn)：鼠标离开时触发
resize(fn)：调整大小时触发
scroll(fn)：滚动时触发
select(fn)：文本选中时触发
submit(fn)：表单提交时触发
~~~



## 4.事件切换

# 事件编程

## 1.绑定事件

绑定单个事件，type与fn用逗号，隔开bind（type，fn）

绑定多个事件，type与fn用冒号：隔开bind({type:fn,type:fn......})

绑定一个只执行一次就不在执行的事件，type与fn用逗号隔开one（type，fn）

移除绑定的事件unbind（type）

~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>blind</title>
    <style type="text/css">
        div{width:400px;height:200px;background:gold;}
    </style>
    <script src="./jquery-1.8.3.js"></script>
<!--    //绑定单个事件-->
    <script>
        $(function(){
            $('[type=button]').bind('click',function(){
                console.log('hello world');
            });
            $(':button').bind('click',function(){
                console.log('python 1905')
            })
        })
    </script>


<!--    //绑定多个事件-->
    <script>
        $(function(){
            $('div').bind({'mouseover':function(){
                $('span').html('鼠标滑过')
            },'mouseout':function(){
                $('span').html('鼠标离开')
            },'click':function(){
                alert('鼠标点击')
            }

            })
        })
    </script>

<!--    //one绑定一个只触发一次的事件-->
    <script>
        $(function(){
            $('#pinkpig').one('click',function(){
                console.log('登录中，请稍后')
            })
        })
    </script>


</head>
<body>
<input type="button" value="绑定事件">

<div></div>
<span></span>

<input type="button" value="登录一次" id="pinkpig">
</body>
</html>
~~~

## 2.绑定事件中的this对象

类似与python中类的self，谁调用就指的是谁

~~~
    <script>
        $(function(){
            console.log(this)
        })
    </script>
    this在在这里指的是document文档
~~~

# 动画及其效果

## 1.基本动画

show(speed,[callback])  显示

hide(speed,[callback])  影藏

speed：速度（动画的持续时间）

[callback]：事件完成时所触发的回调函数

toggle() ：切换显示或隐藏

toggle(switch) ：显示或隐藏true：显示false：隐藏

toggle(speed,[callback])：以动画效果切换显示或隐藏

## 2.滑动效果

slideDown(speed,[callback]) ：以动画效果向下滑动**显示**

slideUp(speed,[callback]) ：以动画效果向上滑动**隐藏**

slideToggle(speed,[callback]) ：以动画效果滑动**显示或隐藏**

## 3.淡入淡出

adeIn(speed,[callback]) ：以动画形式淡入（**显示**）

fadeOut(speed,[callback]) ：以动画形式淡出（**隐藏**）

fadeTo(speed,opacity,[callback]) ：设置元素的透明度 

opacity ：透明度（0-1） 0 全透明  1不透明

## 4.自定义动画

# 文档操作

## 1.在元素内部插入dom元素

> **A.append(B):**在A元素的内部的最后面加入B元素
>
> **B.appendTo(A):**将B元素插入到A元素的最后面

> **A.prepend(B):**在A元素的内部的最前面加入B元素
>
> **B.prependTo(A):**将B元素插入到A元素的最后面

## 2.在元素外部插入dom元素

>**A.after(B):**在A 的外面的后面添加B
>
>**B.insertAfter(A):**将B插入到A的外面的后面

> **A.before(B):**在A外部的前面添加B
>
> **B.insertBefore(A):**将B插入到A的外部的前面

## 3.删除操作

empty（）：清空元素内容，但节点保留下来了

remove（）：删除元素，包括节点和内容一起删除

## 4.复制操作

clone() ：克隆（复制）元素

clone(true)：克隆（复制）元素同时复制元素的事件

## 5.替换操作

- 值的替换：html（）；
- 标签的替换（当然连标签里的值一起替换了）：replaceWith（）；



 ~~~
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jquery02</title>
      <script src="./jquery-1.8.3.js"></script>
      <script type="text/javascript">
          $(function(){
              $("div").click(function(){
                  $(this).html('<h1>我的大刀早已饥渴难耐</h1>');
              })
  
               $(':button:eq(0)').click(function(){
                  $('div').replaceWith($('<strong>无极之道</strong>'));
              });
          });
  </script>
  </head>
  <body>
      <div><h2>蛮王六秒真男人</h2></div>
      <div><h2>蛮王六秒真男人</h2></div>
      <input type="button" value="节点替换操作"/>
  </body>
  </html>
 ~~~

## 6.包裹操作

用新的标签把原来的标签包裹起来

wrap（）：对每个元素进行单独包裹

wrapAll（）：把所有元素包裹成一个大包裹

~~~
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>jquery02</title>
<script <script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
	$("button").click(function(){
		$("p").wrap("<div></div>");
	});
});
</script>
<style type="text/css">
div{background-color:yellow;}
</style>
</head>
<body>

<p>这是一个段落。</p>
<p>这是另一个段落。</p>
<button>给每个P元素包裹一个div元素</button>

</body>
</html>
~~~

## 7.查找操作

>eq(index)：通过元素的索引查找元素，index默认从0开始
>
>filter(expr)：查找与给定元素匹配的元素，expr匹配条件
>
>not(expr)：查找与给定元素不匹配的元素
>
>children([expr])：查找所有子元素
>
>find(expr)：查找所有后代元素
>
>next([expr])：查找紧邻的下一个元素
>
>**nextAll();**查找紧邻的后面的所有元素
>
>prev([expr])：查找紧邻的上一个元素
>
>**prevAll();**查找紧邻的前面的所有元素
>
>parent([expr])：查找当前元素的父元素
>
>siblings([expr])：查找所有同级兄弟节点（无论上下）

隐藏域不能使用show方法显示,只能通过修改type=''hidden''来实现显示

基本选择器

层级选择器

简单选择器 first last not

内容选择器 contains

属性选择器

disable 禁用

只写参数不写值是获取值,又写参数又写值是赋值

A.append(B)      prepend   内部    在A内部加入B

B.appendTo(A)    prependTo     把B插入到A内部

# each方法

遍历jquery对象

协议只是一种规范，不是强制

回调函数，接收服务器返回的数据

# ajax

是一种在页面没有刷新的情况下，通过客户端（浏览器）与服务器交互的一种技术。页面不刷新完成请求。

~~~
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript">
$(function(){   //当页面加载时
        $("input[type=button]").click(function(){
                //写ajax的请求了
                $.ajax({
                    type:'get',   //get发送从服务器请求数据的请求只是用来查询一下数据，不会修改、增加数据，不会影响资源的内容，post向服务器端发送数据的，但是该请求会改变数据的种类等资源
                    dataType:'json'  //期待服务器返回的数据类型，最好是json
                    url:'php文件（见下）',   //所请求的数据所存在的服务器地址
                    success:function(msg){  //回调函数
                    //msg是从服务器端请求回来的数据。
                           console.log(msg)
                    }
                });
        });    
});
</script>


 <body>
       <input type="button" value="获取ajax请求数据"/><br/>
 </body>
~~~

~~~
//php文件
<?php
  	echo "大吉大利,今晚吃鸡!"，
?>
~~~

~~~
//ajax01.html文件
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax01</title>
    <script src="./jquery-1.8.3.js"></script>
    <script>
        $(function(){
            var div=$('div');
            div.css({width:'200px',height:'200px',background:'pink'})
            $.ajax({
                url:'ajax1_1.php',
                dataType:'json',
                type:'get',
                success:function(vscode){
                    div.text(vscode);
                }
            });
            div.click(function(){
               $.ajax({
                    url:'ajax1_2.php',
                    dataType:'json',
                    success:function(vscode){
                        div.text(vscode);
                }
               })
            });
            $('button').click(function(){
                var account=$('input[name=pwd]').val();
                var pwd=$('input[name=pwd]').val();
                var path='ajax1_2.php'
                $.ajax({
                    url:path,
                    type:'post',
                    data:{name:account,pwd:pwd},
                    success:function(msg){
                        div.text(msg)
                    }
                });
            });
        })
    </script>
</head>
<body>
    <table>
        <tr>
            <td>用户名:</td>
            <td><input type="text" name="account" placeholder="用户名/邮箱/手机"></td>
        </tr>
        <tr>
            <td>密码:</td>
            <td><input type="password" name="pwd" placeholder="密码"></td>
        </tr>
        <tr>
            <td><button>提交</button></td>
            <td><input type="reset" value="重置"></td>
        </tr>
    </table>
    <div></div>
</body>
</html>
~~~

~~~
//ajax1_1.php文件
<?php
	header('Access-Control-Allow-Origin:*'),
	$res = $_POST,

	var_dump($res),
?>
~~~

~~~
//ajax1_2.php文件
<?php
	header('Access-Control-Allow-Origin:*'),
	echo rand(1000,9999),
?>
~~~

