title: Hexo NexT 7.X版本配置指南（更新中）
tags: Hexo
categories: Hexo
top: 50
abbrlink: 31505
date: 2020-04-26 20:08:26
password:
copyright:
---
> 接下来我会讲讲如何配置NexT主题，本次使用的NexT版本为7.8。  
<!--more-->
# 语言设置为中文
在Hexo根目录中的`_config.yml`中，将 language后的值更改为 `zh-CN`并重新生成。如下图所示
![mark](http://q9ejyjh5c.bkt.clouddn.com/blog/20200427/Om8bpJe1bw6I.png?imageslim)
# 设置圆形头像并增加动画
在主题的`_config.yml`中找到`avator`项，将`url`项后的#号去掉，再将`rounded`、`rotated`的值改为`true`，并将你想设置的头像名字改为avatar.gif放入`hexo根目录/source/images/`中（没有images文件夹就新建一个）
![mark](http://q9ejyjh5c.bkt.clouddn.com/blog/20200427/7QrPtorWGdFS.png?imageslim)
# 在侧边栏和页面底部增加版权信息
在主题文件夹下的`_config.yml`中找到`creative_commons`项，按照下图更改
![alt](/images/2.png)
其中`license`可以自选，也可以选择是否在侧边栏上启用。

# 生成`阅读更多`按钮
在正文你希望在主页不可见的部分前加入
```
<!--more-->
```
就可以了。

# 将页面底部的标签前的‘#’号改成图标
在主题配置文件中找到`tag_icon`项，改为`true`。
![mark](http://q9ejyjh5c.bkt.clouddn.com/blog/20200427/ULeajXKq6faG.png?imageslim)

# 压缩博文提高访问速度
在Hexo根目录下执行
```
npm install hexo-neat --save
```
安装Hexo-neat插件，然后在hexo的`_config.yml`的末尾添加
```
# hexo-neat
# 博文压缩
neat_enable: true
# 压缩html
neat_html:
  enable: true
  exclude:
# 压缩css  
neat_css:
  enable: true
  exclude:
    - '**/*.min.css'
# 压缩js
neat_js:
  enable: true
  mangle: true
  output:
  compress:
  exclude:
    - '**/*.min.js'
    - '**/jquery.fancybox.pack.js'
    - '**/index.js'  
```
若在生成时报错，则找到报错的文件，按上面的格式填入即可。

# 为博客网站增加live2d看板娘
>主要使用了[张书樵大神的项目](https://github.com/stevenjoezhang/live2d-widget)

安装方法：在`/Hexo根目录/source/`下执行
```
git clone https://github.com/stevenjoezhang/live2d-widget.git
```
然后将`live2d-widget`文件夹中的`autoload.js`文件中的
```
const live2d_path = "https://cdn.jsdelivr.net/gh/stevenjoezhang/live2d-widget/";
改为
const live2d_path = "/live2d-widget/";
```
然后在`/themes/next/layout/_layout.swig`中,新增如下内容：
```
<script src="/live2d-widget/autoload.js"></script>
```
最后在主题配置文件的末尾加入
```
live2d:
  enable: true
```

# 右上角增加 Follow me on GitHub 图标
在主题配置文件中找到`github_banner`，根据自己的想法改。如下图。
![mark](http://q9ejyjh5c.bkt.clouddn.com/blog/20200427/OfW4xtaUIq95.png?imageslim)