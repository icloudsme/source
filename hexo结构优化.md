title: hexo结构优化  
date: 2015/10/30  
tags: hexo | 多说 
 
---  
0x00 Hexo结构优化

http://go.kieran.top/post/1/
├── languages          #多语言
|   ├── default.yml    #默认语言
|   └── zh-CN.yml      #中文语言
├── layout             #布局，根目录下的*.ejs文件是对主页，分页，存档等的控制
|   ├── _partial       #局部的布局，此目录下的*.ejs是对头尾等局部的控制
|   └── _widget        #小挂件的布局，页面下方小挂件的控制
├── source             #源码
|   ├── css            #css源码 
|   |   ├── _base      #*.styl基础css
|   |   ├── _partial   #*.styl局部css
|   |   ├── fonts      #字体
|   |   ├── images     #图片
|   |   └── style.styl #*.styl引入需要的css源码
|   ├── fancybox       #fancybox效果源码
|   └── js             #javascript源代码
├── _config.yml        #主题配置文件
└── README.md          #用GitHub的都知道

0x01 多说
一个博客怎么能连评论都没有呢 所以第一件事就是改评论插件

打开文件 themes\tyrant\layout_partial\comment.ejs
把默认的评论代码部分Disqus全删了
然后在多说进行注册，获得通用代码,将通用代码粘贴到如下位置：

```
<% if ( page.comments){ %>
<section id="comment">
```

通用代码 //注意：在加入多说的通用代码后需要填入三个参数，否则你会发现所以评论都会出现在每篇文章后面

```
</section>
<% } %>
```

下面是需要修改的地方


```
<div class="ds-thread" data-thread-key="请将此处替换成文章在你的站点中的ID" data-title="请替换成文章的标题" data-url="请替换成文章的网址"></div>div>
```

把上面三个参数分别改为post.path post.title post.permalink 就好了。
代码是:


```
<div class="ds-thread" data-thread-key="<%= page.path %>" data-title="<%= page.title %>" data-url="<%= page.permalink %>"></div>
```

0x02 博客标题 .ico 图标

我认为每个博客都应该有一个独有的图标，就跟每个手机APP的图标都不一样
这个图标会显示在浏览器顶栏，收藏夹，可以有效区别于别的博客

在Hexo下，你可以把你的 fanvico.ico 文件放在source目录下
然后在 `themes/light/layout/_partial/head.ejs` 里将
 `<link href=”<%- config.root %>favicon.png” rel=”icon”> 替换为 <link href=”<%- config.root %>favicon.ico” rel=”icon” type=”image/x-ico”>`
就可以了

0x03 载入加速

哦！F[纯洁]K！！！
为什么我本地环境都加载这么慢！！！好几秒才能打开博客！！！
搞毛线啊！！！
愤怒的我决定揪出幕后黑手

F12 打开Chrome 的调试工具
切换到 Network ,然后打开博客
这里会把加载的资源及时间列出来，其他都比较正常都是毫秒级别的，只有两个（从googleapis加载jquery和字体）超时了
Google 你懂的 替换替换！！！

找到 `hexo\themes\light\source\css\ _base\variable.styl`
把`//@import url(“https://fonts.googleapis.com/css?family=Droid+Serif:400italic,700italic,400,700“)`
替换成`//@import url(“https://fonts.useso.com/css?family=Droid+Serif:400italic,700italic,400,700“)`
即把谷歌字体库替换成360的国内谷歌字体库

找到 `themes\light\layout_partial\afterfooter.ejs`
将第一句js里的jQuery资源改成官网的 “`//code.jquery.com/jquery-2.0.3.min.js`”

刷新！几乎秒开！
爽歪歪！

