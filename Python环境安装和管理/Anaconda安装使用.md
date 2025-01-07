# Anaconda和Jupyter（笔记向）

面向深度学习环境用

先休息，再学习[《最愛》周慧敏 1993 - YouTube](https://www.youtube.com/watch?v=EFtYGQmP00Q)

[![周慧敏](https://res.cloudinary.com/marcomontalbano/image/upload/v1700201475/video_to_markdown/images/youtube--EFtYGQmP00Q-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=EFtYGQmP00Q "周慧敏")

[toc]





## 一、Anaconda软件安装

1. 下载

   下载安装包[Free Download | Anaconda](https://www.anaconda.com/download/) ，或者复制下面的网址到浏览器地址栏搜索下载

   > https://www.anaconda.com/download/

   后面会使用虚拟环境，所以conda的base环境中python的版本并不重要，创建虚拟环境时会设置新环境中的python解释器的版本。

2. 安装

   * 安装时 just me 和 all users，选择 **just me** 
   * 可以安装到D盘，D:\\ProgramFiles\\Anaconda
   * 注意：最后不建议在Advanced Options选择的选项【不建议在这里添加环境变量】

3. 配置anaconda的环境变量

   右键此电脑→属性→高级系统设置→(系统属性\\高级)环境变量→系统变量中选中*Path* →编辑→新建→添加下面的三个路径→确定

   > D:\ProgramFiles\Anaconda
   >
   > D:\ProgramFiles\Anaconda\Scripts
   >
   > D:\ProgramFiles\Anaconda\Library\bin

   若此前用户为其他多余Python解释器添加过环境变量，请删除，否则anaconda的环境变量会被挤掉。

4. 更改默认启动环境

   找到安装位置下的`Anaconda\Scripts` 中的`activate.bat` 

   修改其中的为自己的环境名。

   > @CALL "%~dp0..\condabin\conda.bat" activate %*

   修改为：（其中normal为自己的环境名）

   > @CALL "%~dp0..\condabin\conda.bat" activate normal



---

## 二、Jupyter Notebook

### 更改工作路径

1. 选择一个目录新建文件夹作为工作路径，比如我这里设置为

   > D:\myProject\Jupyter

2. 打开anaconda附带安装的Prompt，输入下面的命令

   ~~~cmd
   jupyter notebook --generate-config
   ~~~

3. 打开`C:\User\用户名\.jupyter` （用户名替换为自己的）文件夹，用记事本打开jupyter_notebook_config.py文件

4. 修改其中的

   ~~~cmd
   # c.NotebookApp.notebook_dir = ''
   ~~~

   为下面的内容，并去掉前面的#号

   ~~~cmd
   c.NotebookApp.notebook_dir = 'D:\myProject\Jupyter'
   ~~~

5. 找到Jupyter Notebook的快捷方式

   右键→属性→（快捷方式）目标→删除jupyter-notebook-script.py后面的内容(即 "%USERPROFILE%/")包括空格→应用→确定

### 切换内核

Jupyter的默认内核为Python 3(ipykernel)，我们把kernel切换为自己的虚拟环境，在自己创建的虚拟环境中运行。

列出Jjupyter的内核列表

~~~cmd
jupyter kernelspec list
~~~

安装ipykernel

~~~cmd
conda install ipykernel
~~~

将虚拟环境`envName` 导入jupyter的kernel中

~~~cmd
python -m ipykernel install --user --name=envName
~~~

删除虚拟环境中名字为`envName` 的kernel内核

~~~cmd
jupyter kernelspec remove envName
~~~

出现下面内容为成功

> Installed kernelspec normal in C:\Users\你的用户名\AppData\Roaming\jupyter\kernels\normal



### 保存为Markdown

安装基本依赖

```cmd
conda install pandoc
```

安装`nbconvert` 库

```cmd
conda install nbconvert
```

使用方法，在命令行里输入

```cmd
jupyter nbconvert --to markdown notebook.ipynb
```



或者直接在Jupyter中File → Download as → markdown

> 实际测试，直接全选复制粘贴就行





---

## 三、Conda命令



### 环境相关

#### 查看conda版本

```cmd
conda -V
```



#### 查看虚拟环境

有三种方法，我最常用的是第一种

* **第一种** 

  ~~~cmd
  conda env list
  ~~~

* 第二种

  ~~~cmd
  conda info -e
  ~~~

* 第三种

  ```cmd
  conda info --envs
  ```



#### 创建虚拟环境

创建一个python3.9的空环境，其中的`envName` 为要创建的虚拟环境的名字

~~~cmd
conda create -n envName python=3.9
~~~

克隆一个虚拟环境（从一个旧的环境创建新环境）

~~~cmd
conda create -n newName --clone oldName
~~~



#### 删除虚拟环境

其中`--all`是指删除整个环境

```cmd
conda remove -n envName --all
```



#### 激活环境

```cmd
conda activate envName
```

#### 关闭环境

有两种办法

* 第一种，此时的缺省值为当前环境

  ```cmd
  conda deactivate
  ```

* 第二种，此时缺省值为`base`环境

  ```cmd
  conda activate
  ```





#### 导入/导出环境(requirements.txt)

##### 1. 使用Conda

**导出**，*导出的文件所在目录为：控制台所在目录* ，如果需要指定目录可以`D:\requirements.txt` 

~~~cmd
conda list -e > requirements.txt
~~~

**导入**`requirements.txt` 中的库（*使用这种执行方式，遇到安装不上就整体停止，不继续安装接下来的包* ）

~~~cmd
conda install --yes --file requirements.txt
~~~

上述命令如果`requirements.txt` 中的包不可用，则会抛出“无包错误”，使用下面的方法可以解决上述问题

~~~cmd
while read requirement; do conda install --yes $requirement; done < requirements.txt
~~~

或者执行这个解决上面出现的不执行后续包的问题

~~~cmd
FOR /F "delims=~" %f in (requirements.txt) DO conda install --yes "%f" 
~~~

如果想要在conda命令无效时使用pip命令来代替，则可以使用下面的命令

~~~cmd
while read requirement; do conda install --yes $requirement || pip install $requirement; done < requirements.txt
~~~

##### 2. 使用Pip

pip批量**导出**环境中包含的所有包，包括没有用到的包，*导出的文件所在目录为：控制台所在目录* 

~~~cmd
pip freeze > requirement.txt
~~~

如果需要导出到*指定位置* 

~~~cmd
pip freeze > D:\...\requirement.txt
~~~

**导入**

~~~cmd
pip install -r requirement.txt
~~~

或者从国内源导入（临时换源）

~~~cmd
pip install -i 国内源 -r requirement.txt
~~~

> 一些国内源
>
> 清华源https://pypi.tuna.tsinghua.edu.cn/simple
>
> 中科大https://mirrors.bfsu.edu.cn/pypi/web/simple/
>
> 阿里云http://mirrors.aliyun.com/pypi/simple/
>
> 豆瓣源http://pypi.douban.com/simple/
>
> 华科源http://pypi.hustunique.com/



#### 导出/导入环境(yml)

##### 导出为yml文件

先激活需要导出的环境（如envName），然后输入以下内容

```cmd
conda env export > envName.yml
```

或者在导出的时候添加环境名字`-n envName` 

```cmd
conda env export -n envName > envName.yml
```

##### 导入yml文件

用yml文件创建环境

```cmd
conda env create -f envName.yml
```

用yml文件更新环境

```cmd
conda env update -f envName.yml
```





### 包相关

#### 更改虚拟环境中Python解释器的版本

注意：不管是升级版本还是降版本，都是用下面的命令，==修改版本后，原来的pip安装的包会被删掉，无法使用==

查看当前虚拟环境的python版本

~~~cmd
python -V
~~~

更改python版本为3.9

~~~cmd
conda install python=3.9
~~~

如果遇到问题可以先卸载python，然后再安装

~~~cmd
conda uninstall python
~~~







### 源相关

#### 添加镜像源

```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
```

#### 查看已加载的镜像

```bash
conda config --show channels
```

#### 移除已加载的镜像

```bash
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
```





---

#### 一些国内源

> 清华源https://pypi.tuna.tsinghua.edu.cn/simple
>
> 中科大https://mirrors.bfsu.edu.cn/pypi/web/simple/
>
> 阿里云http://mirrors.aliyun.com/pypi/simple/
>
> 豆瓣源http://pypi.douban.com/simple/
>
> 华科源http://pypi.hustunique.com/
