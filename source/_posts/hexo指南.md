---
title: hexo指南
date: 2017-09-23 22:45:55
tags: hexo
categories: 技术
---
<blockquote class="blockquote-left">这是一篇hexo指南</blockquote>
<!--more-->
# 环境部署

## 安装Node（必须）
&emsp;&emsp;作用：用来生成静态页面的。
&emsp;&emsp;到Node.js[官网](https://nodejs.org)下载相应平台的最新版本，一路安装即可。

## 安装Git（必须）
&emsp;&emsp;作用：把本地的Hexo内容提交到github上去。
&emsp;&emsp;到Git[官网](https://git-scm.com/)下载相应平台的最新版本，一路安装即可。安装成功之后鼠标右键菜单会有 *Git Bash Here* 选项。
- 备注：Git是一个版本管理工具，用指令来完成所有管理操作，Git也可以运行系统指令和系统指令提示符工具一样皆是命令行工具，区别在于Git可以随时跳转到你需要的目录，而系统命令提示符是从系统根目录来跳转到指定文件夹。各有千秋后面会做说明。

## 申请GitHub（必须）
&emsp;&emsp;作用：是用来做博客的远程创库、域名、服务器之类的，怎么与本地Hexo建立连接等下讲。

### GitHub端操作
#### GitHub 注册。
&emsp;&emsp;1.首先打开Github[官网](https://github.com)进行注册。
&emsp;&emsp;2.在打开的页面中点击*Sign up for GitHub*进行注册
&emsp;&emsp;3.填写信息进行注册。
- 备注：GitHub初始语言为英语（应该能看懂），看不懂可以选择用Chorme浏览器进行翻译。没有可以复制粘贴在线翻译。

#### 创建Repository
&emsp;&emsp;1.在自己GitHub主页点击右上角,创建Repository
&emsp;&emsp;2.进入创建界面后,创建一个名字是userName(你自己的GitHub用户名).github.io的Repository。
&emsp;&emsp;3.然后点击*Create repository*按钮完成创建。
#### 配置SSH Keys（很重要）
&emsp;&emsp;SSH密钥是一个用来识别值得信赖的电脑在进行GitHub一些操作时,不用输入密码。用户可以生成一个SSH密钥，并按照本节所述的方法将公共密钥添加到你的GitHub帐户。
&emsp;&emsp;个人建议你定期检查SSH密钥列表，并删除任何一个长时间没有使用的秘钥。
- 备注：没配置SSH 秘钥无法完成多端备份工作。

##### 检测电脑中是否已有SSH 秘钥
&emsp;&emsp;在你生成SSH秘钥之前,如果你有任意一个SSH秘钥,你都要检测一下;
&emsp;&emsp;检测步骤：
&emsp;&emsp;1.在任意目录右键,选择 *Git Bash*
&emsp;&emsp;2. 输入 `ls -al ~/.ssh` 命令查看是否存在SSH秘钥。
```
ls -al ~/.ssh 
# Lists the files in your .ssh directory, if they exist 
```
&emsp;&emsp;3:如果你看到有公共的SSH秘钥已经存在的话,请检测SSH列表的路径;
&emsp;&emsp;默认情况下,公共秘钥的文件名是下列之一：
+ d_dsa.pub
+ id_ecdsa.pub
+ id_ecdsa.pub
+ id_ecdsa.pub

&emsp;&emsp;如果没有一个现有的公共和私有密钥，或者不希望使用任何可用的SSH秘钥来连接到GitHub上，请生成一个新的SSH密钥。
&emsp;&emsp;如果你看到列出现有的公共和私有密钥（例如id_rsa.pub和id_rsa ），你想使用连接到GitHub上，你可以将你的SSH密钥放到ssh-agent(下面会写到)。
+ 小贴士:如果你看到的〜/ .ssh不存在或者错误，不要担心！我们将创建它，并生成一个新的SSH密钥。

##### 生成新的SSH密钥并将其添加到ssh-agent中
&emsp;&emsp;1.在任意目录右键,选择*Git Bash*
&emsp;&emsp;2.输入`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"` (将邮箱替换为你自己的地址)
```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# Creates a new ssh key, using the provided email as a label
Generating public/private rsa key pair.
```
&emsp;&emsp;3.当你提示“输入要保存密钥的文件”，然后按Enter键。接受默认文件位置。
```
Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```
&emsp;&emsp;4.在提示符下，键入一个安全密码(可以为空)。
```
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```
&emsp;&emsp;5.将ssh秘钥添加到 ssh-agent,在任意目录右键,选择Git Bash后输入命令确保ssh-agent的启用
```
# start the ssh-agent in the background
$ eval "$(ssh-agent -s)"
Agent pid 59566
```
##### 添加新的SSH密钥到你的帐户GitHub中
&emsp;&emsp;要配置GitHub的帐户需要使用新的（或现有的） SSH密钥，你还需要将其添加到你的帐户GitHub中。
&emsp;&emsp;1.复制SSH密钥到剪贴板
&emsp;&emsp;2.在GitHub任何界面中,点击右上角个人资料照片,选择*Settings*
&emsp;&emsp;3.在用户设置栏中，点击*SSH keys*
&emsp;&emsp;4.然后点击 *New SSH key*
&emsp;&emsp;5.在“Title”字段中，为新的密钥添加描述性标签。例如，如果你使用的是个人的Mac ，你可以调用这个关键的“个人的MacBook Air ” 。
&emsp;&emsp;6.粘贴刚才复制的秘钥值到“key”框中。
&emsp;&emsp;7.然后点击*Add SSH key*
&emsp;&emsp;8.确认操作,然后输入你的GitHub密码。
##### 测试SSH秘钥是否添加成功
+ 小贴士:当你测试你的连接，你需要使用你的密码，这是你先前创建的SSH密钥密码来验证这个动作。

&emsp;&emsp;1.在任意位置右键,打开Git Bash
&emsp;&emsp;2.输入以下命令`ssh -T git@github.com`
```
$ ssh -T git@github.com
# Attempts to ssh to GitHub
```
&emsp;&emsp;你可能会看到这些警告之一：
```
The authenticity of host 'github.com (192.30.252.1)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?
```
```
The authenticity of host 'github.com (192.30.252.1)' can't be established.
RSA key fingerprint is nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)?
```
+ 小贴士:上面的例子列出了GitHub的IP地址为192.30.252.1 。当侦测GitHub上，你可能会看到一个IP地址范围。

&emsp;&emsp;3.验证你看到消息中的指纹相匹配的以下信息，然后输入 `yes`
```
Hi username! You've successfully authenticated, but GitHub does not
provide shell access.
```
&emsp;&emsp;4.如果你从HTTPS切换到SSH，你需要更新远程存储库的URL。
&emsp;&emsp;ok,如果以上都完成了,那我们GitHub端的工作已经完成。
# Hexo使用指南
## 利用命令行安装Hexo（需要注意）
&emsp;&emsp;Node.js安装完成后,在电脑任意位置,右键,选择 *GitBash* ,或是使用系统命令行工具（个人建议使用系统命令行工具，因为可以看到进度条）执行npm命令。
&emsp;&emsp;由于国区网络环境原因请将自己的npm镜像源切换为淘宝镜像，海区用户可以忽视此步骤。
> 临时使用淘宝源

```
npm --registry https://registry.npm.taobao.org install node-red-contrib-composer@latest
```
> 全局配置切换到淘宝源

```
npm config set registry https://registry.npm.taobao.org
```
> 检测是否切换到了淘宝源

```
npm info underscore
```
```
.......

gitHead: 'e4743ab712b8ab42ad4ccb48b155034d02394e4d',
  dist: 
   { shasum: '4f3fb53b106e6097fcf9cb4109f2a5e9bdfa5022',
     size: 34172,
     noattachment: false,
    //　有　registry.npm.taobao.org　等字样　　说明切换成功
     tarball: 'http://registry.npm.taobao.org/underscore/download/underscore-1.8.3.tgz' },
  directories: {},
  publish_time: 1427988774520 }
```
&emsp;&emsp;ok，国区用户完成以上操作以后我们可以开始安装Hexo了
> 运行全局安装命令（这一步可以在任意文件夹内进行）

```
npm install -g hexo
```
>检测是否安装成功，在终端输入 -v，成功则显示Hexo信息

```
hexo -v
```
## 搭建博客
### 初始化
&emsp;&emsp;所有必须工具都安装完成后，创建一个文件夹，如：Blog，用于存放Hexo配置文件。然后进入文件夹Blog,执行 init 命令初始化 Hexo。
```
hexo init
```
+ <font style="color:#DC143C;">警告：该目录就是我们的博客根目录日后所有指令操作均在本文件夹内进行，初始化操作必须保证根目录文件夹为空文件夹，否则无法完成初始化。</font>

&emsp;&emsp;至此，全部安装工作都已完成。文件夹 Blog 就是你的博客根目录，所有的操作都在里面进行。
### 生成静态页面
```
hexo g
```
### 启动本地服务，进行文章预览调试
```
hexo server
```
&emsp;&emsp;浏览器输入 http://localhost:4000 就可以看见预览页面啦。
### 配置Github
&emsp;&emsp;现在我们需要编辑 Blog 文件夹下的 _config.yml 文件，与自己 Github 账号的 Repository 仓库建立关联
&emsp;&emsp;编辑_config.yml 文件有两种方式（下面都会说，诸位可以看自己适合哪种）。
#### 配置Github方法一（使用命令行工具配置）
```
vim _config.yml
```
&emsp;&emsp;基本配置：修改这几个必须设置的键值对，记得保存，注意配置的键值对之间一定要有**空格**。[更多设置请参考官方API](https://hexo.io/zh-cn/docs/configuration.html)
```
title: xxxx    //网站标题
author: xxx   //作者名字
language: zh-Hans    //网站使用的语言 中文	
deploy:
   type: git  
   repo: https://github.com/username/username.github.io.git
   branch: master
```
&emsp;&emsp;键repo： 对应的值就是你 Github 创建的仓库所对应的URL链接，复制粘贴一下就OK啦
#### 配置GitHub方法二（使用编辑工具配置）
+ <font style="color:#DC143C;font-size:20px;">警告</font>
+ <font style="color:#DC143C;">不要用记事本进行编辑！</font>
+ <font style="color:#DC143C;">不要用记事本进行编辑！</font>
+ <font style="color:#DC143C;">不要用记事本进行编辑！</font>

&emsp;&emsp;请使用*Sublime Text*或者*Visual Studio Code*打开_config.yml 文件进行修改。修改部分和上面的方法一直。
&emsp;&emsp;[Sublime Text官网](http://www.sublimetext.com/)
&emsp;&emsp;[Visual Studio Code官网](https://code.visualstudio.com/)
### 自动部署发布
&emsp;&emsp;配置文件修改完成以后，执行命令，完成自动部署：
```
npm install hexo-deployer-git --save
```
### 新建文章
&emsp;&emsp;如果你此时需要写一篇新的文章，比如标题是：Hello world，执行下面命令就OK啦。在 Blog/source/_posts 文件夹下面就会生成一个 Hello world.md 文件，在电脑上使用*Sublime Text*或者*Visual Studio Code*打开文件随意书写。[Markdown——入门指南](http://www.jianshu.com/p/1e402922ee32)
+ <font style="color:#FF8C00;">提示：文章编辑遵循Markdown语法，使用*Sublime Text*或者*Visual Studio Code*编辑文章时请记得随时保存，快捷键是*Ctrl+S*</font>

```
hexo new "Hello world"
```
### 发布
&emsp;&emsp;启动本地服务，测试没问题后，我们就可以生成静态网页文件发布至我们的 Github pages 上。
```
hexo clean && hexo g && hexo d
```
&emsp;&emsp;如果这是你第一次执行，终端会让你输入Github 的邮箱和密码，正确输入后，稍等片刻，就会把你的博客上传至Github上，个人博客就这样完成啦。以后，每次把博客写完后，执行一下这个命令就可以直接发布了。
# 多终端维护Hexo（很重要）
## 上传操作
&emsp;&emsp;进入 Hexo 所在的文件夹打开 git bash 窗口(或者用系统命令提示符工具跳转到 Hexo 所在的文件夹)
&emsp;&emsp;进行初始化repo
```
git init
```
&emsp;&emsp;完成之后，添加 修改的文件，本来 Hexo 就自带了 .gitignore 文件
&emsp;&emsp;需要忽略的文件 都已经默认配置好了
&emsp;&emsp;接下来进行第一次 提交。
&emsp;&emsp;当然了，git流程还是要走正确的
&emsp;&emsp;首先应该是 add
```
git add .
```
&emsp;&emsp;我们将所有文件进行添加 . 就是这个意思
&emsp;&emsp;然后commit
```
git commit -m "update"
```
&emsp;&emsp;上面指令里""内的内容为注释可随意填写但**不能为空白**
&emsp;&emsp;提交成功之后
&emsp;&emsp;接下来就是 push 到github了
&emsp;&emsp;我们先把本地这个文件夹 映射到 远程 repo 上
```
git remote add origin https://github.com/your-name/your-name.github.io.git
```
&emsp;&emsp;接下来就是把刚刚的提交 push 上去
&emsp;&emsp;关键点到了
&emsp;&emsp;Hexo 部署的 page 是在 master 上的
&emsp;&emsp;如果我们push 到 master 分支上的话
&emsp;&emsp;虽然程序还能运行
&emsp;&emsp;但是 目录结构就会变得很乱了

&emsp;&emsp;我们的做法是：把 这些源文件（包括文章和配置）
&emsp;&emsp;push到另外一个 分支中
&emsp;&emsp;操作方法如下：
&emsp;&emsp;1.先新建一个分支 名字叫 hexo
```
git branch hexo
```
&emsp;&emsp;然后把刚刚的东西全部 push 到 hexo 分支上
```
git push -u origin hexo
```
&emsp;&emsp;输入账号密码后上传
&emsp;&emsp;一会就成功了

&emsp;&emsp;然后去 GitHub 上的 repo 看一下
&emsp;&emsp;有两个分支
&emsp;&emsp;一个是 master,里面的内容是 Hexo 生成了 page 页面
&emsp;&emsp;一个是 hexo, 里面的内容是 我们的文章还有 hexo 的源文件

&emsp;&emsp;这样的话，不管在什么地方 都可以进行最新文章的获取和继续操作了

&emsp;&emsp;当然了，修改了文章或者其他东西，在 deploy 前 还是 先 commit 和push 一下哦
&emsp;&emsp;记得：所有的本地操作 都在 hexo 分支里面。
## 下载操作
&emsp;&emsp;现在我们切换视觉到 一台新的电脑上，
&emsp;&emsp;在这台电脑上没有 Node.js,没有 Hexo，没有 Git
&emsp;&emsp;1.先安装必要的程序 node.js 和 git，过程不再赘述
&emsp;&emsp;2.把 原来的文章下载下来
&emsp;&emsp;3.配置 git ssh key，你才拥有从这台电脑发布文章的权利（请不要在公共电脑操作）
&emsp;&emsp;4.然后就是走 Hexo 的发布流程，也就是上面的 上传操作了
&emsp;&emsp;具体操作如下：
### 把文章下载下来
&emsp;&emsp;找到自己喜欢的 路径，新建一个文件夹，命名随意，自己认识就好
&emsp;&emsp;打开 git bash或者命令提示符跳转到这个文件夹
```
git clone xxxxxxxxx.xx (输入你的 github page 的 repo 地址)
```
&emsp;&emsp;等待下载完成之后，默认的分支是 master，还记得吗？
&emsp;&emsp;master分支是 Hexo 编译之后的 网站程序，我们的文章在 hexo 分支内
```
git checkout hexo
```
&emsp;&emsp;这个时候文件夹内的 内容已经是 我们的文章了
### 配置 git ssh key
&emsp;&emsp;这里的操作和上面的环境部署部分SSH keys配置部分的操作相同
### 然后就是配置 Hexo 程序了
&emsp;&emsp;安装 hexo（记得切换镜像源，操作和上面相同）
```
npm install hexo-cli -g
npm install hexo --save
```
&emsp;&emsp;检查 hexo 是否安装成功
```
hexo -v
```
+ <font style="color:#DC143C;font-size:20px;">警告</font>
+ <font style="color:#DC143C;">这个时候就不做 初始化了</font>
+ <font style="color:#DC143C;">这个时候就不做 初始化了</font>
+ <font style="color:#DC143C;">这个时候就不做 初始化了</font>

&emsp;&emsp;自动安装需要的组件
```
npm install
```
&emsp;&emsp;安装 git 部署的 插件
```
npm install hexo-deployer-git --save
```
&emsp;&emsp;操作完成
&emsp;&emsp;现在这台新电脑 就跟原来那台电脑一样操作就可以发布文章了。
## 多终端维护操作
所有操作均在根目录下执行
&emsp;&emsp;1.更新服务器文件到本地，保证本地文件和服务器端为同一版本
```
git pull
```
&emsp;&emsp;2.编辑完博文以后开始进行备份工作，首先提交我们的博文（博文均在source文件夹下）
```
git add source
```
&emsp;&emsp;3.提交到服务器
```
git commit -m "update"
```
4&emsp;&emsp;.将文件推送到我们之前创建的hexo分支
```
git push origin hexo
```
&emsp;&emsp;这样我们就完成了备份工作。

&emsp;&emsp;*Open source spirit, immortal!*