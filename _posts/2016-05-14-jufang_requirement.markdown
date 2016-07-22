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

0)版本更新检查
===

1. URL: http://localhost:3000/app/checkUpgrade
2. 请求体
   {% highlight javascript %}
   {
       "request": {}
    }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = "",
        newestVersion: '1.0.1',   //最新版本号
        isNeedUpgrade: true,  //是否需要更新
        upgradeType: 'optional', //升级类型 optional表示可选升级，force表示强制升级
        upgradeUrl: 'http://www.baidu.com'   //升级url
    }
  {% endhighlight  %}
  
 
1)获取广告
===

1. URL: http://localhost:3000/app/getAds
2. 请求体
   {% highlight javascript %}
   {
       "request": {}
    }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = "",
        ads: [
                {imageUrl: "http://img.weiphone.net/1/h061/h23/bc9c8fe1img201606071030220_306__220.jpg",
                 clickUrl: "http://www.baidu.com", 
                 title: "信用卡活动"},
                {imageUrl: "http://img.weiphone.net/1/h061/h23/bc9c8fe1img201606071030220_306__220.jpg",
                 clickUrl: "http://www.baidu.com", 
                 title: "信用卡活动"}
             ]
    }
  {% endhighlight  %}
  
2)注册DeviceToken(用于通知推送)
===

1. URL: http://localhost:3000/app/registerDevice
2. 请求体
   {% highlight javascript %}
   {
       "request": {
           deviceToken: "fdsfsdfsdfsfsdfsdf"
       }
    }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = ""
    }
  {% endhighlight  %}
    

3)登录
===

1. URL: http://localhost:3000/user/login
2. 请求体
   {% highlight javascript %}
   {
       "request": {
             username = "13706794290",
             password = "123456",
             deviceToken = "fsdfsdfsdfsdfsdfdsfsdfdsf" 
         }
    }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = "";
        name = "jjh";
        sex = "男",  //男  或  女  或 保密
        codeImageUrl: "http://www.baidu.com/image.png",
        token = "1234567890abcdefghijklmn";
    }
  {% endhighlight  %}
  
  

3)更新权限token
===

1. URL: http://localhost:3000/user/updatetoken
2. 请求体
   {% highlight javascript %}
   {
       "request": {
             username = "13706794290",
             password = "123456",
         }
    }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = "";
        name = "jjh";
        nickname = "jjh",
        level = "vip",
        boss = "lzn",
        sex = "男",  //男  或  女  或 保密
        codeImageUrl: "http://www.baidu.com/image.png",
        token = "1234567890abcdefghijklmn";
    }
  {% endhighlight  %}

  
4)退出登录
===

1. URL: http://localhost:3000/user/logout
2. 请求体
   {% highlight javascript %}
   {
       "request": {}
   }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = "";
    }
  {% endhighlight  %}
  
5)设置姓名
===

1. URL: http://localhost:3000/user/setName
2. 请求体
   {% highlight javascript %}
   {
       "request": {
           newName: 'jjh'
       }
   }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = "";
    }
  {% endhighlight  %}
  
6)设置性别
===

1. URL: http://localhost:3000/user/setSex
2. 请求体
   {% highlight javascript %}
   {
       "request": {
           newSex: '男'
       }
   }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = "";
    }
  {% endhighlight  %}
  
  
7)获取手机验证码
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

8)注册
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
  
9)重设密码（通过验证码）
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
  
10)重设密码（登录之后，提供原密码）
===

1. URL: http://localhost:3000/user/resetPassword
2. 请求体
 {% highlight javascript %}
{ 
    "request": {
        oldPassword = "123456",
        newPassword = "xxxxx"
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
  
  
11)获取推荐人数
===

1. URL: http://localhost:3000/user/getClientNumber
2. 请求体
 {% highlight javascript %}
{ 
    "request": {
    }
}
 {% endhighlight %}

3. 响应
  {% highlight javascript %}
  {
      errorMessage = "";
      status = 0;
      peopleCount = 120
  }
  {% endhighlight %}
  
12)获取课程列表
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
                       count = 50，
                       id = 1;
                       desc: 'desc',
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       listenCount = "1000";
                       name = "test";
                       type = Common; },
                   {
                       author = "test1";
                       count = 2;
                       id = 2;
                       desc: 'desc',
                       image = "http://jjhaudio.hengdianworld.com/images/yuantengfei.jpg";
                       listenCount = "10";
                       name = "test1";
                       type = 'Common'; },
                   {
                       author = "test2";
                       count = 10,
                       id = 3,
                       desc: 'desc',
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       listenCount = "19";
                       name = "test2";
                       type = 'Common';}],
       errorMessage = "",
       status = 0,
       totalNumber = 20
   }
   {% endhighlight  %}
   
   
13) 查找课程
===   

1. URL:  http://jjhaudio.hengdianworld.com:80/album/search
2. 请求体
   {% highlight javascript %}
｛
    "request": {
        keyword = 'test',
	    pageno = 0,
	    pagesize = 15 }
 ｝
{% endhighlight  %}

3. 响应

   {% highlight javascript %}
   {
       albums =  [{
                       author = "Avril Lavigne";
                       count = "50";
                       id = "1";
                       desc: 'desc',
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       listenCount = "1000";
                       name = "test";
                       type = Common; },
                   {
                       author = "test1";
                       count = "32";
                       id = "2";
                       desc: 'desc',
                       image = "http://jjhaudio.hengdianworld.com/images/yuantengfei.jpg";
                       listenCount = "10";
                       name = "test1";
                       type = 'Common'; },
                   {
                       author = "test2";
                       count = "10";
                       id = "3";
                       desc: 'desc',
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       listenCount = "19";
                       name = "test2";
                       type = 'Common';}],
       errorMessage = "",
       status = 0,
       totalNumber = 20
   }
   {% endhighlight  %}
   
   
14)获取当前热门关键字
===

1. URL:  http://jjhaudio.hengdianworld.com:80/album/getHotSearchWords
2.    请求体
 {% highlight javascript %}
｛  
    "request": {}
 ｝
{% endhighlight  %}

3. 响应
   {% highlight javascript %}
   {
       keywords =  ["aa", "bb", "cc"],
       errorMessage = "",
       status = 0
   }
   {% endhighlight  %}
   
15)获取课程的课的列表
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
   
   a) 往期课程response
   
   settings表示每节课的配置，canComment表示是否能评论，maxCommentWord表示能够评论的字数
   {% highlight javascript %}
   {
       songs =  [{
                       author = "Avril Lavigne";
                       count = "50";
                       id = "1";
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       url = "http://jjhaudio.hengdianworld.com/xx.mp3",
                       listenCount = "1000";
                       name = "test";
                       listenPeople: "1100人"，
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
                       url = "http://jjhaudio.hengdianworld.com/xx.mp3",
                       listenCount = "10";
                       name = "test1";
                       listenPeople: "1100人"，
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
                       url = "http://jjhaudio.hengdianworld.com/xx.mp3",
                       listenCount = "19";
                       name = "test2";
                       listenPeople: "1100人"，
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
                       url = "http://jjhaudio.hengdianworld.com/xx.mp3",
                       listenCount = "1000";
                       name = "test";
                       listenPeople: "1100人"，
                       settings =  {
                                       canComment = true; 
                                       maxCommentWord = 20;
                                    }，
                       hasAdvImage: true,
                       advImageUrl: "http://jjhaudio.hengdianworld.com/images/default.png",
                       advUrl: "http://www.baidu.com",
                       startTime = "2016-05-19 13:00:00"，
                       endTime = "2016-05-19 17:00:00"，
                       type = Live; }
       errorMessage = "",
       status = 0,
       totalNumber = 20
   }
   {% endhighlight  %}
   
   
16)获取评论
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
               id = 1;  //Int类型
               time = "1小时前";
               userId = "jjh";
               name="张三"
           },
           {
               content = "test";
               id = 2;
               time = "1分钟前";
               userId = "test";
               name="张三"
           },
          {
               content = "test";
               id = 3;
               time = "刚刚";
               userId = "who";
               name="张三"
           }
       ];
   }
   {% endhighlight  %}


17)获取实时在线聊天记录
===

1. URL:  http://jjhaudio.hengdianworld.com:80/song/livecomments
2. 请求体
   {% highlight javascript %}
{
        request: {
            song = {id: 8},
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
               id = 1; //Int类型
               time = "1小时前";
               userId = "jjh";
               isManager = false   //是否是管理员
           },
           {
               content = "test",
               id = 2,
               time = "1分钟前",
               userId = "test",
               isManager = true
           }
       ];
   }
   {% endhighlight  %}
   
   
18)发送评论
===

1. URL:  http://localhost:3000/comment/add
2. 请求体
   {% highlight javascript %}
{
    "request": {
        comment = 'test',
        song: {id:  120}
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
   
18)发送在线评论
===

1. URL:  http://localhost:3000/comment/addLive
2. 请求体
   {% highlight javascript %}
{
    "request": {
        comment = 'test',
        lastId = '100'
        song: {id:  120}
    }
}
{% endhighlight  %}

3. 响应
   {% highlight javascript %}
{
    errorMessage = "";
    status = 0;
    comments =  [
       {
            content = "test";
            id = 1; //Int类型
            time = "1小时前";
            userId = "jjh";
            isManager = false   //是否是管理员
        },
        {
            content = "test",
            id = 2,
            time = "1分钟前",
            userId = "test",
            isManager = true
        }
    ];
}

   {% endhighlight  %}
   
   
   
19)获取在线人数
===

1. URL:  http://localhost:3000/song/livelistener
2. 请求体
   {% highlight javascript %}
{
    "request": {
        song = "{'id': 8}"   
    }
}
{% endhighlight  %}

3. 响应
   {% highlight javascript %}
{
    errorMessage = "";
    status = 0; 
    listerCount = 1000  //Int类型
}

   {% endhighlight  %}
   
20）上传用户图片
===

上传图片的请求参数和其他请求不同，请求不放在json中，把userid和token放在POST参数中，图片参数名为userimage。服务器响应和其他请求保持一致即可

1. URL:  http://localhost:3000/user/uploadprofileimage
2. 请求体

3. 响应
   {% highlight javascript %}
{
    errorMessage = "";
    status = 0; 
}
   {% endhighlight  %}


21）获取用户的头像图片
===

请求参数不放在json中，放在queryString中，userid=xxx。返回图片

1. URL:  http://localhost:3000/user/getprofileimage?userid=xxxxxx
2. 请求体

3. 响应

    响应和其他请求不同，响应体为图片，注意ContentType设置。

22)获取用户相关统计数据
===

1. URL:  http://localhost:3000/use/getstatdata
2. 请求体
   {% highlight javascript %}
{
}
{% endhighlight  %}

3. 响应
   {% highlight javascript %}
{
    errorMessage = "";
    status = 0; 
    jifen = "1000", 
    chaifu = "1000",
    teamPeople = "12人",
    tuijianPeople = " 100人",
    orderCount = "10笔"
}

   {% endhighlight  %}


23)设置昵称
===

1. URL: http://localhost:3000/user/setnickname
2. 请求体
   {% highlight javascript %}
   {
       "request": {
           newNickName: 'jjh'
       }
   }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        status = 0;
        errorMessage = "";
    }
  {% endhighlight  %}


24)获取歌曲的信息
===

1. URL: http://localhost:3000/song/getsonginfo
2. 请求体
   {% highlight javascript %}
   {
       "request": {
           id: '123'     //songid
       }
   }
   {% endhighlight  %}
3. 响应
   {% highlight javascript %}
    {
        song: {
                       author = "Avril Lavigne";
                       count = "50";
                       id = "1";
                       image = "http://jjhaudio.hengdianworld.com/images/default.png";
                       url = "http://jjhaudio.hengdianworld.com/xx.mp3",
                       listenCount = "1000";
                       name = "test";
                       listenPeople: "1100人"，
                       settings =  {
                                       canComment = true; 
                                       maxCommentWord = 20;
                                    }，
                       hasAdvImage: true,
                       advImageUrl: "http://jjhaudio.hengdianworld.com/images/default.png",
                       advUrl: "http://www.baidu.com",
                       startTime = "2016-05-19 13:00:00"，
                       endTime = "2016-05-19 17:00:00"，
                       type = Live; 
                }
        status = 0;
        errorMessage = "";
    }
  {% endhighlight  %}