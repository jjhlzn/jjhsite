---
layout: post
title:  "接口"
date:   2016-05-01 15:15:09 +0800
categories: jekyll update
---
 

获取课程列表
===

1. URL:  http://jjhaudio.hengdianworld.com:80/album/songs
2. 请求体
   {% highlight json %}
   {"userInfo": {
       token = "";
       userid = "";
   }, "request": {
       type = 'common';
   	   pageno = 0,
   	   pagesize = 15
   }, "client": {
       appversion = "1.0.3";
       model = 'iPhone5';
       osversion = "9.3.1";
       platform = 'iphone';
       screensize = "320.0*568.0";
   }}
   {% endhighlight  %}
3. 响应
   {% highlight json %}
   {
       albums =     
                   [{
               author = "Avril Lavigne";
               count = 50;
               id = 8;
               image = "http://jjhaudio.hengdianworld.com/images/default.png";
               listenCount = "1000\U4e07";
               name = "\U827e\U8587\U513f\U7684\U6b4c";
               type = Common;
           },
                   {
               author = "\U8881\U817e\U98de";
               count = 32;
               id = 0;
               image = "http://jjhaudio.hengdianworld.com/images/yuantengfei.jpg";
               listenCount = "10\U4e07";
               name = "\U8881\U817e\U98de\U8bb2\U5386\U53f2\U7cbe\U9009\U96c6";
               type = 'Common';
           },
                   {
               author = "\U4e45\U77f3\U8ba9";
               count = 10;
               id = 1;
               image = "http://jjhaudio.hengdianworld.com/images/default.png";
               listenCount = "19\U4e07";
               name = "\U4e45\U77f3\U8ba9\U306e\U552f\U7f8e\U7eaf\U97f3\U4e50";
               type = 'Common';
			   }],
       errorMessage = "",
       status = 0,
       totalNumber = 20
   }
   {% endhighlight  %}
   
   
获取课程的课的列表
===

1. URL:  http://jjhaudio.hengdianworld.com:80/album/songs
2. 请求体
   {% highlight json %}
｛"userInfo": {
    token = "";
    userid = "";
}, "request": {
    album = "{'id': 8}";
	pageno = 0,
	pagesize = 15
}, "client": {
    appversion = "1.0.3";
    model = iPhone;
    osversion = "9.3.1";
    platform = iphone;
    screensize = "320.0*568.0";
}｝
{% endhighlight  %}

3. 响应
   {% highlight json %}
   {
       errorMessage = "";
       songs =     ［
                   {
               date = "2016-01";
               desc = des;
               name = "Wish You Were Here";
               url = "http://jjhaudio.hengdianworld.com:80／songs/avril/Wish_You_Were_Here.mp3";
           },
                   {
               date = "2016-01";
               desc = des;
               name = innocence;
               url = "http://jjhaudio.hengdianworld.com:80／songs/avril/innocence.mp3";
           },
                   {
               date = "2016-01";
               desc = des;
               name = "Everybody Hurts";
               url = "http://jjhaudio.hengdianworld.com:80／songs/avril/Everybody_Hurts.mp3";
           }
       ];
       status = 0;
   }
   {% endhighlight  %}
   
   

获取评论
===

1. URL:  http://jjhaudio.hengdianworld.com:80/song/comments
2. 请求体
   {% highlight json %}
｛"userInfo": {
    token = "";
    userid = "";
}, "request": {
    song = "{'id': 8}",
	pageno = 0,
	pagesize = 15
}, "client": {
    appversion = "1.0.3";
    model = iPhone;
    osversion = "9.3.1";
    platform = iphone;
    screensize = "320.0*568.0";
}｝
{% endhighlight  %}

3. 响应
   {% highlight json %}
   {
       comments =     [
                   {
               content = "\U7b2c0\U884c\Uff1a\U771f\U7684\U8ba9\U4eba\U611f\U5230\U8fd9\U6863\U8282\U76ee\U8fd8\U662f\U503c\U5f97\U5173\U6ce8\U7684\Uff0c\U662f\U4ece\U5f20\U5cad\U5f00\U59cb\U7684\U3002";
               id = 1;
               time = "1\U5c0f\U65f6\U524d";
               userId = "\U90a3\U662f\U5f53\U7136";
           },
                   {
               content = "\U7b2c1\U884c\Uff1a\U672c\U6765\U60f3\U5199140\U5b57\U7684\Uff0c\U4f46\U662f\U53d1\U73b0\U5b8c\U5168\U4e0d\U591f\U3002\U4e0d\U591f\U8868\U8fbe\Uff0c\U751a\U81f3\U4e0d\U591f\U90d1\U91cd\U3002 \U65b0\U5e74\U4f0a\U59cb\Uff0c\U771f\U9ad8\U5174\U5c31\U6709\U4e86\U8fd9\U4e48\U63a5\U5730\U6c14\U7684\U8282\U76ee\U3002 \U300a\U4e2d\U56fd\U597d\U6b4c\U66f2\U300b\U770b\U7684\U6211\U7279\U522b\U723d\U3002\U8fd9\U4e48\U591a\U9009\U79c0\U8282\U76ee\Uff0c\U5728\U9009\U624b\U4ecb\U7ecd\U81ea\U5df1\U7684\U65f6\U5019\U6211\U4eec\U5feb\U8fdb\Uff0c\U56e0\U4e3a\U6240\U6709\U53f0\U8bcd\U90fd\U8001\U5957\Uff0c\U4e0d\U7ba1\U771f\U5047\U90fd\U6ca1\U6709\U4eba\U613f\U610f\U4e86\U89e3.";
               id = 2;
               time = "1\U5929\U524d";
               userId = frozenmoon;
           },
                   {
               content = "\U7b2c2\U884c\Uff1a1.\U8fd9\U662f\U4e00\U4e2a\U65b0\U821e\U53f0\Uff0c\U4ece\U6765\U6ca1\U6709\U8fc7\U7684\U5f62\U5f0f\Uff0c\U53c8\U662f\U4ee5\U63a8\U52a8\U539f\U521b\U529b\U91cf\U4e3a\U53e3\U53f7\U7684\U9009\U79c0\U3002\U6240\U4ee5\U5e74\U8f7b\U7684\U89c2\U4f17\U4eec\U5f00\U59cb\U6cb8\U817e\U4e86\Uff0c\U4efb\U4f55\U4e00\U70b9\U6e05\U9192\U7684\U6279\U5224\U90fd\U4f1a\U88ab\U89c6\U4e3a\U4e0d\U5408\U65f6\U5b9c\U7684\U51b7\U6c34\U3002";
               id = 3;
               time = "10\U5c0f\U65f6\U524d";
               userId = "\U4e00\U7247\U96ea";
           }
       ];
       errorMessage = "";
       status = 0;
       totalNumber = 20;
   }
   {% endhighlight  %}
   
   


