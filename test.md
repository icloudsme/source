---
title: hexo部署问题
tags: hexo,部署,next
grammar_cjkRuby: true
---

#### 仅在指定的单个页面page支持多说评论  

经过上面的修改，默认你新建的`page`页面都支持 多说 `/ DISQUS` 评论系统，但是我想指定仅是某个页面支持评论那怎么办呢？
例如，我仅仅是想about页面支持多说评论系统(我使用的是多说评论系统， DISQUS 评论系统就不考虑了，你们自行修改吧)
还是更改NexT主题`page.swig`文件。
`page.swig`的路径： `your-hexo-site/themes/next/layout/page.swig`
找到`page.swing`文件（没经过任何修改的，也就是经过上面提到的让你的page页面支持评论系统处理的），将下面代码
```` html
{% elif page.type === 'about' %}
   {{ page.content }}
<div class="comments" id="comments">
     <div class="ds-thread" data-thread-key="{{ page.path }}"
          data-title="{{ page.title }}" data-url="{{ page.permalink }}">
     </div>
 </div>  
 ````
 插在下面代码之间
 
 ````html
    {{ list_categories() }}
      </div>
    </div>
//代码插在这里
  {% else %}
    {{ page.content }}
````
接着将下面的代码

````
{% block comment_system %}
  {% include '_scripts/comments/duoshuo.swig' %}
{% endblock %}
````
复制到下面代码的底部


#### 为你的hexo网站NexT主题增加留言页

经过上个步骤你现在可以任意指定某些页面支持多说系统，现在我们实现指定guestbook page支持多说系统，从而实现留言功能。指定guestbook页面支持多说系统很简单，只需要把上面提到的仅在指定的单个页面page支持多说评论这例子中的page.type === 'about'改成page.type === 'guestbook'即可。修改完毕后，接下来要做的是：

1. 找到你NexT主题_config.yml（主意是NexT主题的_config.yml，不是hexo站点目录下的_config.yml），文件路径your-hexo-site/themes/next/_config.yml，添加 guestbook 到 menu 中，如下:

````menu:
  home: /
  #categories: /categories
  about: /about
  archives: /archives
  # tags: /tags
  #commonweal: /404.html
  guestbook: /guestbook
````

2. 找到你NexT主题zh-Hans.yml文件（我的网站是简体语言的），文件路径your-hexo-site/themes/next/languages/zh-Hans.yml，添加 guestbook: 留言 到 menu 中，如下:  

```` menu:
          home: 首页
          archives: 归档
          categories: 分类
          tags: 标签
          about: 关于
          commonweal: 公益404
          guestbook: 留言
````
3. 新建一个 guestbook 页面:       
`hexo new page "guestbook"`

#### NexT主题添加腾讯空间404公益页面
原来主题也有介绍了如何在增加腾讯公益404页面，但是整个页面跳了出去，我个人比较喜欢下面404页面嵌在内页这种风格
使用方法一样，新建404.html页面，将下面代码拷进去保存，放到主题的source目录下即可：
````html
<!DOCTYPE HTML>
<html>
<head>
	<title>404 - arao'blog</title>
	<meta name="description" content="404错误，页面不存在！">
	<meta http-equiv="content-type" content="text/html;charset=utf-8;"/>
	<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
	<meta name="robots" content="all" />
	<meta name="robots" content="index,follow"/>
</head>
<body>
	<script type="text/javascript" src="http://qzonestyle.gtimg.cn/qzone_v6/lostchild/search_children.js" charset="utf-8"></script>
</body>
</html>
````

Swiftype站内搜索key:jFNJNJK7GCyqEytwr1Jq 
google站点管理：<meta name="google-site-verification"

 content="fwBag2EuHaND4_Eb0vkMqQwtaz_WL_AFPRwjQNQGhrw" />
Navi
目前导航栏中「分类」和「标签」是无法正常显示的


$ cd ~/Desktop/Joe
$ hexo new page tags
$ hexo new page categories
会在 ~/Desktop/Joe/source 下创建 tags 与 categories 目录
编辑 ~/Desktop/Joe/source/tags/index.md


> 设置当前 page 类型为 tags
type: "tags"

> 设置当前页评论关闭
comments: false
编辑 ~/Desktop/Joe/source/categories/index.md


> 设置当前 page 类型为 categories
type: "categories"

> 设置当前页评论关闭
comments: false


<script>window._bd_share_config={"common":{"bdSnsKey":{},"bdText":"","bdMini":"1","bdMiniList":false,"bdPic":"","bdStyle":"0","bdSize":"16"},"slide":{"type":"slide","bdImg":"3","bdPos":"right","bdTop":"100"},"image":{"viewList":["qzone","tsina","tqq","renren","weixin"],"viewText":"分享到：","viewSize":"16"},"selectShare":{"bdContainerClass":null,"bdSelectMiniList":["qzone","tsina","tqq","renren","weixin"]}};with(document)0[(getElementsByTagName('head')[0]||body).appendChild(createElement('script')).src='http://bdimg.share.baidu.com/static/api/js/share.js?v=89860593.js?cdnversion='+~(-new Date()/36e5)];</script>


#### 设置网站图标

将 favicon 放置到站点的 source 目录下即可


#### 设定归档页面文章的篇数

若要实现首页显示 M 篇文章，而归档页面显示 N 篇文章的需求，需要两个设定：

步骤一
步骤二
安装 Hexo 插件。在站点目录下使用 npm install --save 安装如下扩展：

    hexo-generator-index
    hexo-generator-archive
    hexo-generator-tag



> 设定归档页面文章的篇数
若要实现首页显示 M 篇文章，而归档页面显示 N 篇文章的需求，需要两个设定：
步骤一
安装 Hexo 插件。在站点目录下使用 npm install --save 安装如下扩展：
>````
>    hexo-generator-index
>    hexo-generator-archive
>    hexo-generator-tag
>````
>步骤二
>安装完成后，在 站点配置文章 中，设定：
````
index_generator:
  per_page: 5

archive_generator:
  per_page: 20
  yearly: true
  monthly: true

tag_generator:
  per_page: 10
````
> 将 per_page 设定成所需要的篇数