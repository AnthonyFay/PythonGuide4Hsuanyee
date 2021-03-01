# Python Guide 01



## 实验1-1	初识Git

### step1	安装git

Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。

在Git官网下载**[64-bit Git for Windows Setup](https://github.com/git-for-windows/git/releases/download/v2.30.1.windows.1/Git-2.30.1-64-bit.exe)**并安装。

### step2	设置git

启动Git Bash，设置用户。

注意这个不是登录哦，是给你的电脑设置一个用户，等你上传的时候，告诉远程仓库是谁上传的而已。

```shell
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

使用GitBash/command/powershell，进入本地仓库的文件夹。

用`git init`将当前为文件夹初始化为git仓库

![image-20210301170428245](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210301170428245.png)

显示

> Initialized empty Git repository in your_path

则说明初始化成功。

常用的shell语句有：

```shell
cd path	
cd ..
mkdir foldername
ls
pwd
rm filename
re -rf foldername
```

### step3	创建一个仓库

登录[GitHub](https://github.com/)，点击Create repository，填写仓库信息（选择Public，否则狗羊羊看不见你提交的作业）。

![github.com_new](D:\ChromeDownload\github.com_new.png)

这样我们就成功创建了一个仓库。

![image-20210301165158909](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210301165158909.png)

### step4	建立连接

在GitHub上创建好仓库之后，我们要将本地文件夹和GitHub上的仓库关联起来。

#### 		step4-1	配置SSH

##### 				step4-1-1	检查电脑上是否有SSH Key

​		打开cmd，输入`~/.ssh`或者`~/.ssh ls`，如果电脑上有，则显示

> ​	bash: /c/Users/dell/.ssh: Is a directory

​		否则没有。

![image-20210301171204208](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210301171204208.png)

##### 				step4-1-2	创建SSH Key

​		如果电脑上没有SSH Key，则需要创建一个SSH Key。若有，则跳过这一步。

​		在Git Bash中输入`ssh-keygen -t rsa -C "youremail@email.com"`，然后就会显示这两行：

> ​	Generating public/private rsa key pair.
> ​	Enter file in which to save the key (/c/Users/16627/.ssh/id_rsa):

​		这是让你输入一个文件名，用于保存刚才生成的 SSH key 代码。为了避免麻烦，不用输入，直接回车。

​		这时候已经创建好.ssh这个文件夹了，会提示：

> ​	Created directory ‘/c/Users/16627/.ssh’.

​		紧接着又会问你：

> ​	Enter passphrase (empty for no passphrase):

​		让你输入密码，如果你设置了密码，那在你使用ssh传输文件的时候，你就要输入这个密码。为了避免麻烦，不用设置，直接回车。

> ​	Enter same passphrase again:

​		这就是让你再输入一次密码，就跟我们注册账号时候设置密码需要设置两次一样。上一步没设置密码，这里直接回车就可以了。

​		到这里你的秘钥就设置好了，你会收到这段代码提示：

> ​	Your identification has been saved in /c/Users/…/.ssh/id_rsa
> ​	Your public key has been saved in /c/Users/…/.ssh/id_rsa.pub

​		还会向你展示你的秘钥长啥样：

<img src="https://img-blog.csdnimg.cn/2020042517483573.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NjY3MTcw,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述" style="zoom:150%;" />

​		当你看到上面这段代码，那就说明你的 SSH Key已经创建成功，你可以再使用`~/.ssh`看一下，现在文件是真的存在了。

![image-20210301205314393](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210301205314393.png)

##### 		step4-1-3	将SSH Key添加到GitHub

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210301210042662.png" alt="image-20210301210042662" style="zoom: 67%;" />

​		将 **step4-1-2** 中的 **id_rsa.pub** 的内容粘贴到GitHub。

​		(注意在命令行界面内，复制粘贴分别为`Ctrl+Insert`和`Shift+Insert`，而`Ctrl+C`是强制中断程序的执行)

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210301210435570.png" alt="image-20210301210435570" style="zoom: 45%;" />

##### 		step4-1-4	测试一下该SSH key

​		在git Bash 中输入`ssh -T git@github.com`

> ​	注意是git@github.com，不是你的邮箱。

​		然后会提示你：

> ​	The authenticity of host ‘github.com (13.229.188.59)’ can’t be established.
> ​	RSA key fingerprint is SHA256:nThbg6kXUp…
> ​	Are you sure you want to continue connecting (yes/no/[fingerprint])?

​		输入`yes`，回车

​		接下来就会提示你输入密码，如果上边设置ssh的时候，你没设置密码会提示你：

> ​	Warning: Permanently added ‘github.com,192.30.255.112’ (RSA) to the list of known hosts.

​		忽略警告，如果你能看到如下提示，那你已经成功设置SSH密钥。

> ​	Hi “your username”! You’ve successfully authenticated, but GitHub does not provide shell access.

​		如果你看到：

> ​	access denied

​		则表示拒绝访问，说明你设置出错。

##### 		step4-1-5	连接仓库

​		在你的电脑上打开Git Bash，进入本地仓库的文件夹（hint: 利用上面用过的`cd`指令）。

​		输入`git remote add origin address`

​		`address`即为你复制的ssh地址：

​		<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210301211953727.png" alt="image-20210301211953727" style="zoom: 45%;" />

> ​	e.g. `git remote add origin git@github.com:AnthonyFay/PythonGuide4Hsuanyee.git`

​		添加之后没有任何提示，如果你想确定是否成功了，你可以再输一遍，这时候他会提示你刚才已经设置过了。

​		<img src="https://img-blog.csdnimg.cn/20200425224311204.png" alt="在这里插入图片描述" style="zoom: 150%;" />

### step5	文件上传

文件上传会用到以下的Git命令。

**git add** 将**修改的文件**添加暂存区。

```sh
git add filename	#将一个文件添加到暂存区，若有多个文件，以空格隔开

git add .	#提交新文件(new)和被修改(modified)文件

git add -A	#提交所有变化
```

**git commit** 命令将索引的当前内容与描述更改的用户和日志消息一起存储在新的提交中。

```shell
git commit -m “annotation”
```

**git push** 把文件推到远程仓库。

```shell
git push -u repository_name branch	#你只有一个master分支，仓库名称为origin，那么这条命令应为 git push origin master
```



还有一个` git push origin master -f` 强制推送，如果你某次推送失败，Git Bash报错，你懒得处理错误，你就可以用这个。但是有风险，因为报错90%是因为你本地仓库和远程仓库数据发生冲突，使用这个会直接用本地数据覆盖掉远程数据，可能损失数据哦。

现在你去网页版刷新一下，就可以看到你本地仓库的东西都在那里了。并且文件后边写着你在**commit**步骤中添加的注释。



## 实验1-2	学习Python的基本语法、数据结构

阅读[Python基础教程](https://www.liaoxuefeng.com/wiki/1016959663602400/1017032074151456)**第一个Python程序 - 输入和输出**至**函数 - 递归函数**，完成作业。



## 练习题

### 1. 判断BMI指数

​	BMI指数（即身体质量指数，英文为 Body Mass Index ，简称 BMI ），是反应体内脂肪总量的指标，
​	BMI 指数的计算方法为BMI=w/h^2，其中 **w** 为体重，单位是千克； **h** 为身高，单位是米。
​	计算BMI指数可粗略评价身体状况，如下：

- BMI<18.5 轻体重

- 18.5<=BMI<24 正常

- 24<=BMI<28 超重

- BMI>=28 肥胖

  现在请设计程序，提示用户分别输入自己的身高和体重，并给出BMI指数的建议。

### 2. 打印乘法表

​	请打印九九乘法表。  

### 3. 请编写一个函数，使用递归方法计算 n 的阶乘，并进行测试

### 4. 请编写程序，使用 math 库计算27的立方根

### 5. 找出假硬币

​	有装有15个硬币的袋子。15个硬币中有一个是伪造的，并且那个伪造的硬币比真的硬币要轻一些。
​	我们要找出这个伪造的硬币。我们有一台可用来比较两组硬币重量的仪器，利用这台仪器，可以知道两组硬币的重量是否相同。

​	请编写程序使用分治方法模拟上述过程，假设硬币的重量为列表[2,2,2,2,2,2,1,2,2,2,2,2,2,2,2]找出假币的序号（序号从0开始，假币的序号为6）  