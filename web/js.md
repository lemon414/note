## 	Js

JavaScript是一种小型的、轻量级的、面向对象的、跨平台的客户端脚本语言。

什么是对象？就是现实中的’东西‘。显示中的‘东西’看得见摸得着。

**js程序代码也是嵌入到HTML中的。<script type="text/javascript">这里写js的代码</script>**

typeof（）判断变量的数据类型

**/ JS是区分大小写的 /**

### 一、JS的输出方法

#### 1）document.write(str)

文本对象，控制所有文本（body），只限于标签部分

将内容打印到body当中

document.不能去掉，去掉就废了

#### 2）window.alert(str)

window对象，去除document之外的部分

弹出一个警告对话框，内容是str，不加以解析。

window能去掉，依然能正常使用

#### 3）console.log（str）

控制台输出，只能在控制台里面操控

### 二、注释

HTML的注释：<!--注释内容-->

CSS注释：/*  注释内容 */

JS的单行注释：//

JS的多行注释：/*  多行注释 */

### 三、JS的变量

变量是在内存中存在和运行的。

声明变量：var 变量名；（声明变量和定义变量是不同的，var和变量名之间用空格隔开）

&不能乱用，jQuery=&



### 四、JS的数据类型

基本数值类型：字符型（**不能进行加减乘除**）同名变量将被覆盖,下面变量将覆盖上面的同名变量、数值型（**能进行加减乘除的**）、布尔型（false和true）、未定义型（undefined）当一个变量定义了，但未赋值，此时，该变量的类型是**未定义型**。、空型（null）null代表一个空对象，或者是对象的一个占位符。

复合数值类型：数组型、对象型、函数型。

### 五、数据类型的转换

变量之间的运算必须是同类型的，不同类型要转化成同类型才能进行运算。

在字符串进行—减法会变成NaN类型

NaN加上数值类型还是NaN，加上str会变成字符串类型

NaN和谁都不相等，和它自己也不相等。NaN==NaN#False  

无论什么类型都能转换成字符型

不是整数类型的字符串转换成数值型会变成NaN类型

```
其他类型转布尔型：var result = Boolean(a);
var a = "";        //false
var a = undefined; //false
var a = null;      //false
var a = 100;       //true
var a = 0;         //false
var a = 0.98;      //true
var a = NaN;       //false
var a = "abc";     //true
```

~~~
其他类型转数值型：var result = Number(a);
var a = "100px"; // NaN
var a = ""       // 0
var a = true;    // 1
var a = false;   // 0
var a = undefined // NaN
var a = null;    // 0
var a = "abc"    // NaN
~~~

**系统函数 parseInt()**：在一个字符串，**从左往右**提取整型；如果遇到非整型的内容，则停止提取，并返回其值。如果第一个字符不是整型的话，则直接返回NaN。

**系统函数 parseFloat()**：在一个字符串中，从左往右提取浮点数；如果遇到非浮点数的字符，则停止提取，并返回提取的值。如果第一个字符是非浮点数字符，则直接返回NaN。

### 六、JS的运算符

#### 1）算数运算符：+、-、*、/、%、++、--

a++和++a的区别：

**++a：先加在用；a++：先用在加**,但用在for里面就没有区别,两个用谁都一样

**左右两个操作数一个是字符串的话，将执行字符串的拼接运算，会将另一个数值转化为字符串然后进行拼接操作。**



python中while可以叫else，而js中while不能加else

#### 2）赋值运算符：=、+=、-=、*=、/=、%=

比较运算符结果是一个布尔值

**==只检查值相等或者数据类型相等，只要有一个一致则true**

**===既检查值是否相等，还检查数据类型是否相等。一致返回true**

#### 3）逻辑运算符

“&&”逻辑与(并且)。如果左右两个条件同时为true，则结果为true。反之，结果为false。

“||”逻辑或(或者)。如果左右有一个条件为true，则总结果为true。反之，结果为false。

#### 4）三元运算符

语法格式：条件判断？结果1：结果2

var max = a > b ? a : b;

### window.prompt()

用于显示提示用户进行输入的对话框

语法：**window.prompt(text,defaultText)**

点击确定返回一个字符串的数据，点击取消返回null

#### 5）一些特殊的运算符

- 1）new运算符

创建一个对象的实例。举例：var today = new Date(); Today是日期对象的实例的名称。today变量类型是对象。

- 2）delete运算符

删除对象的属性或数组中的元素。

举例：delete arr[0]  // 删除数组中索引为0的元素

- 3）typeof运算符

判断一个变量的数据类型，**返回值是字符**串：“string” “number” “boolean” “undefined” “object” “function”

~~~
console.log(typeof(变量))
~~~



- 4）小数点

用来调用对象的属性或方法

- 5）小括号（）和 []运算符

[]主要用于存取数组中的元素

#### 6）运算符优先级

特殊运算符》算数运算符》比较运算符》逻辑运算符》赋值运算符

### switch分支语句

switch（条件判断）{

​	case1：

​			代码1;

​			break;

​	case2:

​			代码2;

​			break；

​	default：

​			默认代码3；

}

### while循环--重复执行

```
while(条件判断){
  	如果条件true,重复执行的代码
  	循环体代码,一般完成某项功能
}
```

循环三要素：变量初始化；条件判断；变量更新

### for循环

```
for(变量初始值;条件判断;变量更新){
  	循环体的代码
}
```

break中断语句：无条件中断循环，只能退出一层循环。

continue语句：用于结束本次循环，而开始下一次新的循环。也就是：本次循环的剩余代码不再执行。

## 函数

### 1.函数的定义

函数定义未调用前是一个类，调用（即实例化）变成实例方法。函数的特点：减少代码量、提高工作效率、后期维护十分方面。

~~~
function getMax(a,b){     //关键字function定义函数，函数名称与变量一样，采用小驼峰法。
  var min;
  if(a>b){
  	min = b;          //函数功能的实现
  }else{
  	min = a;
  	return min    //向函数调用者返回一个值，一旦执行，剩下代码将不在执行。结束函数的运行。
  }
  document.write(a+"和"+b+"的最小值是:" + min + "<hr />");
}
getMax(10.20);   //函数的调用：函数名（）加小括号
getMax(5,8)
~~~

形参：定义函数时的参数，主要用来接收调用函数者传递的一个值。

实参：调用函数时的参数，主要用来向定义函数传值。

**形参和实参个数必须一样**

如果不使用retrun语句返回的话，则函数返回undefine值。

#### 全局变量和局部变量

**全局变量：**可以再网页任何地方（函数内外）都能使用的变量，在网页关闭时自动消失。

**局部变量：**只能在函数内部使用的变量，不能再函数外部使用，函数执行完毕就消失了。

#### 匿名函数（没有名字的函数）

匿名函数，一般是用来给其它变量赋值用的。将匿名函数的定义，作为一个数据，赋给另一个变量。这样一来，该变量就是函数型了。

~~~
var a = function(){
  document.write("ok");
}
//调用函数
var b = a; //引用地址:将变量a的地址给b
b(); //调用函数
~~~



## 拷贝传值和引用传址

**拷贝传值：**将一个变量的值，“复制”一份，传给另一个变量。这两个变量没有任何关系。这两个变量是相互独立的，修改其中一个，另一个不会受影响。

**引用传址：**将一个变量的“数据地址”，“复制”一份，传给了另一个变量。那么，这样来，两个变量指向了“同一物”“同一空间”。这两个变量之间是有联系的，修改其中一个，另一个也会变。

哪些数据类型是“拷贝传值”？**基本数据类型都是拷贝传值：字符型、数值型、布尔型、undefined、null**。

哪些数据类型是引用传地址？**复合数据类型：数组、对象、函数。**

~~~
//引用传地址
var arr1 = [10,20,30];
var arr2 = arr1; //将arr1的地址,复制一份,传给arr2
arr1[0] = 100; //将arr1[0]进行了修改
document.write(arr2[0]);
结果是100，因为是一个数组，属于引用传地址，所以修改其中一个另一个也会改变。
~~~

## 二维数组

二维数组：就是数组套数组

~~~
var arr[
 [1,2,3,4],
 [4,5,7,8],
 [23,7,47,83,,]
]
(2)使用new关键字，结合Array（）构造数组
var arr = new Array(); 
arr[0] = "Mary";
arr[1] = "女";
console.log(arr)//结果:["Mary", "女"]
**二维数组的访问:arr[][]**
~~~

[][]数组在js中说它想list不如说更加的像dict,也需要先定义,然后可以自由的添加元素

~~~
//求二维数组的平均值
            var arr = [
              [10,11,12,13],
              [20,21,22],
              [30,31],
              [40]
            ]
            var sum=0
            for(i in arr){//遍历外面数组
               for(j in arr[i]){//遍历数组里面套着的数组
                    sum+=arr[i][j]
               }
            }
            console.log(sum)
~~~

## 对象

对象是由属性和方法构成的。

### 1）对象的分类

- **String对象：**一个字符就是一个String对象。如：var str = “12345678”;  var len = str.length；
- **Number对象：**一个数值数据就是一个Number对象。如：var a = 100.9888;  a.toFixed(2)；
- **Boolean对象：**一个布尔值就是一个Boolean对象。
- **Math对象：**数学对象。如：Math.PI、Math.abs()、Math.random()
- **Function对象：**一个函数就是一个function对象。
- **Array对象：**一个数组变量，就是一个Array对象。如：var len = arr.length
- **BOM对象：**window、location、history、screen、document
- **DOM对象：**a对象、p对象、html对象等。CSS对象。

### 2）自定义对象的创建

- 使用new关键字，结合Object（）

~~~
                var obj=new Object()//创建一个空的对象
                obj['name']='lucy';
                obj.sex='woman';  //添加属性
                obj.hobby='play game';
                obj.func=function(n){  //添加方法（函数）
                    return n
                }
                console.log(obj.name)//lucy
                console.log(obj.func(100))//调用对象里的方法（函数）100
~~~

- 使用{}创建

~~~

~~~

### 3）JS内置对象

- String对象：提供了一些对字符串处理的属性和方法。一个字符串的变量，就是一个String对象。

  - **length**属性：动态获取字符串的长度

  **语法：var len = strObj.length**

  ~~~
  var str = "上海py1905班";
  var len = str.length;
  document.write("长度为:"+len); //9
  ~~~

  - **toLowerCase()和toUpperCase()**

    strObj.toLowerCase() 将字母转成全小写。

    strObj.toUpperCase() 将字母转成全大写。

    ~~~
    var str = "Welcome to ShangHai";
    document.write(str.toLowerCase()); //全小写
    document.write(str.toUpperCase); //全大写
    ~~~

    

  - **charAt(index)**：返回字符串中指定下标处的**一个**字符，若不存在返回undefined

    **语法：strObj.charAt(index)**

  - **indexOf()**

    > **描述：在原始字符串，从左往右查找指定的字符串，如果找到，返回其下标值。如果没有找到，返回-1。**

    **语法：strObj.indexOf(substr)**

    注意：只查找第一次出现的字符，第二个相同的不再查找。

  - **lastindexOf()**：从右往左

  - **substr():**提取指定字符串，从索引处往后切几个

    **语法：strObj.substr(startIndex [ , length])**

    ~~~
    startIndex是要查找的子字符串的开始位置(索引号)。
    length可选项。从startIndex处往后提取length个字符。如果length省略，则一直提取到结尾。
    var str = “abcdefgh”;
    str.substr(0,3);  // “abc”
    str.substr(0,5);  // “abcde”
    str.substr(3,3);  // “def”
    str.substr(5);   // “fgh”
    ~~~

    

  - **substring（）：**从原始字符串下标提取至指定字符串下标，含前不含后

  - **split()：**将一个字符串切成若干段，将一个字符串用指定的连接号分割成一个数组。

    语法：**array strObj.split(分割符)

    返回值：是一个数组

- Array对象：对数组操作的属性和方法

  - **length属性：**动态获取数组的长度，也就是元素的总个数。

  - **join()：**将一个数组各元素，用指定的连接号，连成一个字符串。

  - **添加和删除元素**

    ~~~
    delete删除元素的值，而下标还在(长度不会减少)。
    
    push从后面插入新的元素。
    
    shift()删除第1个数组元素，数组长度减1。并返回删除元素的值。
    
    pop()删除最后1个数组元素，数组长度减1。并返回删除元素的值。
    ~~~

  - **reverse()：**倒叙

- Date对象：提供了对系统时钟副本操作的属性和方法。
  
  - getTime（）获取当前时间戳

Boolean对象：一个布尔值，就是一个Boolean对象。

- Number对象：一个数值就是一个Number对象。- toFixed(2)：保留小数点后面的几位数

- Math对象：数学方面的属性和方法
  - random()返回0-1之间的随机小数。Math.random() = 0.9026920931341323

## BOM

### 1.window对象--浏览器窗口对象

#### window对象方法

- **window.alert():**弹出一个警告对话框，只有一个确定按钮。

- **window.prompt:**弹出一个输入对话框，有确定和取消两个按钮。单“确定”返回字符串数据。单击“取消”返回null。

- **window.confirm(提示信息):**弹出一个确认对话框。单击“确定”返回true，单击“取消”返回false。

- **window.close():**关闭window窗口。

- **window.open():**打开一个新的浏览器窗口。

### 2.screen屏幕对象

Width：屏幕总宽度，包括任务栏。

Height：屏幕总高度，包括任务栏。

availWidth：屏幕有效宽度，不含任务栏。

availHeight：屏幕有效高度，不含任务栏。

### 3.navigator对象

### 4.location对象--地址栏对象

**js跳转:**location.href='http://www.sina.com.cn';

**html跳转:**<meta http-equiv='refresh' content='2;url=http://www.baidu.com'>

一些属性:

href:获取或设置地址栏中的地址。

host：获取或设置主机名。

pathname：文件及路径。

 search：查询字符串。指地址栏中“?”之后的字符。

protocol：协议。如：http://、ftp://、file:///

hash：锚点名称。如：#top

 reload()：刷新网页，相当于工具栏中“刷新”按钮。

### 延时器--时间一到执行一次

**1.setTimeout（）**：设定延时器

语法：var timer = window.setTimeout(code,millisec)

**2.clearTimeout（）**：清除延时器

语法：window.clearTimeout(timer)

~~~

~~~

## 定时器--周期性执行

**1.setInterval():**每隔指定的毫秒值，执行JS程序一次(周期性执行)。返回定时器的变量id，是一个整型。用来被 clearInterval() 清除。

语法：var timer = window.setInterval(code,millisec)

**2.clearInterval():**清除定时器变量

语法：window.clearInterval(timer)

~~~
var timer = window.setInterval(“func()” , 1000)  //每隔1秒调func()函数。
~~~

~~~
var timer = window.setTimeout(“func()” , 1000)  //1秒后调用func()函数，带引号，带括号，是传地址。
~~~

*args 元组

*kwargs 字典



注意切片：mysql limit从索引为3的位置上向后取3个

python 半闭区间

date对象 getTime（）

定时器重要