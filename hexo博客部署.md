title: hexo博客部署  
date: 2015/10/30  
categories: hexo  


### 部署hexo博客

    npm install -g hexo 安装hexo
    npm install安装博客
    hexo init初始化

hexo g 生成
hexo d部署
hexo clean 清理
hexo s启动

#### 主题安装
next主题安装
>cd your-hexo-site
git clone https://github.com/iissnan/hexo-theme-next themes/next

#### 启动next主题
克隆/下载 完成后，打开 站点配置文件，找到 theme 字段，并将其值更改为 next

#### 验证主题是否启用
运行 hexo s --debug，并访问 http://localhost:4000，确保站点正确运行

#### 主题设定
选择scheme
Next通过scheme提供主题中的主体。`Mist`是Nextde第一款scheme，启用mist仅需在主题配置文件中将`#scheme： Mist`前面的#注释去掉即可

#### 语言设置
编辑站点配置文件,将`language`设置成你所需要的语言
例如选用整体中文,则配置为:
>language: zh-Hans    

