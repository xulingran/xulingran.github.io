title: 2020年将 Hexo 部署到 Github 上作为免费博客
abbrlink: 4668
tags:
  - Hexo
categories:
  - Hexo
top: 100
date: 2020-04-25 16:10:00
password:
copyright:
---
>我相信许多人有着想建一个属于自己的博客的想法，接下来我就来讲讲如何在 Github 上部署 Hexo 作为博客。
>本次安装环境为 Windows 10。
<!--more-->
# 配置 Hexo
## 安装 Node.js
在 Node.js 官网下载 **LTS** 版本（[点击跳转](https://nodejs.org/en/)）。在写本篇文章时 Node.js 版本为 *12.16.2*。下载后直接打开安装包，全程无脑下一步。完成后在 CMD 中输入
```bash
npm -v
```
来确认版本。
## 安装 Git
在 Git 的官网下载（[点击跳转](https://git-scm.com/downloads)）。在写本篇文章时 Git 版本为 *2.26.2* 。依旧无脑下一步。
安装完成后在 CMD 中输入

```bash
git --version
```
来查验 Git 是否安装成功。
## 将 npm 源更换为阿里源（可选）
**注意：若本步您未选择更换源，则请将后续的所有`cnpm`命令更改为`npm`。**
输入命令，将源更换为阿里源。
```bash
npm config set registry https://registry.npm.taobao.org
```
验证是否更换成功,若返回`https://registry.npm.taobao.org`，说明镜像配置成功。
```bash
npm config get registry
```
安装 cnpm（若不换源，可无视）
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
## 下载 Hexo
在硬盘中新建一个文件夹用来放 Hexo ，这里我选择在D盘新建 blog 文件夹来存放 Hexo 文件。在打开 blog 文件夹后，右键选中 Git Bash Here ，在打开的窗口中输入
```bash
cnpm install -g hexo-cli
```
在完成后，输入
```bash
hexo init
```
在文件夹中安装 Hexo 。这一步可能需要较长时间，所以请耐心等候。
完成后依次输入（分别为生成文件和启动服务）

```bash
hexo g
```
```
hexo s
```
执行完成后，你就可以访问（[http://localhost:4000](http://localhost:4000)）来看看 Hexo 的效果了
# 主题下载
笔者比较喜欢以下两种主题，因精力有限，故仅选择 NexT 为示例安装。若有兴趣，亦可下载 Ayer 研究。***事实上，因 Ayer 主题为国人开发，主题内的`_config.yml`也有中文注释，所以相对来讲Ayer更适合初学者，也更容易配置些。***在 blog 文件夹中，用 Git Bash 执行下面的命令。

## NexT
```bash
git clone https://github.com/theme-next/hexo-theme-next themes/next
```
## Ayer
```sh
git clone https://github.com/Shen-Yu/hexo-theme-ayer.git themes/ayer
```
完成后在 blog 下的`_config.yml`中将`Theme`后的值更改为主题的名字 ，并重新生成。
**注意：冒号后必须要有一个空格**。例如我这里用的是 NexT 主题，所以就将值改为`theme: next`。*注：theme后的值为主题文件夹的名字*

# 配置 Github
## 注册一个 Github 账号
没什么好说的，注册就好了。
## 新建一个 Repositories 
新建一个名称为`【你的 Github 用户名】.github.io`的 Repositories 。注意 Repositories 的名称只能为`【你的 Github 用户名】.github.io`。不然后续很麻烦。也由此可得一个账户只能创建一个网站。就是说如果你的 Github 用户名为`example`，那么你的 Repositories 的名字就是 `example.github.io`。

# 配置SSH

在`Git Bash`中依次输入以下代码（`yourname`改为GitHub用户名，`youremail`改为GitHub的注册邮箱）

```
git config --global user.name "yourname"
```
```
git config --global user.email "youremail"
```

## 查看 SSH 密钥
查看`C:\Users\你的系统用户名\`下是否有`.ssh`文件夹，如果没有，则执行
```bash
ssh-keygen -t rsa -C "你的邮件地址"
```
来获取 SSH 密钥。完成后进入`C:\Users\你的系统用户名\.ssh`中复制`id_rsa.pub`文件中的全部内容。
## 在 GitHub 中配置 SSH 密钥
在 [GitHub首页](https://github.com/)  的右上角进入个人设置（Settings），后找到`SSH and GPG keys`，点击`New SSH key`，将之前复制的内容粘贴到`Key`框中，点击`Add SSH key`，输入密码即可。
## 检查 SSH 配置是否成功
在 CMD 中输入：
```sh
ssh -T git@github.com
```
查看状态。返回`Are you sure you want to continue connecting (yes/no)?`后输入 yes 并回车。若返回`Hi 你的GitHub用户名! You've successfully authenticated, but GitHub does not provide shell access.`
则表示 SSH 密钥配置成功！
## 上传到 GitHub
在 GitHub 的刚才创建的 Repositories 中拷贝 SSH 链接，在 blog 文件夹下的`_config.yml`中找到`deploy`并做以下配置。**冒号后要有空格**。
```sh
deploy:
  type: git
  repo: 
      Github: 这里填入刚刚复制的地址
  branch: master
```
比如我的就是
```sh
deploy:
    type: git
    repo: 
        Github: git@github.com:xulingran/xulingran.github.io.git
    branch: master
```
然后在 Git Bash 中执行
```sh
cnpm install hexo-deployer-git --save
```
完成后执行
```sh
hexo d
```
正常情况下此时你就可以登录 `http://你的 Github 用户名.github.io` 访问你的博客了。我的博客就是 ([https://lingchenblog.tk](https://lingchenblog.tk)），因为 Github 在中国访问不是很稳定，所以我在`Coding`又搭了一个一模一样的博客。如果有兴趣的话，也可以上去看看，网址是`https://xulingran.tk`。接下来我会写写如何配置 NexT 主题。

>参考：https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html

> 附录：命令示例
>
> ```bash
> hexo g = hexo generate       生成文件
> hexo s = hexo server         创建本地服务器（本地预览）
> hexo d = hexo deploy         上传至服务器
> hexo clean                   删除生成的public文件夹
> ```
>
> 更多命令可执行`hexo`命令查看

