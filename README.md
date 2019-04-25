# shadowsocks-over-websocket
基于 [shadowsocks](https://zh.wikipedia.org/zh-cn/Shadowsocks) 协议的科学上网工具 , 可部署在 [Heroku](https://www.heroku.com/) 平台上 , 实现免费科学上网


## 如何部署在 Heroku 平台上

### 1.准备工作
* [Heroku](https://signup.heroku.com/) 注册
* [GitHub](https://github.com/join?source=header-home) 注册

### 2.Fork [本项目](https://github.com/VincentChanX/shadowsocks-over-websocket) 到个人账号下
![1](./imgs/1.jpg)
进入 <https://github.com/VincentChanX/shadowsocks-over-websocket> 页面  ==>  Fork

---

### 3.创建 [Heroku](https://dashboard.heroku.com/new?org=personal-apps) 应用
![2](./imgs/2.png)
登陆 Heroku 帐号，进入 [Dashboard](https://dashboard.heroku.com/apps) 页面  ==> Create New App ==> 输入 App Name  ==>  Create App

---

### 4.Heroku 帐号与 Github 帐号关联
![3](./imgs/3.jpg)
进入 Deploy 页面 ==> 选择 Deployment Method 为 Github ==> Connect to GitHub

---

### 5.选择要关联的Github项目
![4](./imgs/4.jpg)
选择GitHub帐号  ==> 查找shadowsocks-over-websocket ==> Connect

---

### 6.部署 master 分支

![5](./imgs/5.jpg)

---

### 7.配置环境变量
![6](./imgs/6.png)
Setting 页面 ==> Reveal Config Vars

配置三个环境变量：METHOD(加密方法) aes-256-cfb，PASSWORD(密码），SERVER_ADDRESS(`0.0.0.0`) 

支持以下加密方法:

* rc4
* rc4-md5
* table
* bf-cfb
* des-cfb
* rc2-cfb
* idea-cfb
* seed-cfb
* cast5-cfb
* aes-128-cfb
* aes-192-cfb
* aes-256-cfb
* camellia-256-cfb
* camellia-192-cfb
* camellia-128-cfb

---

## 启动客户端：

### 命令行启动:

1）本地安装 git：https://git-scm.com/downloads

2）本地安装 node

```
brew install node
```

3）克隆项目

```
git clone https://github.com/VincentChanX/shadowsocks-over-websocket.git ~/
```

4）进入目录

```
cd ~/shadowsocks-over-websocket
```

5）安装插件

```
npm install
```

6）打开 Shadowsocks 客户端

新增或切换到 heroku 节点：地址 127.0.0.1，端口 1080，加密方法如上，密码如上

7）杀掉 shadowsocks 本地 socks5 进程

每次提示端口占用，都要杀掉一次

```
kill -9 $(lsof -i tcp:1086 -t)
```

8）开启服务

如图查看本地 shadowsocks 客户端的 Socks5 端口，比如图片是 1086

![](https://i.loli.net/2019/04/25/5cc171e2410b2.png)

```
node local.js -s vpnxxx.herokuapp.com -l 你的Socks5端口 -m 设置的加密方法 -k 设置的密码 -p 80

# 比如我的
node local.js -s vpn999.herokuapp.com -l 1086 -m aes-256-cfb -k Qq112233 -p 80
```

** 完成以上配置后，以后只需重复 4）6）7）8） 四步即可进行科学上网，打开 https://www.google.com 试试。 ** 

PS：刚开始连接时 heroku 还处于睡眠状态，会比较慢。