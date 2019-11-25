## cookie与session的区别

1、cookie数据存放在客户端上，session数据放在服务器上。
2、cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗 
考虑到安全应当使用session。
3、session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能 
考虑到减轻服务器性能方面，应当使用COOKIE



## session与token的区别

1.作为身份认证 token安全性比session好，因为每个请求都有签名还能防止监听以及重放攻击
2.Session 是一种HTTP存储机制，目的是为无状态的HTTP提供的持久机制。Session 认证只是简单的把User 信息存储到Session 里，因为SID 的不可预测性，暂且认为是安全的。这是一种认证手段。 但是如果有了某个User的SID,就相当于拥有该User的全部权利.SID不应该共享给其他网站或第三方.
3.Token,如果指的是OAuth Token 或类似的机制的话，提供的是 认证 和 授权 ，认证是针对用户，授权是针对App。其目的是让 某App有权利访问 某用户 的信息。这里的 Token是唯一的。不可以转移到其它 App上，也不可以转到其它 用户上。



## csrf豁免

```
CSRF
	防跨站攻击
	实现机制
		页面中存在{% csrf_token %}时
		在渲染的时候，会向Response中添加 csrftoken的Cookie
		在提交的时候，会被添加到请求体中， 会被验证有效性
    csrf（https://www.jianshu.com/p/d1407591e8de）
解决csrf的问题/csrf豁免：
    1 注释中间件
    2 在表单中添加{%csrf_token%}
    3 在方法上添加 @csrf_exempt
```

