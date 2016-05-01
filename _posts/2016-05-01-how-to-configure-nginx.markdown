---
layout: post
title:  "nginx配置"
date:   2016-05-01 15:15:09 +0800
categories: jekyll update
---
架构  
===
nginx有一个master进程和一些worker进程。master用于处理配置文件，以及维护worker进程。woker进程处理请求。nginx使用基于事件、依赖操作系统的机制来高效分发请求到各个woker进程。


配置文件位置
===
配置文件的名称为`nginx.conf`，一般放置在`／usr/local/nginx/conf`, `/etc/nginx`, 或者`／usr/local/etc/ngix`目录下。
		
		
命令
===
运行nginx只需执行nginx二进制文件，或者`service nginx start`。一旦nginx启动后，可以用使用`nginx -s singal`向其发送命令。 
sigal可以是： 

1. stop    快速关闭
2. quit    优雅的关闭
3. reload  重新加载配置文件
4. reopen  新建日志文件
	
重点说明下`nginx -s reload`。master进程接到reload命令后，首先会验证新配置文件是否有效，并且尝试应用新的配置文件。如果成功，master
进程启动新的worker进程，并且发送消息给旧的worker进程，要求它们关闭。如果失败，master进程回滚变化，继续使用旧的配置文件。
	
	
静态站点配置
===
{% highlight xml %}
server {
	listen 80;
	server_name: www.jinjunhang.com;
	location / {
		root /home/jjh/jjhsite/_site;
		index index.html index.htm;
	}
}
{% endhighlight xml %}
一个server可以使用多个location配置，location配置可以使用正则表达式。


反向代理配置
===
{% highlight xml %}
server {
	locatoin / {
		proxy_pass http://localhost:8080/;
	} 
	location ~ \.(gif|jpg|png)$ {
		root /data/images;
	}
}
{% endhighlight xml %}
这里，第二个locaiton就是使用正则表达式方式进行配置。～后面跟了一个正则表达式。
	
负载均衡
===
nginx负载均衡策略：

* round-robin(轮询)  － 请求根据轮询方式分发到应用服务器。
* least-connected:  －  请求被分发到具有最好活动连接的服务器
* ip-hash  － 请求根据客户端的ip分发到不同的服务器。

需要注意的是，前面两种方式，无法满足Session要求，而`ip-hash`方式则可以，因为同一ip总是被分发到同一个服务器。	
例子：
{% highlight xml %}
upstream myapp {
	ip_hash;
	server svr1.example.com;
	server svr2.example.com;
	server svr3.example.com;
}
{% endhighlight xml %}
活动监测: nginx的反向代理实现包含活动监测。加入某个服务器的响应失败了，nginx就会标记这个服务器，并且将会避免将后续的请求分到到这个服务器。


注意点  不要将你的站点的owner设置为root，否则会提示403错误。



参考文献
===

* <a href='http://nginx.org/en/docs/beginners_guide.html'>nginx Beginner's Guide</a>
* <a href='http://nginx.org/en/docs/http/load_balancing.html'>Using nginx as HTTP load balancer</a>
* <a href='http://yufree.cn/blogcn/2014/10/25/kramdown.html'>kramdown 语法简介</a> 



