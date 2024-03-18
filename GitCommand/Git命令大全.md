先看个视频放松下吧

[《南屏晚钟》_哔哩哔哩__bllibili_](https://www.bilibili.com/video/BV1Gs4y1k7mx)



[toc]



# 安装和配置

## 1.下载安装

### 下载

使用下面的网址下载

[Git - 安装 Git (git-scm.com)](https://git-scm.com/book/zh/v2/起步-安装-Git)

>  <https://git-scm.com/book/zh/v2/起步-安装-Git>

### 安装

可以默认安装



## 2.初始配置

### 设置姓名和邮箱地址

```bash
git config --global user.name "your name"
git config --global user.email "your_email@example.com"
```

这个命令会在`/c/Users/用户名/.gitconfig`中保存

```bash
[user]
  name = your name
  email = your_email@example.com
```

> * global的作用域为当前计算机的当前登录用户的所有git仓库，配置文件位于`/c/Users/用户名/.gitconfig` 
>
> * local的作用域为当前仓库，配置文件位于`.git/config`
> * system的作用域为当前计算机下的所有用户，配置文件位于`git安装路径\etc\gitconfig` 
>
> **注意：在GitHub上公开仓库时，这里的姓名和邮箱地址也会随着提交日志一同被公开，所以不要使用不便公开的信息** 



### 设置SSH Key

使用下面的代码生成ssh key

```bash
ssh-keygen -t rsa
```

GitHub上连接已有仓库时的认证是通过使用了SSH的公开密钥认证方式进行的。

在`C:\Users\用户名\.ssh`目录下有两个文件`id_rsa`和`id_rsa.pub`

其中"id_rsa.pub"为公钥，要添加到GitHub中。

可以通过下面的方法查看公钥内容

> ```bash
>cat ~/.ssh/id_rsa.pub
> ```

这里的公钥`id_rsa.pub`中的内容要粘贴到GitHub或者gitee中，私钥`id_rsa`在自己的电脑中保存。

如果需要多台电脑push仓库到远端，则在每一台电脑上生成一个ssh key，然后将每台电脑生成的公钥粘贴到GitHub或者gitee中。





## 3.其他配置

### 配置文本编辑器

```bash
git config --global core.editor vim
```

### 差异分析工具

```bash
git config --global merge.tool vimdiff
```

> 在解决合并冲突时，使用vimdiff差异分析工具。
>
> Git可以理解kdiff3，tkdiff，meld，xxdiff，emerge，vimdiff，gvimdiff，ecmerge和opendiff等合并工具的输出信息。



## 4.信息查看

### 4.1查看配置信息

#### 1)查看版本

```bash
git --version
```

#### 2)查看所有git配置

```bash
git config --list --show-origin
```

#### 3)查看单个配置

```bash
git config user.name
git config user.email
```

#### 4)配置文件的内容

* **使用vim** 

```bash
vim ~/.gitconfig
```

> 查看当前用户的配置，即global的配置，可编辑

* **使用git** 

```bash
# 查看系统config
git config --system --list
# 查看当前用户配置
git config --global --list
# 查看当前仓库配置
git config --local --list
```





### 4.2查看仓库信息

#### 1)查看仓库状态

```bash
git status
```

> **如果文件名的中文部分为数字或者乱码，可以使用下面的方法** 
>
> ```bash
> git config --global core.quotepath false
> git config --global gui.encoding utf-8
> git config --global i18n.commit.encoding utf-8
> git config --global i18n.logoutputencoding utf-8
> export LESSCHARSET=utf-8
> ```
>
> 1. `git config --global core.quotepath false`：
>    * 这个命令将 Git 的 `core.quotepath` 设置为 `false`。
>    * `core.quotepath` 是一个 Git 配置选项，用于指定在输出中显示文件路径时是否进行 quoting（引用）。
>    * 将其设置为 `false` 可以确保 Git 在输出中以原始的非转义形式显示文件路径，包括包含空格或特殊字符的文件路径。
> 2. `git config --global gui.encoding utf-8`：
>    * 这个命令将 Git 的 `gui.encoding` 设置为 `utf-8`。
>    * `gui.encoding` 是一个 Git 配置选项，用于指定图形用户界面（GUI）工具使用的字符编码。
>    * 将其设置为 `utf-8` 可以确保 Git 在图形界面工具中使用 UTF-8 字符编码来正确处理和显示字符。
> 3. `git config --global i18n.commit.encoding utf-8`：
>    * 这个命令将 Git 的 `i18n.commit.encoding` 设置为 `utf-8`。
>    * `i18n.commit.encoding` 是一个 Git 配置选项，用于指定提交消息的字符编码。
>    * 将其设置为 `utf-8` 可以确保提交消息以 UTF-8 编码进行存储和显示。
> 4. `git config --global i18n.logoutputencoding utf-8`：
>    * 这个命令将 Git 的 `i18n.logoutputencoding` 设置为 `utf-8`。
>    * `i18n.logoutputencoding` 是一个 Git 配置选项，用于指定日志输出的字符编码。
>    * 将其设置为 `utf-8` 可以确保日志输出以 UTF-8 编码进行存储和显示。
> 5. `export LESSCHARSET=utf-8`：
>    * 这个命令设置环境变量 `LESSCHARSET` 的值为 `utf-8`。
>    * `LESSCHARSET` 是一个环境变量，用于指定 `less` 命令所使用的字符编码。
>    * 将其设置为 `utf-8` 可以确保在使用 `less` 命令浏览文本时，正确地显示 UTF-8 编码的字符。



#### 2)检查远程仓库的 URL

```bash
git remote -v
```

> 如果 URL 以 `https://` 开头，而不是 `git@github.com:`，则表示你正在使用 HTTPS URL。
>
> 你需要更新远程仓库的 URL 为 SSH URL：
>
> ```bash
> git remote set-url origin git@github.com:username/repo.git
> ```
>
> 将 `username/repo.git` 替换为你的 GitHub 用户名和仓库名称。







如何同时提交到GitHub与gitee









