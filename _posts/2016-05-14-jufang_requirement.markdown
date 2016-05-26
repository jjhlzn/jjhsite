---
layout: post
title:  "接口"
date:   2016-05-01 15:15:09 +0800
categories: jekyll update
---

重要点
---

每个接口的请求体都是一个json字符串，例如：
   {% highlight javascript %}
{
   "userInfo": {
                 token = "",
                 userid = ""},
   "client": {
                 appversion = "1.0.3",
                 model = "iPhone6s",
                 osversion = "9.3",
                 platform = "iPhone",
                 screensize = "375*667"}, 
   "request": {
                 password = "123456",
                 username = "13706794299"}
 }
   {% endhighlight %}
每个请求体都会包含userInfo和client，分别表示用户信息和客户端信息，后面的接口就不重复出现了。
每个接口的响应都会包含status和errorMessage字段，表示响应的代码和错误消息。status = 0 表示请求成功，其他值表示出错的情况，例如-1表示出现异常，-10表示用户权限问题。

1)登录
===

1. URL: http://localhost:3000/user/login
2. 请求体
   {% highlight javascript %}
   {
       "request": {
             username = "13706794290",
             password = "123456"}
    }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = "";
        name = "jjh";
        token = "1234567890abcdefghijklmn";
    }
  {% endhighlight  %}
  
  
2)获取手机验证码
===

1. URL: http://localhost:3000/user/getPhoneCheckCode
2. 请求体
{% highlight javascript %}
{
    "request": {
        phoneNumber = "13706794299" }
}
{% endhighlight %}

3. 响应
{% highlight javascript %}
{
    errorMessage = "";
    status = 0;
}
{% endhighlight%}

3)注册
===

1. URL: http://localhost:3000/user/signup
2. 请求体
 {% highlight javascript %}
{ 
    "request": {
        checkCode = "123456";
        invitePhone = "12345678900";
        password = "123456";
        phoneNumber = "13706794299";}
}
 {% endhighlight %}

3. 响应
  {% highlight javascript %}
  {
      errorMessage = "";
      status = 0;
  }
  {% endhighlight %}
  
4)重设密码（通过验证码）
===

1. URL: http://localhost:3000/user/getPassword
2. 请求体
 {% highlight javascript %}
{ 
    "request": {
        checkCode = “fdsfdf”,
        password = "123456",
        phoneNumber = "13706794299"
    }
}
 {% endhighlight %}

3. 响应
  {% highlight javascript %}
  {
      errorMessage = "";
      status = 0;
  }
  {% endhighlight %}
  
5)获取课程列表
===

1. URL:  http://jjhaudio.hengdianworld.com:80/album/songs
2. 请求体
   {% highlight javascript %}
{
       "request": {
           type = "common";
   	       pageno = 0,
   	       pagesize = 15}
}
   {% endhighlight  %}
   说明：type类型有三个值，分别为`common`(往期课程), `live`(直播课程), `vip`(课程)
   
3. 响应
   {% highlight javascript %}
   {
       albums =  [{
                       author = "Avril Lavigne";
                       count = "50";
                       id = "1";
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       listenCount = "1000";
                       name = "test";
                       type = Common; },
                   {
                       author = "test1";
                       count = "32";
                       id = "2";
                       image = "http://jjhaudio.hengdianworld.com/images/yuantengfei.jpg";
                       listenCount = "10";
                       name = "test1";
                       type = 'Common'; },
                   {
                       author = "test2";
                       count = "10";
                       id = "3";
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       listenCount = "19";
                       name = "test2";
                       type = 'Common';}],
       errorMessage = "",
       status = 0,
       totalNumber = 20
   }
   {% endhighlight  %}
   
   
6)获取课程的课的列表
===

1. URL:  http://jjhaudio.hengdianworld.com:80/album/songs
2. 请求体
   {% highlight javascript %}
｛
    "request": {
        album = "{'id': 8}";
	    pageno = 0,
	    pagesize = 15 }
 ｝
{% endhighlight  %}

3. 响应
   
   a) 往期课程和VIP课程的response
   
   settings表示每节课的配置，canComment表示是否能评论，maxCommentWord表示能够评论的字数
   {% highlight javascript %}
   {
       albums =  [{
                       author = "Avril Lavigne";
                       count = "50";
                       id = "1";
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       listenCount = "1000";
                       name = "test";
                       settings =  {
                                       canComment = true; 
                                       maxCommentWord = 20;
                                   };
                       type = Common; },
                   {
                       author = "test1";
                       count = "32";
                       id = "2";
                       settings =   {
                                       canComment = true;
                                       maxCommentWord = 20;
                                   };
                       image = "http://jjhaudio.hengdianworld.com/images/yuantengfei.jpg";
                       listenCount = "10";
                       name = "test1";
                       type = 'Common'; },
                   {
                       author = "test2";
                       count = "10";
                       id = "3";
                       settings =   {
                                       canComment = false;
                                       maxCommentWord = 20;
                                   };
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       listenCount = "19";
                       name = "test2";
                       type = 'Common';}],
       errorMessage = "",
       status = 0,
       totalNumber = 20
   }
   {% endhighlight  %}
   
   b）直播课程的resonse
   
   直播课程需要提供直播的开始时间和结束时间，格式例如：'2016-05-19 13:00:00'
   {% highlight javascript %}
   {
       albums =  [{
                       author = "Avril Lavigne";
                       count = "50";
                       id = "1";
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       listenCount = "1000";
                       name = "test";
                       settings =  {
                                       canComment = true; 
                                       maxCommentWord = 20;
                                    }，
                       startTime = "2016-05-19 13:00:00"，
                       endTime = "2016-05-19 17:00:00"，
                       type = Live; }
       errorMessage = "",
       status = 0,
       totalNumber = 20
   }
   {% endhighlight  %}
   
   
7)获取评论
===

1. URL:  http://jjhaudio.hengdianworld.com:80/song/comments
2. 请求体
   {% highlight javascript %}
{
        "request": {
            song = "{'id': 8}",
            pageno = 0,
            pagesize = 15 
        }
 }
{% endhighlight  %}

3. 响应
   {% highlight javascript %}
   {
       errorMessage = "";
       status = 0;
       totalNumber = 20;
       comments =  [
          {
               content = "test";
               id = 1;
               time = "1小时前";
               userId = "jjh";
           },
           {
               content = "test";
               id = 2;
               time = "1分钟前";
               userId = "test";
           },
          {
               content = "test";
               id = 3;
               time = "刚刚";
               userId = "who";
           }
       ];
   }
   {% endhighlight  %}


8)获取实时在线聊天记录
===

1. URL:  http://jjhaudio.hengdianworld.com:80/song/livecomments
2. 请求体
   {% highlight javascript %}
{
        "request": {
            song = "{'id': 8}",
            lastId = 10  //lastId表示上次获得的最新的聊天记录id, -1表示第一次请求
        }
}
{% endhighlight  %}

3. 响应
    
   每次返回最新，并且id > lastId的至多100条（最多条数可以以后看情况再改）聊天记录
   {% highlight javascript %}
   {
       errorMessage = "";
       status = 0;
       comments =  [
          {
               content = "test";
               id = 1;
               time = "1小时前";
               userId = "jjh";
           },
           {
               content = "test";
               id = 2;
               time = "1分钟前";
               userId = "test";
           },
          {
               content = "test";
               id = 3;
               time = "刚刚";
               userId = "who";
           }
       ];
   }
   {% endhighlight  %}
   
   
8)发送评论
===

1. URL:  http://localhost:3000/comment/add
2. 请求体
   {% highlight javascript %}
{
    "request": {
        comment = Rwerewr
    }
}
{% endhighlight  %}

3. 响应
   {% highlight javascript %}
{
    errorMessage = "";
    status = 0;
}

   {% endhighlight  %}
   
   
9)获取在线人数
===

1. URL:  http://localhost:3000/song/livelistener
2. 请求体
   {% highlight javascript %}
{
    "request": {
        comment = Rwerewr
    }
}
{% endhighlight  %}

3. 响应
   {% highlight javascript %}
{
    errorMessage = "";
    status = 0;
    listerCount = 1000
}

   {% endhighlight  %}
   


