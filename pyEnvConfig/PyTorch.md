## 安装PyTorch

pytorch虽然是一个库，但安装时的核心组件叫做torch，另外还有两个额外的小组件叫做torchvision和torchaudio。

### GPU版本

由于PyTorch库的下载组件内部含有cudatoolkit，它是CUDA的子集，里面的东西足够PyTorch使用，因此不用单独安装CUDA和CUDNN，也不用考虑PyTorch内置cuda与计算机显卡CUDA版本之间的关系。

查看本机显卡CUDA版本，在CMD中输入下面的内容，可以在右上角看到CUDA版本号

~~~cmd
nvidia-smi
~~~

可以在这个网站[Previous PyTorch Versions | PyTorch](https://pytorch.org/get-started/previous-versions/) 下载安装需要的版本

> https://pytorch.org/get-started/previous-versions/

网站里有对应版本的命令。

使用下面的命令查看conda可以安装的torch版本

```cmd
conda search pytorch
```

推荐使用pip指令安装指定版本的pytorch



### CPU版本

CPU版本的安装和GPU版本安装步骤是一样的，可在网站中选择CPU版本



**检查**：如果`torch.cuda.is_available()` 返回`False` 那么使用的是CPU版本的torch