# html

## 1.网络结构

C/S 终端/服务器（发送请求 响应请求 下载文件 ）

B/S 浏览器/服务器

## 2文件结构

```
<！DOCTYPE html>不是HTML标签；它告诉浏览器页面使用的是HTML什么版本。这里默认h5
<html></html>：表示一个网页。有两个子标记<head>和<body>
<title>网页标题</title>:表示网页的标题，其内容只能是纯文本。
<meta charset="utf-8" />：设置字符集，表示用什么编码解析。
<body>正文内容</body>。
```

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">  
    <title>Title</title>
</head>
<body></body>
</html>
```

HTML标记只能顺序嵌套，不能交叉嵌套。

## 3.文本修饰标记

```
<b></b>:文本加粗
<i></i>:文本斜体`
<u></u>:下划线
<s></s>:删除线(strike)
<sup></sup>:上标
<sub></sub>:下标
<font color='blue' face='楷体' size='7' face='楷体'></font>:文本字体
```

## 4.排版标记

```
<p>:段落，在段前或段后，会有一个空行
<p align='center'>我在中间</p>

<br />：换行标记，行间距不会发生任何改变

<hr />水平线标记

<pre></pre>：原来怎么样就输出什么样，原封不动的输出

<input type="text"/>：输入框，相当于网站上的输入密码的框框。

```

## 5.块元素div和行内元素span

```
<div>`和`<span>`是两个最没有意义的标记
```

块元素`单独占一行`，不管有多少内容。常用的块元素有<p>、<h1>、<h2>、<h3>、<pre>、<div>、<table>

等。

多个行内元素排在同一行.常用的行内元素有<font>、<b>、<i>、<u>、<sup>、<sub>、<span>等.

注意事项：行内元素和块元素，`相互嵌套时，块元素中嵌套行内元素`。

#### 字符实体

&copy：版权号

空格：&nbsp

```
import html
print(html.escape('<div>'))#&lt;div&gt;
```



#### HTML中的列表 块元素

```
<!--ul>li*5表示ul里面有五个li-->
ul*5>li*5表示五个ul里每个都包含五个li
```

ul 无序列表

ol 有序列表

dl 自定义列表

#### 滚动字幕

```
<marquee direction='left' width='400px' height='300px' bgcolor='#ffff66' scrollAmount='100' scrollDelay='40'>
<p>我是漂浮物</p>
</marquee>
```



#### 图片标记 行内元素

```
<img src='images_2/qf_01.jpg' width='40%' border='2' align='left'/>

src：指图片的路径，该路径可以是相对地址，也可以是绝对地址。
alt：图片说明。当图片不存在时，显示一个提示信息。
```

#### 超链接 行内元素

```
<a href="http://www.baidu.com" target="_blank">百度</a>

href：链接的地址，默认_blank
target：链接的目标文件在哪个窗口中来打开。target_blank：弹出一个空白窗口来打开文件。
target_self：在当前窗口中来打开目标文件。
```



注意事项：以 `http://` 开头的网址，就是“绝对路径”

​                   以 file:/// 协议开头的网址，也是“绝对路径”

## 6.锚点链接

锚点链接：可以实现在一个网页的不同部分实现跳转，用在长网页当中(`一定要有滚动条`)。相当于淘宝软件中的返回顶部。

定义锚点(记号):`<a  name = “top"></a>

跳转到锚点(记号)：<a  href = “#top">返回顶部</a>



## 7.meta标记

http-equiv：模拟HTTP协议的文件头信息。一般要与content属性配合使用。

   1）设置网页的类型和字符集

   2）网页自动刷新，以及延时跳转

```
<meta http-equiv="refresh" content="2">   //每隔2秒，刷新网页一次
<meta http-equiv="refresh" content="5;url=http://www.ifeng.com">  //5秒钟后，跳转到凤凰网
```

name：指定网页的描述信息。一般要与content属性配合使用。

设置网页关键字

```
<meta name="keywords" content="游戏，二次元，热血，战斗" />
```

content属性：指定参数的详细信息。

###### 适应手机各种移动端：

```
适应手机各种移动端：
<meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0,maximum-scale=1.0,user-scalable=0"/>
```



## 8.表格标签

```
<!--table>td*3>tr*3表示表格三行三列-->
<table>代表表格标记。<tr>代表行标记。<td>普通单元格。<th>代表标题行，其中的内容居中加粗显示。
```

1.table属性

border：边线粗细。
bordercolor：边线颜色。
width：表格宽度。
height：表格高度。
align：水平对齐方式，取值：left、center、right
bgColor：背景颜色
background：背景图片
rules：合并所有单元格边线。取值：all
cellpadding：内填充距离(单元格边线到内容间的距离)
cellspacing：单元格间距(两个单元格边线之间的距离)

2.tr属性

height：行高。
bgColor：背景色
background：背景图片
align：水平对齐方式，取值：left、center、right
valign：垂直对齐方式，取值：top、middle、bottom

3.td属性

width：单元格宽度。
height：单元格高度。
bgColor：背景色
background：背景图片
align：水平对齐方式
valign：垂直对齐方式
colspan：合并列的单元格。
rowspan：合并行的单元格。

4.caption表格标题

含义：给表格添加一个标题。
语法：<caption>……</caption>
说明：<caption>标记，放在<table>开始标记之后，所有的<tr>标记之前。一个表格只能有一个<caption>标记。

## 9.音频标签和视频标签和flash标签

1.音频标签

```
<audio src="于文文 - 体面 [mqms2].flac" controls></audio>
```

要加一个controls管控视频音频，不然播放不了

2.视频标签

```
<video src="video.mp4"controls></video>
```

## 10flash闪存标签(embed)

```
<object classid="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,29,0" width="778" height="202">
    <param name="movie" value="../../resource/banner.swf">
    <param name="quality" value="high">
    <param name="wmode" value="transparent">
    <embed src="images_2/banner.swf" width="100%"  quality="high" pluginspage="http://www.macromedia.com/go/getflashplayer" type="application/x-shockwave-flash" wmode="transparent"></embed>
</object>
```



## 11表单

#### 表单格式

<form action="http://httpbin.org/post" method="post" enctype="multipart/form-data">
	<table>
        <caption>登录界面</caption>
		<tr>
			<td>用户名：</td>
            <td><input type="text" name="uername" value=""></td>
        </tr>
        <tr>
            <td>密码:</td>
            <td><input type="password" name="pwd" value=""></td>
        </tr>
        <tr >
             <td><input type="submit" value="登录"></td>
             <td><input type="reset" value="返回登录"></td>
        </tr>
	</table>
</form>

其中 method是提交方法，有get和post两种。get相对来说不太安全，因为密码不应该显示在地址栏。不能传递海量数据，因此地址长度有限制。url字符最大长度65535。最大不能超过4kb chrome8k不能上传附件。

post相对来说比较安全。POST方式直接将表单数据发给了服务器，不会在地址栏显示包传递可以传递海量数据，长度没有限制。可以上传附件。

#### 常用属性

name：表单元素的名称。可以包含a-z、A-Z、0-9、_这些符号，但不能以数字开头。
value：元素的值。
size：文本框的长度，以字符为单位。
maxlength：最多可以输入的字符数
readonly：只读属性。如：readonly = “readonly”
disabled：禁用属性。如：disabled = “disabled”

type：元素的类型。取值：text、password、radio、checkbox、button、submit、reset等。

1)单行文本域 ：语法格式：<input type = “text” 属性 = “属性值” />

2)单行密码框 ：语法格式：<input type = “password” 属性 = “属性值”  />

3）单选按钮：语法格式：`<input  type = “radio” 属性 = “属性值” />`

​         				checked：是否默认选中。如：checked = “checked”

4）复选框：语法格式：`<input  type = “checkbox” 属性 = “属性值” />`

<input type="checkbox" name="hobby[]" value="1"><span>打游戏</span>

​					checked：是否默认选中。如：checked = “checked”

​					注意:`复选框的name后面要带[],是一个数组.

5）下拉列表：<select>标记的属性

<select name="dot">
	<option value="">..请选择</option>
	<option value="1">巴厘岛</option>
	<option value="2">马尔代夫</option>
	<option value="3">巴黎</option>
	<option value="4">悉尼</option>
	<option value="5">千锋</option>
</select>

6)文本区域:语法:<textarea  属性 = “属性值”></textarea>

<textarea name="info" rows="10" cols="50" value="" style='resize: none;'>..请输入你的信息</textarea>
7)上传文件域:语法格式：`<input  type = “file”  属性 = “属性值”  />

文件上传的方式只能是`post`,`form`表单必须要多加一个属性和值enctype="multipart/form-data"

8）表单中的各种按钮
提交按钮：提交表单。如：`<input  type = “submit”  value = “提交表单”  />`
重置按钮：重新填写。如：`<input  type = “reset”  value = “重新填写”  />`
图片按钮(不常用)：指定图片的路径，功能也是提交表单。如：`<input type="image" src="images/btn02.png" />`



```
前端代码的测试网站:www.httpbin.org
```

