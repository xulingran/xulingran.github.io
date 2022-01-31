---
title: Mango - 自建漫画服务器
tags: 软件
categories: 软件
abbrlink: 34043
date: 2022-01-30 19:18:47
---

> 近日来想看些漫画，又不想将漫画存到本地，于是便上 Github 找了一下，果真找到了一个比较好用的漫画服务端，在这里分享一下。
>
> 系统为 Ubuntu Server 18.04 LTS
>
> 项目地址为[hkalexling/Mango:  (github.com)](https://github.com/hkalexling/Mango)，在这里简单汇总一下安装方式和我遇到的一些问题。

<!--more-->

---

# 部署

## 下载

 尽量使用`root`账户，运行：

```bash
wget https://github.com/hkalexling/Mango/releases/latest/download/mango
chmod +x mango
./mango
```

若是国内用户，可使用

```bash
wget https://github.com.cnpmjs.org/hkalexling/Mango/releases/latest/download/mango
```

在启动之后，在输出中会有新生成的 admin 账户及密码，我们接下来会使用到该账户和密码进行登录。如图![](https://one.xulingran.cn/uploads/3.png)

## 设置

进入`/root/.config/mango`文件夹并修改其中的`config.yml`文件

（不会有人不会吧）
```bash
nano /root/.config/mango/config.yml
```
config.yml文件示例，请勿直接复制：
```
---
host: 0.0.0.0 
port: 9000                                    # 这个是端口号，可以根据自己vps的端口情况修改
base_url: /
session_secret: mango-session-secret
library_path: /root/mango/library             # 这个是目录
db_path: /root/mango/mango.db
scan_interval_minutes: 5                      # 这个是扫描间隔，保持原样也能用
thumbnail_generation_interval_hours: 24
log_level: info
upload_path: /root/mango/uploads
plugin_path: /root/mango/plugins              # 插件目录，可以下载插件放到这里面
download_timeout_seconds: 30
library_cache_path: /root/mango/library.yml.gz
cache_enabled: false                          # 是否启用缓存，个人感觉没太大用
cache_size_mbs: 50
cache_log_enabled: true
disable_login: false                          # 禁用登录（没用过）
default_username: ""
auth_proxy_header_name: ""
mangadex:
  base_url: https://mangadex.org
  api_url: https://api.mangadex.org/v2
  download_wait_seconds: 5
  download_retries: 4
  download_queue_db_path: /root/mango/queue.db
  chapter_rename_rule: '[Vol.{volume} ][Ch.{chapter} ]{title|id}'
  manga_rename_rule: '{title}'
```



打开`服务器ip:端口号`用先前的密码登陆后点击 `ADMIN` 进入管理界面，点击 `User Management ` 进入账户管理，  `NEW USER` 创建新用户，输入自己日后想用的账号密码，勾选 `Admin Access` 按钮，在再点击 `SAVE `。至此就安装完了。

## 导入漫画

> 我原本以为这步会是最简单的一步，但我错了……

将你要看的漫画（文件夹）放在 `library` 目录下 ，目录格式要为

```
├── 漫画 1
│   ├── 第一册.zip
│   ├── 第二册.zip
│   ├── 第三册.zip
│   └── 第四册.zip
└── 漫画 2
    └── 第一册
        └── 第1~3章
            ├── 1.zip
            ├── 2.zip
            └── 3.zip
```

两种格式都可以。

**开始愉快的追漫吧！**

# 更多玩法

## 后台运行

不知各位发现没有，在前面步骤中运行`./mango`之后程序便一直在前台运行，一旦断开 ssh 或`CTRL + C`后程序便会终止，很不方便，因此下面我介绍几种可以后台运行的方法：

### Screen

screen 是一个很好用的软件，我们可以用它来执行很多用时很久而我们不想一直连接着 ssh 的任务，用来使 mango 后台运行属实有点小题大做，但……不管了

root 下运行

```bash
apt install screen
```

在安装完成后运行下面的命令来创建一个新的 screen 会话

```bash
screen -S mango
```

在这里我们运行`./mango`后，程序开始运行。这时候先按下`ctrl + a` 后`d`就可以安全退出screen了，此时 mango 依然在运行，我们的目的也达成了。

```bash
# 补充一些screen 命令
screen -S xxx # 生成一个名为 xxx 的screen
screen -r xxx # 重新连接到 xxx
screen -D -r xxx #踢掉前一用户在登陆，适用于尝试登陆时发现 screen attached
screen -ls # 查看在运行的 screen
screen -X -S xxx quit # 关闭 xxx 的 screen
```

另外转载一下 [SiyuanChen的博客](https://www.cnblogs.com/siyuan1998/p/10706814.html)

```
3.1 Screen分屏命令：
输入命令：screen使用工具
上下分屏：ctrl + a  再按shift + s
切换屏幕：ctrl + a  再按tab键
新建一个终端：ctrl + a  再按c
关闭一个终端：ctrl + a  再按x （或直接输入exit退出）
```

### nohup

这种方法的好处是不需要安装额外的软件

运行命令：

```bash
nohup ./mango > mango.log 2>&1 &
# 解释：nohup就是不挂起的意思，将mango直接放在后台运行，并把终端输出存放在当前
# 目录下的mango.log文件中。当客户端关机后重新登陆服务器后，直接查看mango.log文件就可看执行结果
```

(究极缝合怪)引用[*求知之人*的博客]([使程序在Linux下后台运行 - andy_1 - 博客园 (cnblogs.com)](https://www.cnblogs.com/andylhc/p/9721705.html))

```
linux后台运行命令nohup和&的区别
1.&的意思是在后台运行， 什么意思呢？  意思是说， 当你在执行 ./a.out & 的时候， 即使你用ctrl C,  那么a.out照样运行（因为对SIGINT信号免疫）。 但是要注意， 如果你直接关掉shell后， 那么， a.out进程同样消失。 可见， &的后台并不硬（因为对SIGHUP信号不免疫）。
2.nohup的意思是忽略SIGHUP信号， 所以当运行nohup ./a.out的时候， 关闭shell, 那么a.out进程还是存在的（对SIGHUP信号免疫）。 但是， 要注意， 如果你直接在shell中用Ctrl C, 那么, a.out进程也是会消失的（因为对SIGINT信号不免疫）
3.所以， &和nohup没有半毛钱的关系， 要让进程真正不受shell中Ctrl C和shell关闭的影响， 那该怎么办呢？ 那就用nohua ./a.out &吧， 两全其美。
```

## 下载插件

我们还可以在[这里](https://github.com/hkalexling/mango-plugins)下载自己喜欢的插件，来拓展更多功能。

里面有一些漫画网站的插件，可以让你方便的下载漫画到你的漫画服务器上观看。

但似乎有些年久失修，请各位自行尝试。

## 多人运动(bushi

[之前](#设置)也说过，在`User Management`中可以增加用户，所以我们可以给朋友也开几个账号（当然不用有 admin access ），大家一起愉快的玩耍！

## 利用反向代理，使其变成可访问的网站

可利用反向代理，更方便访问，不需要记忆端口号和ip。具体方法这里不过多赘述。各位可自行百度。

---

谢谢观看。



