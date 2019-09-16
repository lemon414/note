# Linux 目录结构和作用

/ 系统根目录

/ home 普通用户的家目录 存放所有用户文件的根目录，是用户主目录的基点。

/ root 超级管理员的家目录   sudo su - 变成超级管理员

/proc 虚拟的目录，是系统内存的映射。可直接访问这个目录来获取系统信息。

/etc  配置文件

/dev 设备文件下有个null 无底洞，丢弃一切写入其中的数据

linux里面隐藏文件可以在文件名前面加一个点进行重命名 利用ls -A 显示出隐藏文件

/run 运行目录,存放系统运作时的运行时数据

/tmp 临时目录,可以在该目录中创建和删除临时工作文件

/var  可变目录,用以存放经常变化的文件,比如日志文件

# Linux日常操作及命令

- cd 进入目录

- cd -  进入上一次位置

- ls 查看当前目录里的所有目录或文件

- pwd 显示当前的绝对路径位置

- mkdir 创建一个树级文件夹 mkdir -p a/{b/{d,e},c/{f,g}}

  - touch 创建文件 touch a/b/d/{x,y,z}

- find ./ -name '*.txt' 查找当前目录下所有txt文件

  - find ./ -type d
  - find ./ -size -1k 查找当前目录下小于1k的文件
  - find ./ -size +1k -size -2k 小于2k大于1k的文件
  - find ./ -name '*.py' -type f -size -1k

- rm -a 删除a    -r表示递归删除 -f强制删除

- cp 和mv  cp(mv) x ../e 把文件x复制(移动)到../e文件下

  其中mv 移动位置，其还可以实现重命名的功能

- cat 查看文件，显示里面的内容

- ln -s 源文件（绝对路径） 目的地（随便路径）   创建软链接，即快捷方式。ln 源文件 目的地 创建硬链接。

- tar -czf xxx.tgz a  将a打包并压缩到xxx.tgz里面 解压-xzf

- ehco='abcdefg' > 'abc'  创建一个abc文件清空并写入内容 >>是追加

## Bash快捷键

ctl + f 前进一一个字符
ctl + b 后退一一个字符
ctl + a 回到行首首
ctl + e 回到行尾
ctl + w 向左删除一一个单词
ctl + u 向左删除全部
ctl + k 向右删除全部
ctl + y 粘贴上次删除的内容
ctl + l 清屏

## 查找

find

- 查找当前文件夹下全部文件:find  ./
- 只查找文件     :  find  ./  -type   f
- 只查找目录     :   find  ./  -type  d
- 只查找链接     :   find   ./  -type  l
- 按名称查找     :   find   ./  -name  '*.py'
- 按权限查找     :   find   ./  -perm  0644
- 按大小查找     :   find   ./  -size  +1k  -size -5k   (1-5k间的文件) 

grep

- -i   忽略大小写
- -I   忽略二进制文件
- -r  递归查找目录
- -n   打印行号
- -c   只显示匹配到的个数
- -l   只显示匹配到的文件列表
- -o  只显示匹配到的单词
- -v  忽略制定的字段
- -E  通过正则表达式匹配
- include = '*.py'  仅包含py文件
- exclude='*.js'    仅包含js文件

which

whereis

## 压缩

- tar
  - 压缩:tar  -czf  abc.tar.gz  abc/
  - 解压:tar  -xzf   abc.tar.gz
- zip
  - 压缩:zip -r  abc.zip  abc/
  - 解压: unzip  abc.zip


