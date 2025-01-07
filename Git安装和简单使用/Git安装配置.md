# Git的安装和配置

先放松，再学习

[合唱《雨蝶》哔哩哔哩 bilibili](https://www.bilibili.com/video/BV1DM411x7si/?vd_source=a26806a76d4618342a3d74d75fe95c73)




## 1. 下载安装

* 下载地址：[https://git-scm.com/download/win](https://git-scm.com/download/win)

* Git官网：[https://git-scm.com/](https://git-scm.com/)

文件不大，默认安装就行，省去后面出现的很多莫名其妙的问题。

安装完成后在任意区域右键，可以看到菜单里出现`Open Git Bash here`，win11用户点击`显示更多选项`后查看。

点击`Open Git Bash here`，输入命令查看版本信息

```bash
git --version
```

输出类似下面内容即为安装成功

*git version 2.44.0.windows.1*

---



## 2. 初始化配置

在任意区域右键打开`Git Bash`

### 2.1 设置姓名和邮箱地址

```bash
git config --global user.name "your name"
git config --global user.email "your_email@example.com"
```

> 这里的信息会在commit代码的时候保留在git log中，如果仓库为public或者开源，请避免使用不方便公开的信息。

上面的配置命令会在`C:\Users\用户名\.gitconfig`中同步更改和保存

```
[user]
	name = your name
	email = your_email@example.com
```

这里配置的作用域为当前登录用户，下面给出不同作用域的配置方法和文件

|  关键字  |               作用域               |         配置文件位置         |
| :------: | :--------------------------------: | :--------------------------: |
| `global` | 当前计算机的**当前用户**的所有仓库 | `C:\Users\用户名\.gitconfig` |
| `local`  |            **当前仓库**            |    `仓库目录\.git\config`    |
| `system` |   当前计算机的**所有用户**的仓库   | `git安装路径\etc\gitconfig`  |

### 2.2 查看git所有配置

```bash
git config --list --show-origin
```

---





## 3. 配置ssh key

使用下面的代码生成ssh key

```bash
ssh-keygen -t rsa
```

push代码到远端的认证是通过使用SSH的公开密钥进行的。

在`C:\Users\用户名\.ssh`目录下有两个文件`id_rsa`和`id_rsa.pub`

其中`id_rsa.pub`为公钥，`id_rsa`为私钥。

可以通过下面的方法查看公钥内容

```bash
cat ~/.ssh/id_rsa.pub
```

**这里公钥`id_rsa.pub`中的内容要粘贴到GitHub或者gitee中，私钥`id_rsa`在自己的电脑中保存。**

如果需要多台电脑push仓库到远端，则在每一台电脑上生成一个ssh key，然后将每台电脑生成的公钥粘贴到GitHub或者gitee中。

---



## 4. 可视化Git工具

推荐使用的工具：

1. Fork 网址：[fork.dev](https://fork.dev)

2. GitHub Desktop
