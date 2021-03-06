---
{}

---
# 宝塔安装[ gd-utils](https://github.com/iwestlin/gd-utils)

# Google Drive 百宝箱

不只是最快的 google drive 拷贝工具 [与其他工具的对比](https://github.com/iwestlin/gd-utils/blob/master/compare.md)

## 配置环境

```
#node.js安装
#Debian/Ubuntu系统
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt install -y git nodejs 

#CentOS系统
curl -sL https://rpm.nodesource.com/setup_10.x | bash -
yum install nodejs git -y

git clone https://github.com/iwestlin/gd-utils && cd gd-utils
npm install --unsafe-perm=true --allow-root
```

如果之前配置过gclone的话

还是很容易的

直接将 /AutoRclone/accounts/ 的文件全部复制到/gd-utils/sa/

如果没有配置过，请看我上一篇的文章

## 修改配置文件

/root/gd-utils/config.js

主要修改的是以下内容，其余的视情况自行修改

```
  const DEFAULT_TARGET = '团队盘ID或者是目录ID' 
  client_id: 'your_client_id',
  client_secret: 'your_client_secret',
  refresh_token: 'your_refrest_token',
  以上三项如果是直接配置的SA的话就不需要修改
  tg_token: '机器人Token'
  tg_whitelist: ['个人用户名'] 

```

![image-20200630202942898](https://cdn.jsdelivr.net/gh/chenaidairong/picture/image-20200630202942898.png)

打码部分即为你自己的用户名

以上即为电报Bot的配置修改

## 宝塔安装web对接电报Bot

**Centos安装命令：**

```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```

**Centos/Ubuntu/Debian**

```
 curl -sSO http://download.bt.cn/install/install_panel.sh && bash install_panel.sh
```

**Ubuntu/Deepin安装命令：**

```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh
```

**Debian安装命令：**

```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh
```

安装web环境

宝塔安装完后打开界面会自己跳出来的，具体自行百度

建立新网站

![image-20200630203420363](https://cdn.jsdelivr.net/gh/chenaidairong/picture/image-20200630203420363.png)

域名自行修改A记录到服务器的IP地址上，不需要套CF的

回到服务器命令界面

```
npm i pm2 -g
cd /gd-utils/
pm2 start server.js
```

再次回到宝塔界面，打开网站配置
![](https://cdn.jsdelivr.net/gh/chenaidairong/picture/20200701144328.png)

设置SSL
添加反向代理

![image-20200630203807807](https://cdn.jsdelivr.net/gh/chenaidairong/picture/image-20200630203807807.png)

```
代理名称：自定
目标URL：http://127.0.0.1:23333
```

其他的不需要管

最后访问

```
你的域名/api/gdurl/count?fid=124pjM5LggSuwI1n40bcD5tQ13wS0M6wg
```

如果能出现

![img](https://github.com/iwestlin/gd-utils/raw/master/static/count.png)

说明配置成功

最后对接到电报Bot

```
curl -F "url=HTTPS://你的域名/api/gdurl/tgbot" 'https://api.telegram.org/bot电报Token/setWebhook'
```

去往你的机器人对话界面输入

/help

获取相关信息

本次教程，到此结束

![](https://cdn.jsdelivr.net/gh/chenaidairong/picture/20200701144328.png)