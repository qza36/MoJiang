---
title: 使用Hexo搭建博客并部署在自己的服务器上
date: 2023-04-15 20:33:46
tags: 教程
---
# 前言
* 本教程将会教会你如何从本地进行博客调试然后推送到自己的服务器上，最后用户只需输入你的域名即可访问你的博客。
* 此教程需要一个外部服务器。
* 信息来源：
    * Hexo官网：<https://hexo.io/zh-cn/docs/>
    * Archlinux官网（中国）：<https://wiki.archlinuxcn.org/wiki/Nginx>
    * 只会玩辅助的博客：<https://www.cnblogs.com/wangcuican/p/12522239.html>
* 图床支持：<https://imgloc.com/>
# 本地上的准备工作（Windows环境）
## 安装Node.js
1. 从官网下载[Node.js](https://nodejs.org/en)
2. 下载到本地后，默认安装就行
## 安装Hexo
 打开cmd，输入`npm install -g hexo-cli` 看到以下内容就说明安装成功了<a href="https://imgloc.com/i/iEfifQ"><img src="https://i.328888.xyz/2023/04/15/iEfifQ.md.png" alt="iEfifQ.png" border="0" /></a>
## 安装Git
[官网下载Git](https://git-scm.com/download/win),下载完成后默认安装就可以了

# 服务器上的准备工作（Archlinux环境）<br>[此步并没有什么卵用，可以滤过]
## 购买服务器
## 安装git
> pacman -S git
## 购买域名
这里大家就随意发挥吧。
# 开始搭建博客

## 本地搭建

 本地搭建博客是为了更好的编写文章，相比服务器上枯燥的黑底白字，Windows上的编辑器用起来更加的舒服。而且，在本地可以及时查看博客生成的网页，并作出修改。万事俱备后，就可上传到服务器了。

### 搭建博客

在本地上新建个文件夹，我命名为Blog，大家可以随便取名字。<br>
进入到Blog，然后***在当前目录***打开cmd。<br>
在CMD中输入`hexo i`此命令会在Blog文件夹中生成若干文件。<br>
接着输入`hexo g`<br>
<a href="https://imgloc.com/i/iEUbnt"><img src="https://i.328888.xyz/2023/04/15/iEUbnt.md.png" alt="iEUbnt.png" border="0" /></a><br>
待命令完成后，输入`hexo s` ，浏览器打开箭头所指的网址，要是看见hello，world说明本地搭建已经成功啦<br>
<a href="https://imgloc.com/i/iEUjRJ"><img src="https://i.328888.xyz/2023/04/15/iEUjRJ.md.png" alt="iEUjRJ.png" border="0" /></a>

### 新建博客

在博客文件夹里打开CMD输入`hexo n <博客的标题>`，就会生成一个后缀名为md的文档。
<a href="https://imgloc.com/i/iEU7oa"><img src="https://i.328888.xyz/2023/04/15/iEU7oa.png" alt="iEU7oa.png" border="0" /></a><br>
我们要编写那个文档，支持Markdown和html，内容编写好后就使用`hexo g` 来生成html文件，他们储存在`/Blog/public`里，你可以通过`hexo s`来查看实际的效果

### 使用Git来实现本地和服务器的同步，当然，你也可以直接使用FTP来传送文件。
* 建立本地仓库
    * 进入Blog文件夹，鼠标右键，选择`Git Bash Here`
    * 在git终端输入`git init`<br>
    <a href="https://imgloc.com/i/iEUJyZ"><img src="https://i.328888.xyz/2023/04/15/iEUJyZ.png" alt="iEUJyZ.png" border="0" /></a>
    *  将本地代码放入暂存区 ，输入 `git add . `(add 后有个点，别漏了) <br>
    <a href="https://imgloc.com/i/iEUYtX"><img src="https://i.328888.xyz/2023/04/15/iEUYtX.md.png" alt="iEUYtX.png" border="0" /></a>
    * 输入`git status` 若文件都是绿色说明没有问题。<br>
    <a href="https://imgloc.com/i/iEnfGo"><img src="https://i.328888.xyz/2023/04/15/iEnfGo.png" alt="iEnfGo.png" border="0" /></a>
    * 输入git commit -m ' 提交信息'    把暂存区的文件放到版本库中
    <a href="https://imgloc.com/i/iEnO2p"><img src="https://i.328888.xyz/2023/04/15/iEnO2p.md.png" alt="iEnO2p.png" border="0" /></a>
* 推送代码到Github
    * 在github上建立一个库
    * 生成并部署公钥
    >本机命令，生成公钥：ssh-keygen -t rsa -C "*@*.com"  邮箱可以任意填写<br>
    >本机命令，查看公钥：cat ~/.ssh/id_rsa.pub   查看之后然后copy
    >github线上添加公钥：项目仓库 => settings => SSH and GPG keys => New SSH key <br>
    把生成的公钥填入即可。
    * 本地仓库与远程仓库建立连接，添加远程源，这里我们采用ssh协议
    >git remote add origin git@github.com:qza36/PocchiBlog.git      #origin是远程源的名字
    <a href="https://imgloc.com/i/iEtB3w"><img src="https://i.328888.xyz/2023/04/16/iEtB3w.png" alt="iEtB3w.png" border="0" /></a>
    * 提交本地仓库代码到远程仓库
    >git push -u origin master origin是远程源的源名，可以自定义；master是分支名，是默认的主分支
    * 至此，本地搭建到推送代码到远程仓库教程已结束
### 
## 服务器搭建

# 新建博客
* 在`/home`目录下建立一个空文件夹,就叫Blog吧。
* 然后在终端输入`git init`
* 生成并部署公钥
    >本机命令，生成公钥：ssh-keygen -t rsa -C "*@*.com"  邮箱可以任意填写<br>
    >本机命令，查看公钥：cat ~/.ssh/id_rsa.pub   查看之后然后copy
    >github线上添加公钥：项目仓库 => settings => SSH and GPG keys => New SSH key <br>
    把生成的公钥填入即可。
* 本地仓库与远程仓库建立连接，添加远程源，这里我们采用ssh协议
    >git remote add origin git@github.com:qza36/PocchiBlog.git      #origin是远程源的名字
    <a href="https://imgloc.com/i/iEtB3w"><img src="https://i.328888.xyz/2023/04/16/iEtB3w.png" alt="iEtB3w.png" border="0" /></a>
* 拉取远程仓库代码
    >git pull origin master


# 代理服务器（Nginx）安装及配置
1. 安装Nginx，`pacman -S Nginx`
2. 修改配置文件，`vim /etc/nginx/nginx.conf` 找到以下内容，修改` root`后面的内容。<br>
这个代码的意思是：Nginx会在` /home/blog/publc`里寻找`index.html index.html`<a href="https://imgloc.com/i/iEycJc"><img src="https://i.328888.xyz/2023/04/15/iEycJc.md.png" alt="iEycJc.png" border="0" /></a><br>
<i>**注意** </i>: 不推荐将博客文件夹建立在<i>操作系统</i>root目录下，这样做可能会导致404错误。

3. 修改后保存，然后在在终端输入`nginx -s reload` 

5. 记得打开防火墙
    >sudo ufw allow http
    >sudo ufw allow https

4. 输入自己的域名就可以访问啦（前提是要把自己的域名解析到服务器哦）


## 注意事项
* 一定要`hexo g`后提交代码
* 不要在root目录下建博客文件夹！



 




