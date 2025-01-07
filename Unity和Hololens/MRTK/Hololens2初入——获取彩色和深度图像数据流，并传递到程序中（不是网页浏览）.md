#### 文章目录 

 *  [Hololens2 初入——获取彩色和深度图像数据流，并传递到程序中（不是网页浏览）][Hololens2]
 *   *  [前言][Link 1]
     *  [基础环境][Link 2]
     *  [配置过程][Link 3]
     *   *  [下载github上的工程][github]
         *  [编译 HoloLens2-Unity-ResearchModeStreamer][HoloLens2-Unity-ResearchModeStreamer]
         *  [配置Unity项目][Unity]
     *  [配置package文件中的兼容性][package]
     *  [在VS中编译与部署][VS]
     *  [修改PC端接收文件][PC]
     *  [程序运行][Link 4]
     *  [实时性问题的解决和深度图数据问题的解决][Link 5]
     *  [发布到Hololens2 后 找不到.dll文件][Hololens2 _ _.dll]

## Hololens2 初入——获取彩色和深度图像数据流，并传递到程序中（不是网页浏览） 

### 前言 

HoloLen2 设备内集成了多种不同类型的传感器。软件上也提供了研究者模式，便于开发者们访问传感器的原始数据，进行科研开发。  
但是由于设备较新，其官方文档并没有过多的介绍这部分的内容.旧的Hololens1代码又不能直接用在新的Hololens2 上， 官方的github工程也较少，大都只停留在真机上可以获取数据而已。  
本文的配置将实现把设备上的图像数据通过wifi实时地传递到电脑端，方便用深度学习算法对图像进行处理。  
PS 这个工程是github上的， 目前仍然达不到实时传输的效果，延迟很高，尚未解决。但是可以在线获得图像数据便是。

### 基础环境 

1.  WIN10 专业版
2.  VS2019社区版
3.  Unity2019.3.4版本
4.  WIN SDK 最新
5.  HoloLens2处于研究者模式(见我另外一篇博客)
6.  [参考出处][Link 6]
7.  关掉两边的防火墙

### 配置过程 

#### 下载github上的工程 

[地址传送门][Link 6]

#### 编译 HoloLens2-Unity-ResearchModeStreamer 

1.  用VS打开该项目中插件工程  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/d23eea70dbac1078df70be4f563c9096.png)
2.  设置项目属性为release 和arm64  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/194bfaf891ea96082f92f7451581d3f8.png)
3.  生成解决方案  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/571ac7d316766a5cb55834057608c306.png)  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e82e60e1bd70063d3f6b192e5bdeb166.png)

#### 配置Unity项目 

1.  新建一个Unity的3D项目
2.  将项目切换到Universal windows patform
3.  新建如下路径"Assets/Plugins/"
4.  将前面编译好的文件拷贝到新建的文件夹下  
    文件位置![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a7ffff1afdb1e5582654806d819cc7c5.png)  
    拷贝过去后![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/0324b68a8eb8e172d7ae138cda0cbb71.png)
5.  新建一个StreamerHL2.cs（名称注意一致，或者自己在代码中对应修改类名称），复制下面代码到脚本里面（清空原本的代码）

```java
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System;
using System.Runtime.InteropServices;

public class StreamerHL2 : MonoBehaviour
{
            
   
     
     
    // Start is called before the first frame update
    // [DllImport("HL2RmStreamUnityPlugin", EntryPoint = "StartStreaming", CallingConvention = CallingConvention.StdCall)];
    //[DllImport("HL2RmStreamUnityPlugin", EntryPoint = "StartStreaming", CallingConvention = CallingConvention.StdCall)]
    //private static extern void StartDll(); 这是旧的函数入口点。更新为下面 2021-11-1
    [DllImport("HL2RmStreamUnityPlugin", EntryPoint = "Initialize", CallingConvention = CallingConvention.StdCall)]
	public static extern void InitializeDll(); // 更新的函数入口点  2021-11-1

    void Start()
    {
            
   
     
     

        //StartDll();
        InitializeDll();

    }

    // Update is called once per frame
    void Update()
    {
            
   
     
     
        
    }
}
```

6.将脚本随便挂在在一个对象上，我挂载的是主相机  
7.设置Unity 项目的兼容性，根据下图指引，勾选  
InternetClient, InternetClientServer, PrivateNetworkClientServer, WebCam, SpatialPerception. 5个位置![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/53605fcada1cd9fbea9a5d645e1aac5f.png)![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/27bf9d1cda76b2fad9a53565c304029a.png)![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/7555b4c5c3eaf1cfc2d056152f1c146b.png)  
8. 编译unity工程，注意架构选择的是ARM64.  
ps. 不需要在unity中运行工程，因为我们添加的是ARM64的动态链接库，在PC端运行的话会报加载不了的错误。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/20f6fc50ee3c0b3dd3bcc0e1317ec2ca.png)

### 配置package文件中的兼容性 

1.  用记事本的方式打开编译好的Unity工程文件夹中的“Package.appxmanifest”文件  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b9cacf61cd8bc66f18accf6fed6bdb69.png)
2.  将如下代码添加到 Package 中。注意前后各有一个空格

```java
xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities"
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/eb364a221e71d123d7fe529130857d4d.png)  
3.仍然在Package这一行中,找到"IgnorableNamespaces"的属性，添加“rescap”字段，如下图  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/9934adffdc2a291bf76ec6780bcb0d27.png)  
4. 在 Capabilityes添加如下代码

```java
<rescap:Capability Name="perceptionSensorsExperimental" />
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/53ffc35dbc1817d04ad34db081198a82.png)  
5.保存文件退出

### 在VS中编译与部署 

见我博客中的另外文章[Unity项目部署到HL2上][Unity_HL2]

### 修改PC端接收文件 

1.  打开前面下载好的github工程中的hololens2\_simpleclient.py文件，路径如下  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/5eb90a2bb423c503bc73f6fe874844ad.png)
2.  修改文件中的HOST参数。 （电脑和HoloLens 2同在一个局域网的时候,查看HL中的IP地址，这个HOST参数就是IP地址）  
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/2685cd3caef7a31ae7af956c041cad1b.png)

### 程序运行 

1.  将电脑和HL连接到同一个局域网中
2.  在HL中运行部署好的APP应用，然后运行hololens2\_simpleclient.py文件  
    3.![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/0691685550b644a04722188f6d1b30b2.png)

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/d155c4db8da88f46f122d75f75a1939b.png)

### 实时性问题的解决和深度图数据问题的解决 

见另外一个博文[Hololens2初入——解决HL真机到PC图像传输的实时性问题][Hololens2_HL_PC]

### 发布到Hololens2 后 找不到.dll文件 

把拷贝到unity中的dll设置一下参数  
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/73eab22cfbd2e9edab7253ecf56d5719.png)


[Hololens2]: #Hololens2__1
[Link 1]: #_2
[Link 2]: #_8
[Link 3]: #_19
[github]: #github_20
[HoloLens2-Unity-ResearchModeStreamer]: #_HoloLens2UnityResearchModeStreamer_22
[Unity]: #Unity_31
[package]: #package_81
[VS]: #VS_101
[PC]: #PC_103
[Link 4]: #_109
[Link 5]: #_115
[Hololens2 _ _.dll]: #Hololens2__dll_117
[Link 6]: https://github.com/cgsaxner/HoloLens2-Unity-ResearchModeStreamer
[Unity_HL2]: https://blog.csdn.net/scy261983626/article/details/111840585
[Hololens2_HL_PC]: https://blog.csdn.net/scy261983626/article/details/116381193