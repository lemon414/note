## CSS

## css选择器

CSS Cascading style sheet   层叠 样式 表

CSS控制结构中的元素的样式或者说,控制网页的外观

JS是控制网页的动作的;

必须写在style标签中

```
语法格式：
<style type="text/css">
	h1 {color:red;font-size:12px;}
</style>
属性名"是CSS中规定的,不能自己定义.
```

###### 类选择器：给一类的HTML标记添加样式.只要HTML标记的`class`属性是一样的,浏览器就认为是一类.一个标签中可以有多个，用空格分开。

HTML里的公共属性,就是每个标签都可以拥有的属性;比如`id`,`name`,`class`,`style`,`title`等.调用这些类时，要在在<style></style>>里,以小数点开头比如 **. **div{color:red;}其中各个属性定义要用分号隔开。

- id选择器：具有唯一性，在<style></style>>里使用时必须以#开头命名.
- 多元素选择器：同时给多个元素，加同一种样式
- 后代元素选择器：给它的所有子元素或者孙子元素（只要是他的后代都可以）添加样式。它与它的后代之间用空格隔开。
- 子元素选择器：只能给当前元素的子元素添加样式。用>隔开。

margin外边距和padding内边距一般先设置为零。

内边距可以被背景颜色填充，外边距不可以

进程在做大规模的计算时使用，线程在计算并不会提速。线程只会在读写的时候会提速。协程

###### 伪类选择器：

：link{color:gray;text-decoration:none;}  :正常链接效果。
：visited{color:green;text-decoration:underline;}  ：访问过的效果
：hover{color:red;}                     ：鼠标放上的效果
：active{color:yellow;}                 ：激活状态(鼠标点击的一瞬间出现一般不用)

注意：这4个的顺序一定不能弄错,弄错了就没有效果

## css一些属性

#### 1）字体属性

- font-size：文字大小。
- font-weight：加粗效果。取值：bold
- font-style：斜体效果。取值：italic
- font-family：字体。

#### 2）文本属性

- color：文本颜色。
- line-height：行高，可以是百分比，也可以是固定值。
- text-align：文本的水平对齐方式，取值：left、center、right
- letter-spacing：字间距。
- text-decoration：文本修饰线，取值：underline(下划线)、none、overline(上划线)、line-through(删除线)
- text-indent：首行缩进。

#### 3）px和em和rem

- px 像素
- em是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。em是根据父类的变化而变化的.
- rem和em类似,`rem:root em`;相对于根的比较;
- 默认的大小是16px

#### 4)列表属性

- list-style：去除列表前面的小点或者标题数字。

#### 5）边框属性

- border-left：左边框线。
  	格式：border-left: 粗细 线型 颜色;(px)

- border-right：右边框线。

- border-top：上边框线。

- border-bottom：下边框线。

- 简写方式：
  	border：四个边框都加同一种边线。
    	举例：div{border:2px solid blue;

- 	线型：none(无线)、solid(实线)、dotted(点状线)、dashed(虚线)、double(双线)
    	颜色:十进制  十六  单词
    	注意：多个参数值之间用空格隔开。
    	举例：div{border-left:5px solid red;}

#### 6)填充属性

- 内边距（padding）

  padding：numpx numpx numpx numpx//顺序为上右下左

- 外边距（margin）

  同内边距

#### 7）背景属性

- background-color：背景颜色

- background-image：背景图插图

- background-repeat：控制图片的平铺方式

  no-repeat：不平铺

  repeat-x：水平方向平铺

  repeat-y：垂直方向平铺

  默认水平竖直都平铺

- background-position：背景图片的定位方式

  注意事项：`要想使用图片定位功能，该图片不能进行平铺`。

  定位的单词：left，center，right，top，bottom

##### 例题

```
/*全局样式设置*/
body,h2,p{margin:0px;padding:0px;}
body{font-size:14px;color:red;background-color:blue;}
/*局部样式设置*/
.box{
	width:600px;
	margin:30px auto;
	padding:10px 10px 130px;
	background:white url(images/02.gif) no-repeat 480px bottom;

}
.box h2{
	text-align:center;
	padding:10px 0px;
	color:red;
}
.box p{
	line-height:160%;
	text-indent:28px;
	color:blue;
}
```

```
<div class="box">
<h2>python 1905</h2>
<p>hello world</p>
</div>
```

#### 8）display属性（控制元素的显示方式）

取值：`none`(不显示)、`block`(块显示)、`inline`(以行内元素显示)

注意：元素隐藏不再占空间了。

#### 9）overflow属性（处理内容溢出）

取值：scroll(出现滚动条)、hidden(隐藏)、auto(自动)、visible(显示)

#### 10)cursor(改变鼠标类型)

取值：pointer(手形)、help(帮助)、text(文本)、wait(等待)等。

## css定位属性

- position(定位属性)：static：静态定位，不定位，默认值。		

​			   :   fixed ：固定定位。
​    		   :   relative :  相对定位。相对所有标记的高度和
​			   :  absolute ：绝对定位。 相对的浏览器的边框

- 定位坐标值

left：距离目标元素左边的距离。
righ：距离目标元素右边的距离。
top：距离目标元素顶边的距离
bottom：距离目标元素底边的距离。
提示：如果不指定定位坐标值，定位元素在“原地不动”

- 固定定位——position:fixed

  固定定位元素，是相对于浏览器窗口，来进行的定位。固定定位元素，不再占空间了。固定定位元素层级高于普通元素。固定定位元素，一定是块元素，不管原来是什么元素。如果不指定定位坐标，则该元素“原地不动”，位置不会改变

- 相对定位（position：relative）

  相对定位，是相对于“原来的自己”进行的定位。相对定位元素，所占的空间依然存在。相对定位元素，层级要高于普通元素。如果不指定定位坐标，该元素“原地不动”。原来是什么元素，进行相对定位后，还是什么元素。定位元素可以超出父元素的边界，而浮动元素，是不可以超出父元素的边界。

## css浮动和清除

#### 1)浮动

- float：浮动属性，取值：left或right。
- CSS浮动可以使元素向左或向右浮动。浮动到父元素的边上或者上一个浮动元素的边上。
- 浮动的元素不再占空间了。
- 浮动的元素层级高于普通元素(没有浮动)。
- 浮动的元素一定是块元素，不管以前是什么元素。换句话：行内元素浮动以后，也变成了块元素。

#### 2）清除浮动

- clear：清除浮动，取值：left、right、both(两者)`clear:both;`
- 一般情况下，上面有浮动，下面就得清除浮动
- 先浮动，后清除；有浮动，必须要有清除浮动
- 清除浮动后，可以让父元素在“视觉”上包含浮动元素
- 清除浮动后，清除浮动之后的其它元素，将恢复默认排版(不再继承上面的浮动特性)

## HTML引入css的方法

#### 嵌入式

通过`<style>`标记来书写CSS代码。
格式：`<style  type = “text/css”>……</style>`
说明：这种方式只能在当前HTML文件中使用，不能被多个HTML文件共享。
说明：`<style>`标记可以在网页中多次出现，想写在什么地方，就写在什么地方。

#### 外联式

将外部的 `.css`文件引入到当前的HTML文件中。
说明：可以将公共的CSS代码放在外部的文件，通过`<link>`标记将其引入，可以实现多个网页共享同一个CSS文件。
**格式：`<link href = “css/public.css" type = “text/css" rel = “stylesheet" />**
属性：
`href`：指定外部的CSS文件路径。
`type`：指链入文件的类型。
`rel`：链接入文件与当前HTML文件的关系。取值：`stylesheet`。
说明：`<link>`标记是`<head>`的子标记。一个网页中也可出现多个`<link>`。`<link>`标记可以放在HTML网页的任何地方。