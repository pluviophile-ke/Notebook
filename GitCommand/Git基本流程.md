# 使用Git的基本流程

练习使用git bash

先放松，再学习

[看完了繁花，必须唱下王菲的《执迷不悔》哔哩哔哩](https://www.bilibili.com/video/BV1Qi4y1i7zk/?vd_source=a26806a76d4618342a3d74d75fe95c73)

---



[toc]

## 1. 基本流程指令

> git的三个区域：
>
> 1. 工作区(unstaged/untracked)
>    (`git add`)
> 2. 暂存区(staged)
>    (`git commit`)
> 3. 仓库

### 1.1 初始化仓库

#### 1.1.1 初始化仓库

在想要新建仓库的位置右键-`Open Git Bash here`

```bash
git init
```

初始化后，目录下出现`.git`文件

#### 1.1.2 设置忽略文件

可以使用bash新建一个文件，也可以用其他方法新建

```bash
touch .gitignore
```

在文件中写入需要忽略的文件名

```bash
//使用通配符忽略特定后缀的文件
*.txt
```



### 1.2 查看仓库状态

```bash
git status
```



### 1.3 工作区到暂存区

```bash
git add [fileName]
```

将所有未暂存的文件移动到暂存区，使用通配符`.`代表所有文件

```bash
git add .
```



### 1.4 暂存区到仓库

使用一条指令将文件提交
```bash
git commit -m "message"
```

使用下面指定提交时会打开编辑页面，在编辑页面中有自动生成的提交描述，修改后保存退出

```bash
git commit
```



### 1.5 查看提交日志

#### 1.5.1 基本命令形式如下

```bash
git log [option]
```

* options
  * --all 显示所有分支
  * --pretty=oneline 将提交信息显示为一行
  * --abbrev-commit 使得输出的commit id更简短
  * --graph 以图的形式显示

#### 1.5.2 *无敌查看log指令

在正常情况下用下面这条指令

```bash
git log --pretty=oneline --abbrev-commit --all --graph
```

在低版本中，上面指令可能出现问题，需要在后面加上`--decorate`

```bash
git log --pretty=oneline --abbrev-commit --all --graph --decorate
```



### 1.6 版本回退

作用是版本切换

命令形式

```bash
git reset --hard commitID
```

commitID可以使用`git log`查看，但是如果记录被删除了，可以使用`git reflog`







## 2. 分支

### 2.1 分支基本指令

#### 2.1.1 查看本地分支

```bash
git branch
```

#### 2.1.2 创建本地分支

```bash
git branch [分支名]
```

#### 2.1.3 *切换分支

* 切换到一个已存在的分支

  ```bash
  git checkout [分支名]
  ```

* 切换到不存在的分支，即新建分支并切换到此分支

  ```bash
  git checkout -b [分支名]
  ```

#### 2.1.4 合并分支

切换到一个分支，然后使用下面指令将另一个分支合并到此分支

```bash
git merge [分支名]
```

#### 2.1.5 删除分支

**不能删除当前分支，只能删除其他分支**

* 删除分支时，需要做各种检查

  ```bash
  git branch -d [分支名]
  ```

* 强制删除，不做任何检查

  ```bash
  git branch -D [分支名]
  ```

#### 2.1.6 解决冲突

当两个分支上对文件的修改可能存在冲突，例如同时修改同一个文件的同一行，这时就需要手动解决冲突。处理冲突的步骤如下

1. 处理文件中冲突的地方
2. 将解决完冲突的文件加入暂存区
3. 提交到仓库



## 3. 提交到远端

使用fork：

在远程新建仓库，复制远端的地址，在fork中push的时候粘贴，即可实现到远端的推送