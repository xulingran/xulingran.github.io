title: Hexo NexT 7.X版本配置指南
tags: Hexo
categories: Hexo
top: 
abbrlink: 31505
date: 2020-04-26 20:08:26
password:
copyright:
---
> 接下来我会讲讲如何配置NexT主题，本次使用的NexT版本为7.8。部分来自网络  
<!--more-->
# 语言设置为中文
在Hexo根目录中的`_config.yml`中，将 language后的值更改为 `zh-CN`并重新生成。如下图所示

# 设置圆形头像并增加动画

在主题的`_config.yml`中找到`avator`项，将`url`项后的#号去掉，再将`rounded`、`rotated`的值改为`true`，并将你想设置的头像名字改为avatar.gif放入`hexo根目录/source/images/`中（没有images文件夹就新建一个）

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


# 压缩博文提高访问速度
在Hexo根目录下执行
```
cnpm install hexo-neat --save
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
>
>对部分电脑来说可能会略卡

安装方法：在`/Hexo根目录/source/`下执行
```
git clone https://github.com/stevenjoezhang/live2d-widget.git
```
然后将`live2d-widget`文件夹中的`autoload.js`文件中的
```
const live2d_path = "https://cdn.jsdelivr.net/gh/stevenjoezhang/live2d-widget/";
```
改为
```
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

# 在每篇文章末尾添加“本文结束”字样

在`\themes\next\layout\_macro`中新建文件`passage-end-tag.swig`，添加以下内容

```bash
<div>
    {% if not is_index %}
        <div style="text-align:center;color: #ccc;font-size:14px;">-------------本文结束<i class="fa fa-paw"></i>感谢您的阅读-------------</div>
    {% endif %}
</div>

```

接着打开`\themes\next\layout\_macro\post.swig`文件，在`END POST BODY` 之前添加如下代码

```
<div>
  {% if not is_index %}
    {% include 'passage-end-tag.swig' %}
  {% endif %}
</div>
```

如图

# 文章置顶
>转自[Hexo 生成永久文章链接](https://zhuanlan.zhihu.com/p/134492757)
>
>在`hexo根目录`执行
```
npm uninstall hexo-generator-index
cnpm install hexo-generator-index-pin-top --save
```
使用时只需要在文章中加入`top`属性即可，top越大文章越靠前。

# 生成永久链接

## 1.安装[hexo-abbrlink](https://github.com/rozbo/hexo-abbrlink)插件
```
cnpm install hexo-abbrlink --save
```
## 2.配置
修改博客根目录配置文件 `_config.yml` 的 `permalink`：
```
# permalink: :year/:month/:day/:title/
permalink: p/:abbrlink.html  # p 是自定义的前缀
abbrlink:
    alg: crc32   #算法： crc16(default) and crc32
    rep: hex     #进制： dec(default) and hex
```
不同算法和进制生成不同的格式：
```
crc16 & hex
https://xxx.com/posts/66c8.html
crc16 & dec
https://xxx.com/posts/65535.html

crc32 & hex
https://xxx.com/posts/8ddf18fb.html
crc32 & dec
https://xxx.com/posts/1690090958.html
```
## 3.验证
```
hexo clean
hexo g
hexo s
```