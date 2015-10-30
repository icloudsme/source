title: hexo使用github发布博客  
date: 2015/10/30  
tags: hexo | github
 ---
#### - 本地markdown编辑博客文档
在本地新建一个filename.md文件
每一篇文章的 .md 文件开头按照这个格式
>title: #文档标题
>date: #文档日期
>cate:  #文章分类目录 可以省略
>tags:  #文章标签  可以省略
>description: #文章的描述 可以省略
>`---`
>这里开始使用markdown格式输入你的正文
***需要注意这里的---横线不要后面不要加空格，标签后面也不要加空格，否则部署时就会出现问题***
#### - 创建github仓库
创建github仓库，New repository输入名称确认

#### - 在本地创建仓库编辑
打开`gitbash`，选择本地的文件目录
输入：`mkdir github` `cd github`
初始化仓库：`git init`
写好的文章放在github仓库中,执行如下命令：

**在命令行上创建一个新的存储库**
- 添加文件

```
git add README.md
```

- 提交

```
git commit -m "first commit"
```

- 添加远程主机

```
git remote add origin https://github.com/icloudsme/xxx.git
```

- 上传本地当前分支到master分支

```
git push -u origin master
```

**从命令行中推送现有的存储库**


- 添加远程主机

```
git remote add origin https://github.com/icloudsme/xxx.git
```

- 上传本地分支到远程master

```
git push -u origin master
```

执行完毕后，文件已经同步至远程仓库
***如果在执行的时候github中有更新文件，并且只有一个分支的情况下，需要先执行下面命令***

 `git pull`命令的作用是，取回远程主机某个分支的更新，在于本地指定的分支合并
如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名`git pull origin`

#### - 在hexo更新博客
在`hexo/source/_post/`目录下执行: `git clone https://github.com/icloudsme/***.git`
把github上的博客克隆到这个目录下
在执行`hexo g d`在预览博客，文章已经发布好
这样虽然有一点麻烦，但是博客文章可以备份到github上，方面以后迁移使用