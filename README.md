# 网易云音乐升级

调用官方接口，每天自动刷完300首歌，一个账号平均耗时为1分钟左右。放在服务器运行即可不需要人工干预，每天自动听歌做任务，向你的微信发送任务通知，支持无服务器的云函数部署。api接口项目地址：[https://github.com/ZainCheung/netease-cloud-api](https://github.com/ZainCheung/netease-cloud-api)

<p align="center">
    <a href="https://github.com/ZainCheung"><img alt="Author" src="https://img.shields.io/badge/author-ZainCheung-blueviolet"/></a>
    <img alt="PHP" src="https://img.shields.io/badge/code-Python-success"/>
    <img src="https://visitor-badge.glitch.me/badge?page_id=ZainCheung.netease-cloud"/>
</p>


[💡 总体介绍](#总体介绍)

[🐛 部署Python项目的三种方法](#部署项目)

[🚩 部署API接口的三种方法](#部署接口)

[📌 配置账号](#配置账号)

[📷 效果演示](#效果演示)

[🎁 下载地址](#下载地址)

[📋 查看日志](#查看日志)

[🔔 注意事项](#注意事项)

[🎨 项目结构](#项目结构)

[👻 免责声明](#免责声明)

------



# 总体介绍

这个项目可以做到的功能有：

1. 每天自动登陆听完300首歌
2. 每天自动向你的微信推送听歌任务进度

这个项目分为Python客户端和API接口（服务器），一共两个项目，各有三种部署方法。Python项目的部署最简单的是**云函数法**，API项目的部署最简单的是**直接复制项目法**

自己搭建API和申请Server酱**并不是并须**的，没有的话项目也可以运作，只是开发者觉得自己搭建API比较安全，用别人的API别人悄悄加后门你都不知道，当然开发者的API已经公开并且所有代码都开源了，肯定是没有后门的，大家可以拿去用。至于Server酱是为了让你每天知道进度以及项目有没有出问题，也不是必须要加的。

所以你想快速使用的话，可以**直接看部署Python项目的云函数法**和后面的部分，部署API项目可以不看。

当你成功运作项目后如果想学习自己搭建API接口再回来看API这一部分。

无论采取哪一种方式部署，都要看**配置账号**这一部分，很简单却也很重要！！！

更多内容请看**其他事项**



------



# 部署项目

## 云函数

**全民升级时代来了！项目支持了云函数！！！**

什么是**云函数**？就是可以让你没有服务器、本地电脑不用下载Python也可以使用这个项目，而且还是**白嫖**！

既解决了很多人部署的麻烦，也给了那些被劝退的朋友回来的勇气，**十分钟**便可以全部弄完。

### 1. 进入云函数

这里拿腾讯云的云函数做个案例，没有的可以免费开通一下，地址：[https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default](https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default)

### 2. 新建函数

函数名随意，运行环境选**Python 3.6**，创建空白函数，然后下一步

![新建函数](https://s1.ax1x.com/2020/06/29/Nhgyod.png)

### 3. 上传代码

确保环境为python 3.6，执行方法改为：`index.main`，提交方式一定要选本地文件夹，然后从GitHub项目克隆Zip压缩包，解压成文件夹，然后点击这个上传把文件夹上传进来，完了后点击下面的高级设置。

![](https://s1.ax1x.com/2020/06/29/NhWswF.png)

### 4. 高级设置

内存用不了太大，**64MB**就够了，超时时间改为最大的**900秒**，然后点击最下面的完成。

![](https://s1.ax1x.com/2020/06/29/Nh251x.png)

### 5. 配置账号

自己改下`init.config`里的账号密码以及Server酱密匙，用到多账号的也要配置`account.json`，做完后点击保存并测试。如果你的配置没有错，稍等几分钟便可以看到结果，在此期间不要刷新页面。结果会在自行日志里。

![](https://s1.ax1x.com/2020/06/29/NhR62t.png)

### 6. 设置定时

点击左边的触发管理，然后新建触发器，触发周期为自定义，表达式就是每天的什么时候做任务，我选择的早上8点30分，可以自行修改，填好后点击提交即可，到此你的每日听歌项目便部署完成，感谢使用！！

![](https://s1.ax1x.com/2020/06/29/NhWZIH.png)

------

## 本地使用

> 本地部署需要电脑下载并**安装配置好Python**

### 1. 下载项目

克隆项目到本地

```bash
git clone https://github.com/ZainCheung/netease-cloud.git
```

或者fork本项目到你的仓库进行克隆

又或者在项目仓库直接下载ZIP压缩包，这些都是可以的

### 2. 安装依赖

> 需要安装的依赖目前只有一个`request`，如果运行报错缺少什么模块就给什么模块加进`requirements.txt`中

```bash
pip install -r requirements.txt
```

### 3. 配置账号见后文

### 4. 启动程序

> 程序需要`python3`的运行环境，如果没有请自行下载安装配置，，启动程序前一定要先配置账号，然后再启动程序

```
python main.py
```

------



## 服务器部署

推荐使用宝塔面板，在宝塔应用商店里面有一个Python项目管理器，下载安装，并选择3.0以上版本，推荐3.7.2版本.

### 1. 下载安装Python项目管理器

![](https://s1.ax1x.com/2020/06/28/Ngr2K1.png)

### 2. 新建项目

> 这里的netease-cloud就是这个项目的文件夹,我给放在了/www/wwwroot/路径下了,可见我这里下载安装的是3.7.2版本的python框架选择Python，启动方式也为Python，启动文件选择`main.py`端口不用填，勾选安装模块依赖，是否要开机启动自己随意咯，然后确定。

![](https://s1.ax1x.com/2020/06/28/Ng6lE6.png)

![](https://s1.ax1x.com/2020/06/28/NgsKz9.png)

### 3. 确定运行状态

![](https://s1.ax1x.com/2020/06/28/Ng6egJ.png)

这时候项目就开始在运行了，就可以去项目在文件夹的路径，找到`run.log`即可查看运行日志

部署前也要记得先配置，然后再部署

------

# 部署接口

建议新手使用自动托管方式，可以完全不需要编程基础即可搭建api接口，推荐使用网站：[https://glitch.com/](https://glitch.com/)

这个网站是国外的，名气也很大，在上面托管网站的有几百万，免费使用，缺点就是速度没有国内的服务器快，还有就是如果没有访问了，一定时间后会进入休眠，等待下一次请求到来后需要等待几秒的解冻时间。不过这些对这个项目并没有什么影响，所以可以放心部署。

API项目地址：[https://github.com/ZainCheung/netease-cloud-api](https://github.com/ZainCheung/netease-cloud-api)

下面三种方法，第一种第二种最简单但速度慢，而且需要你有网站账号，第三种访问速度快但需要你有服务器，大家自己取舍，但基本上有服务器了都想自己搭建吧，大家随意

## 从GitHub导入项目

1. fork这个API项目到你的仓库

2. 打开网站注册并登陆，新建项目，选择从GitHub导入，地址为本项目的git地址
3. 修改你的glitch项目名，例如：netease-test
4. 那么你的接口名为“项目名.glitch.com”：https://netease-test.glitch.me/
5. 访问你的接口看到欢迎页面即部署成功

使用这种方式部署网站接口，0成本且快速可用，且不用担心环境部署运维等问题，当然如果有条件用自己的服务器搭建也是可以的。

#### 1. fork项目

感谢Star

![](https://s1.ax1x.com/2020/06/29/NWoCGj.png)

#### 2. 导入项目

填入你的的git地址,地址在你的Github项目的clone按钮里,要用https

![](https://s1.ax1x.com/2020/06/29/NWo8L6.png)

改自己项目名

![](https://s1.ax1x.com/2020/06/29/NWocTS.png)

------



## 复制项目

或者可以直接复制一份这个API项目成为你的项目,进入开发者的api服务器： https://glitch.com/edit/#!/netease-cloud-api 选择右上角的 `Remix to Exit`，即可成为你自己的项目，你便可以对代码进行修改，自定义你的域名

![](https://s1.ax1x.com/2020/06/29/NWTJcn.png)

------



## 服务器部署

部署到服务器，对于新手还是比较建议安装宝塔面板，然后就可以在浏览器中进行界面化操作，免得有的人不会Linux的命令行。

#### 1. 下载PHP

确保下载了PHP,版本不要太老就行

![](https://s1.ax1x.com/2020/06/29/NWh7Ps.png)

#### 2. 添加网站

填入你提前在你的域名运营商解析的域名，可以是子域名比如，api.xxxxxx.com，写个网站备注，然后根目录选择到下载的项目路径，FTP不创建，数据库不创建默认utf-8就行，程序类型PHP，版本选择下载的版本，提交即可运行你的网站.

![](https://s1.ax1x.com/2020/06/29/NWhza4.png)

![](https://s1.ax1x.com/2020/06/29/NW4Ydg.png)

#### 运行网站

这里演示域名为test.com,然后在浏览器里输入你的网站地址，看到欢迎页面即为部署成功

![](https://s1.ax1x.com/2020/06/29/NW4hS1.png)

![](https://s1.ax1x.com/2020/06/29/NWIt8s.png)

# 配置账号

> 为了保护账号信息，所有的账号密匙都打上了*号，使用时请换成自己的账号

打开`init.config`文件，进行配置

```bash
# setting.config(UTF-8)
```

第一句注释是为了声明编码格式，请不要删除该行注释

------



## 1. 账号

```bash
[token]
# 网易云音乐账号（手机号/网易邮箱）
account = 150********

# 密码，明文/MD5,建议自己去MD5在线加密网站给密码加密,然后填到下面
# 明文例如：123456abcd
# MD5例如：efa224f8de55cb668cd01edbccdfc8a9
password = bfa834f7de58cb650ca01edb********
```

`token`区域下存放个人账号信息，account存放网易云账号，password存放密码

> 注意，这里密码填写类型与后面的md5开关相关联，具体见后面介绍

------



## 2. 设置

```bash
[setting]
# 开关的选项只有 True 和 False
# 打卡网站的网址，如果失效请提issue：https://github.com/ZainCheung/netease-cloud-api/issues/new
api = https://netease-cloud-api.glitch.me/
```

api是指提供接口的服务器地址，这里提供一个Demo，源码也已经全部开源，如有对项目存在疑问欢迎查看源码，项目地址：[ZainCheung/netease-cloud-api](https://github.com/ZainCheung/netease-cloud-api)

另外想快速拥有一个一模一样的api服务并且使用自己定义的域名，那么可以按照上面项目的教程自己快速搭建

------



### 2-1. MD5


```bash
# 密码是否需要MD5加密，如果是明文密码一定要打开
# true  需要, 则直接将你的密码（明文）填入password,程序会替你进行加密
# false 不需要, 那就自己计算出密码的MD5，然后填入上面的password内
md5Switch = false
```

md5开关，如果自己不会加密md5，那么将这个开关置为true，并且将你的密码（明文）填入password，程序会为你加密。如果已经知道密码的md5，则将这个开关置为false，将md5填入上面的password内

**自己制作MD5时一定要是32位小写！！！**

------



### 2-2. 多账号

```bash
# 是否开启多账号功能,如果打开将会忽视配置文件里的账号而从account.json中寻找账号信息
# 如果选择使用多账号,请配置好account里的账号和密码,即account和password,而sckey不是必需的,如果为空则不会进行微信推送
# 介于账号安全着想,account.json中的密码必须填写md5加密过的,请不要向他人透露自己的明文密码
peopleSwitch = false
```

这个开关是为那些拥有多账号或者准备带朋友一起使用的朋友准备的，正如注释所说，如果你有多个账号，都想使用这个服务，那么可以打开`peopleSwitch`置为true，那么配置文件里的账号就会被程序忽略，直接读取`account.json`中的账号信息，关于`account.json`的配置在后面。

------



### 2-3. 微信提醒

```bash
# Server酱的密匙,不需要推送就留空,密匙的免费申请参考:http://sc.ftqq.com/
sckey = SCU97783T70c13167b4daa422f4d419a765eb4ebb5ebc9********
```

Server酱，是一个可以向你的微信推送消息的服务，并且消息内容完全自定义，使用之前只需要前往官网，使用GitHub登陆，扫码绑定微信，便可以获得密匙，从此免费使用Server酱

------



## 3. 配置多账号

第一次打开`account.json`，内容会是这样

```json
[
    {
        "account": "ZainCheung@163.com",
        "password": "10ca5e4c316f81c5d9b56702********",
        "sckey": "SCU97783T70c13167b4daa422f4d419a765eb4ebb5ebc9********"
    },
    {
        "account": "150********",
        "password": "bfa834f7de58cb650ca01edb********",
        "sckey": "SCU97783T70c13167b4daa422f4d419a765eb4ebb5ebc9********"
    },
    {
        "account": "132********",
        "password": "f391235b15781c95384cd5bb********",
        "sckey": "SCU97783T70c13167b4daa422f4d419a765eb4ebb5ebc9********"
    }
]
```

可见里面是一个数组文件，成员为账号对象，对象有三个属性，分别是账号、密码、Server酱密匙。

不同的账号对应不同的密匙，在做完这个账号的任务后会给这个密匙绑定的微信发送消息提醒，如果留空则不提醒，留空也请注意语法，记得加双引号，列举一个正确的案例

```json
[
    {
        "account": "ZainCheung@163.com",
        "password": "10ca5e4c316f81c5d9b56702********",
        "sckey": ""
    },
]
```

可见这里的`sckey`为空，那么完成任务后便不会发送消息提醒，如果不确定是否成功可以查看日志

------

# 效果演示

使用前可以看到是**9027**首

![使用前](https://s1.ax1x.com/2020/06/27/N6YGQg.png)

使用后是**9327**首，刚好涨了300首

![使用后](https://s1.ax1x.com/2020/06/27/N6tWuQ.png)



## 微信提醒

微信提醒依赖于Server酱，这是个很奈斯的工具，个人开发的一个项目，对所有人保持免费开放，需要使用GitHub登陆，然后绑定微信，拿到你的密匙，填入到配置文件的`sckey`中，或者多账号文件`account.json`中

提示的内容也可以自行修改，`main.py`文件的第143行左右的`diyText`函数里的content为提示内容，里面可以自定义提示内容，比如你不是考研党就把考研那一行删去，以及每日一句，，等等，如有需要尽情改。

看一下效果：

![微信提醒](https://s1.ax1x.com/2020/06/28/NgSrAx.png)

------



# 下载地址



api接口项目地址：[https://github.com/ZainCheung/netease-cloud-api](https://github.com/ZainCheung/netease-cloud-api)

api的Demo演示地址：[https://netease-cloud-api.glitch.me/](https://netease-cloud-api.glitch.me/)

api在线服务器：[https://glitch.com/edit/#!/netease-cloud-api](https://glitch.com/edit/#!/netease-cloud-api)

------



# 查看日志

只有本地部署和服务器部署才会生成日志文件，而用云函数搭建的不会有这个`run.log`文件，如需查看日志可以查看云函数内置的日志。

日志文件记录了程序运行的状况，程序运行中生成的所有记录都会保存在日志文件中，第一次克隆项目时，不会看到`run.log`日志文件，而在程序第一次运行时才会生成，下面看一下我在服务器上的日志：

![日志](https://s1.ax1x.com/2020/06/27/N6dRGq.png)

> 可以看到我打卡了不止一个账号，还有我朋友的号，这个就用到了多账号配置，如果你有个小迷妹，你可以帮她带着一起用，又或者你想像我一样放在服务器上使用，那么就配置一下吧

------



# 注意事项

### 1. Server酱

一定要绑定微信才会有效果

Server酱的官网地址：[http://sc.ftqq.com/](http://sc.ftqq.com/)

### 2. MD5

**制作时选择32位小写！！！**

在线“制作”MD5：[https://tool.chinaz.com/tools/md5.aspx](https://tool.chinaz.com/tools/md5.aspx)

比较建议大家使用MD5，因为别人即使知道了你的MD5，也很难还原你的密码，相对而言要安全很多，而原密码在你制作MD5时就被隐藏起来了，只有你一个人知道密码

### 3. 修改main.py

如果你的等级比较高，然后使用这个发现每次都没有听满300首，那么你可以修改程序的`start`函数（165行左右）的打卡次数，将3改大点，比如改到6就可以打卡6次

```python
for i in range(1,3):
```

如果你嫌打卡速度慢了，可以修改休眠时间，30秒改为10秒之类的，请自行调试

```
time.sleep(30)
```

### 4. 可用性

可能有人会说，直接使用网页或者电脑程序每天打卡不就好了，干嘛还要脚本。是的，使用网站和程序确实可以做到一样的效果，不过我懒啊，还总是忘事，所以就让它彻底全自动化，可能也有不少人愿意像我这样折腾一番，然后就可以坐享其成一劳永逸，每天坐等微信提醒就行。

### 5. 初衷

使用网易云也有挺久了，听的歌也挺多，但总是会听重复的歌，而重复的歌又不算进等级里去，所以还是很想升级的。

### 6. 反馈

欢迎到GitHub提Issue或者在吾爱帖子下提问题，遇到程序报错可以截图或者复制报错信息。

------

# 项目结构

```
|-- 项目文件夹
    |-- LICENSE
    |-- README.md
    |-- account.json
    |-- init.config
    |-- main.py
    |-- requirements.txt
    |-- run.log
```

`LICENSE`：开源许可证

`README.md`：项目自述文件

`account.json`：账号存放文件

`init.config`：配置文件

`main.py`：主程序

`requirements.txt`：依赖清单

`run.log`：运行日志

# 免责声明

请不要找我代挂账号，如果使用我的api请使用md5摘要密码，本项目的所有脚本以及软件仅用于个人学习开发测试，所有`网易云`相关字样版权属于网易公司，勿用于商业及非法用途，如产生法律纠纷与本人无关。

------

