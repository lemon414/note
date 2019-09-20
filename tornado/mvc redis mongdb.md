# MVC

mvc模式：m 模型（不是模板）  v 视图  c 控制器

版本控制工具的作用：
​	1.能够追踪全部代码的状态
​	2.能够进行版本之间的差异对比
​	3.能够进行版本回滚
​	4.能够协助多个开发者进行代合并

# 虚拟环境

一般在你的项目文件夹里面创建

## Github 代码托管网站

配置
git config --global user.name 'xxxx'
git config --global user.email 'xxxx'

增加 .gitignore 影藏文件，在里面添加 忽略不需要追踪的文件

git init --初始化仓库，产生了一个 .git 目录，这个文件夹就是本地仓库
git status  查看信息
git add ./   --将当前文件夹的所有文件添加到暂存区

git reset --将暂存区的文件取消暂存的状态

git commit -m "提交完成时的提示信息" --将暂存区的代码提交到本地仓库s

git remote add origin git@github.com:lemon414/test01.git
git push -u origin master  --将本地仓库推送到远程操作 

ssh-keygen  --在~/ssh --目录下生成一对公钥和秘钥

cd ~/.ssh (里面有公钥秘钥的文件  非对称加密算法)
cat id_rsa_pub 公钥
将公钥内容复制到github

git clone --将已有远程仓库复制到本地，是将远程仓库全部拉取下来
git pull --将远程仓库拉取到本地仓库，只将最新的更新拉取到本地仓库

merge 合并

git log --查看历史信息

git checkout 提交id  --提交id通过git log 找到

git diff --差异对比

git blame --追责，查看最后一次代码谁修改的

redis 6379

3306 mysql

## 解决冲突

```
git push 在拉取的时候发现与别人修改的代码有冲突
git pull 将线上代码拉取到本地
git status 找到冲突文件有哪些，冲突文件的状态：both modified
逐一打开冲突文件，逐行解决冲突
冲突代码解决后，删除代码冲突标记
git add ./
git commit -m "提示信息"
git push
```


## 分支
git branch 分支名  --创建分支
git checkout 分支名 --切换分支
git checkout -b 分支名 --创建并切换分支（上面两句的合成）

git merge 分支名 --合并分支
# redis 

键值对数据库

redis-sever redis.conf --启动redis服务器

redis-cli --连接redis

存取数据时只支持字符串，即使你值是个字典或者其他类型，也会当做字符串取出来

set 存数据 以键值对存 set 键 值 EX 数（存取数据多少时间）

get 取数据 根据键取值

incr 自增