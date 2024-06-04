# Shader学习笔记

[toc]

## Chapter01-认识Shader

### 一个shader的基本流程：

shader→materials→mesh renderer→object

### Shader代码解析

* 第一行：文件路径，并不是真正在这个文件目录下，而是在材质球选择Shader的时候的路径

  ```
  Shader "ShaderLearn/Chapter01/Custom/StandardDiffuse1"
  ```

* Shader属性，每行最后无分号，Shader属性的变量名都是下划线开头

  举例：

  * _Color：Shader属性**变量名**，在代码中使用，以下划线开头
  * "Color"：显示在使用此Shader的材质球的Inspector中的名字
  * Color：类型名，除了此类型外还有Range, Color, 2D, Rect, Cube, Float, Vector
    * Color，Vector	→	float4，half4（半浮点型），fixed4（）
    * Range，Float	→	float，half，fixed
    * 2D	→	sampler2D
    * 3D	→	sampler3D
    * Cube	→	samplerCube
      * float【32位】
      * half【16位】
      * fixed【11位】，数值范围[-2,+2]
  * Range(start, end)：滑动条类型

  ```
  Properties  // Shader属性
  {
      _Color ("Color", Color) = (1,1,1,1)
      _Glossiness ("Smoothness", Range(0,1)) = 0.5
      _Metallic ("Metallic", Range(0,1)) = 0.0
      _AmbientColor ("AmbientColor", Color) = (1,1,1,1)
      _MySliderValue ("This is a slider", Range(0,10)) = 2.5
      // Range, Color, 2D, Rect, Cube, Float, Vector
  }
  ```

* 声明变量，因为Color类型是一个RGBA四维的变量，所以用float4，

  ```
  float4 _AmbientColor
  float _MySliderValue
  ```

  

> 注：
>
> 1. CG语言编译错误会将unity中的对象渲染成纯白色（unity5为洋红色）
> 2. CG语言编译错误不会影响C#程序的运行





## Chapter02 

## 表面着色器和纹理映射

