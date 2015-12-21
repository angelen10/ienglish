# ienglish
title: 史上最详细“截图”搭建Hexo博客——For Mac
date: 2015-11-10 16:10:46
tags: [DevTools, Mac]
photos: 
- http://7u2ogo.com1.z0.glb.clouddn.com/github+hexo.png
---

环境准备：
>- 首先hexo是基于nodejs的，所以必须安装nodejs
>- 安装nodejs方法很多，我选择homebrew安装方式，所以需要安装它
>- 安装homebrew就很简单了，mac自带ruby脚本功能，一句话搞定
>- hexo提交部署github需要使用git工具，所以需要安装git，用homebrew的话也是一句话搞定
>- OK整理一下安装顺序：homebrew-nodejs-hexo-git

## 1.安装Homebrew
官网地址：http://brew.sh/
打开终端窗口, 粘贴以下脚本。
```ruby
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
安装完成之后，在终端输入
```ruby
brew
```
如果出现以下信息，说明你已经安装Homebrew成功。
![](/images/20151110/01-01-check Homebrew.png)
## 2.安装Node.js
打开终端窗口, 粘贴以下脚本。
```ruby
brew install node
```
## 3.安装Hexo
使用Node.js自带的npm命令安装。打开终端窗口, 粘贴以下脚本。
```ruby
npm install -g hexo
```
![](/images/20151110/03-01-npm install -g hexo.png)
```ruby
hexo init
```
![](/images/20151110/03-02-hexo init.png)
```ruby
npm install
```
![](/images/20151110/03-03-npm install-1.png)
![](/images/20151110/03-04-npm install-2.png)
## 4.安装Git
在终端继续输入以下命令。
```ruby
sudo brew install git
```
P.S.当你运行该命令的时候，你有可能被提示以下Error：
```error
Cowardly refusing to 'sudo brew install'
```
此时，只要给予权限即可。输入以下命令。
```ruby
sudo chown root /usr/local/bin/brew
sudo brew install git
```
如下图所示：
![](/images/20151110/04-01-sudo brew install git.png)
## 5.本地查看
输入以下命令：
```ruby
hexo g
hexo s
```
P.S.hexo g和hexo s都是简写，详情请浏览文章底部Tips。
![](/images/20151110/05-01-local check.png)
在浏览器输入：
```url
http://0.0.0.0:4000/
```
效果如下：
![](/images/20151110/05-02-visual effect.png)
如果出现了以上的画面，说明你已经搭建本地博客成功。
## 6.部署到Github上
### 6.1注册Github账号
这里不演示了。
### 6.2创建Repository
创建的时候注意Repository的名字。比如我的Github账号是angelen10，那么我应该创建的Repository的名字是：angelen10.github.io。
![](http://7u2ogo.com1.z0.glb.clouddn.com/My-New-Start-3.png)
### 6.3修改配置文件
到你刚刚创建的Repository下，找到以下内容：
![](http://7u2ogo.com1.z0.glb.clouddn.com/My-New-Start-4.png)
先点击HTTPS，然后复制里面的地址。然后编辑_config.yml文件（在你所创建的Hexo路径下）。
修改文件里面的deploy。
![](/images/20151110/06-01-modify_deploy.png)
其中的repository就改成你刚刚复制的地址。注意，hexo更新到3.0之后，deploy的type的github需要改成git。如果不是3.0之后的版本，可能type是github，这个我没有试过。
同时，在命令行输入：
```ruby
npm install hexo-deployer-git --save
```
![](/images/20151110/06-02-hexo 3.0.png)
### 6.4设置SSH keys
在终端输入以下命令：
```ruby
ssh-keygen -t rsa -C "angelen10@163.com"
```
![](/images/20151110/06-04-SSH keys01.png)
然后它会提示要你输入passphrase（如上图，我没有输入直接回车，如果你输入的话，要记得，到时候会用到）。
继续输入：
```ruby
ssh-agent -s
```
![](/images/20151110/06-05-ssh-agent -s.png)
继续输入以下指令：
```ruby
ssh-add ~/.ssh/id_rsa
```
![](/images/20151110/06-06-add.png)
如果出现以上问题，输入以下指令：
```ruby
chmod 700 id_rsa
```
再次输入刚刚的指令：
```ruby
ssh-add ~/.ssh/id_rsa
```
![](/images/20151110/06-08-add success.png)
虽然还是有警告，但是起码文件是添加成功了。
### 6.5进入Github设置，添加SSH key
![](/images/20151110/06-09-Github Settings.png)
![](/images/20151110/06-10-SSH KEY Add.png)
第④步的内容就是.ssh目录下的id_rsa.pub文件里面的内容。
### 6.6授予Github权限
Add key之后，在终端输入：
```ruby
ssh -T git@github.com
```
![](/images/20151110/06-11-ssh -T git@github.com.png)
### 6.7完成部署
最后一步，快要成功了，键入指令：
```ruby
hexo g
hexo d
```
OK，我们的博客就已经完全搭建起来了，在浏览器输入（当然，是你的用户名）：
```ruby
http://angelen10.github.io/
```
![](http://7u2ogo.com1.z0.glb.clouddn.com/My-New-Start-20.png)
注意：每次修改本地文件后，需要键入hexo generate才能保存。每次使用命令时，都要在Hexo目录下。每次想要上传文件到Github时，就应该先键入hexo g保存之后，再键入hexo d。大概成功之后是酱紫的：
![](http://7u2ogo.com1.z0.glb.clouddn.com/My-New-Start-21.png)
对了，记住上图的Username是你的Github账号名称，而不是邮箱；Password就是你的Github的密码。

Tips
-----
hexo现在支持更加简单的命令格式了，比如：
```ruby
hexo g == hexo generate
hexo d == hexo deploy
hexo s == hexo server
hexo n == hexo new
```
参考文章
-----------
我的成功搭建Hexo离不开广大网友的帮助，谢谢Google和度娘，还有Q群的大神的帮助。
http://www.cnblogs.com/mjiayou/p/3791373.html
http://zipperary.com/categories/hexo/
http://ibruce.info/2013/11/22/hexo-your-blog/
http://blog.163.com/gis_warrior/blog/static/19361717320153100184696/
福利
-----------
为感谢看这篇文章，送个女朋友给你：
´´´´´████████´´´´
´´`´███▒▒▒▒███´´´´´
´´´███▒●▒▒●▒██´´´
´´´███▒▒▒▒▒▒██´´´´´
´´´███▒▒▒▒██´
´´██████▒▒███´´´´´
´██████▒▒▒▒███´´
██████▒▒▒▒▒▒███´´´´
´´▓▓▓▓▓▓▓▓▓▓▓▓▓▒´´
´´▒▒▒▒▓▓▓▓▓▓▓▓▓▒´´´´´
´.▒▒▒´´▓▓▓▓▓▓▓▓▒´´´´´
´.▒▒´´´´▓▓▓▓▓▓▓▒
..▒▒.´´´´▓▓▓▓▓▓▓▒
´▒▒▒▒▒▒▒▒▒▒▒▒
´´´´´´´´´███████´´´´
´´´´´´´´████████´´´´´´
´´´´´´´█████████´´´´´
´´´´´´██████████´´´
´´´´´´██████████´´
´´´´´´´█████████´
´´´´´´´█████████´
´´´´´´´´████████´´´
________▒▒▒▒▒
_________▒▒▒▒
_________▒▒▒▒
________▒▒_▒▒
_______▒▒__▒▒
_____ ▒▒___▒▒
_____▒▒___▒▒
____▒▒____▒▒
___▒▒_____▒▒
███____ ▒▒
████____███
█ _███_ _█_███







