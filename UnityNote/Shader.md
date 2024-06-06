# Shader学习笔记



[toc]

## Chapter01 - 认识Shader

### 一个shader的基本流程：

shader→materials→mesh renderer→object

### Shader代码解析

1. **第一行**：文件路径，并不是真正在这个文件目录下，而是在材质球选择Shader的时候的路径

  ```
  Shader "ShaderLearn/Chapter01/Custom/StandardDiffuse1"
  ```

2. **Shader属性**，每行最后无分号，Shader属性的变量名都是下划线开头

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

3. **声明变量**，因为Color类型是一个RGBA四维的变量，所以用float4，

  ```
  float4 _AmbientColor
  float _MySliderValue
  ```

4. **表面输入结构体**，不允许为空（必须有成员存在），当把`_MainTex`纹理属性删除之后，下面表面输入结构体不能删（只是弃用）。

  ```cg
  struct Input
  {
      float2 uv_MainTex;
  };
  ```

5. 代码**基本结构**

  ```
  Shader "....."
  {
  	Properties
  	{
  		...
  	}
  	SubShader
  	{
  		Tags { "RenderType = Opaque" }
  		LOD 200
  		
  		CGPROGRAM
  		...
  		struct Input
  		{
  			...;
  		};
  		...;
  		void surf()
  		{
  			...;
  		}
  		ENDCG
  	}
  	FallBack "..."
  }
  ```

  

> 注：
>
> 1. CG语言编译错误会将unity中的对象渲染成纯白色（unity5.x版本为洋红色）
> 2. CG语言编译错误不会影响C#程序的运行





## Chapter02 - 表面着色器和纹理映射

### 漫反射着色代码

```C
// 目录
Shader "ShaderLearn/Chapter02/Custom/CustomDiffuse"
{
    Properties
    {
        // 无光照的基色
        _Color ("Color", Color) = (1,1,1,1)
    }
    SubShader
    {
        Tags { "RenderType"="Opaque" }  // 渲染类型=不透明
        LOD 200

        CGPROGRAM
        // Physically based Standard lighting model, and enable shadows on all light types
        #pragma surface surf Standard fullforwardshadows
        // #pragma：编译器指令，指定表面函数、光照模型等其他渲染设置
        // surface：关键字，告诉shader，表示当前表面处理函数为surf
        // surf
        // Standard：使用标准光照模型，可以创建自定义光照模型（写自己名字）
        // fullforwardshadows：完整的前向的阴影，使用了阴影的效果

        // Use shader model 3.0 target, to get nicer looking lighting
        #pragma target 3.0
        // shader模型使用3.0版本

        // 表面函数输入结构体
        struct Input
        {
            float2 uv_MainTex;
        };

        // 和属性值相对应的变量，只有创建了相对应的变量才可以使用属性的值
        fixed4 _Color;

        // Add instancing support for this shader. You need to check 'Enable Instancing' on materials that use the shader.
        // See https://docs.unity3d.com/Manual/GPUInstancing.html for more information about instancing.
        // #pragma instancing_options assumeuniformscaling
        UNITY_INSTANCING_BUFFER_START(Props)
            // put more per-instance properties here
        UNITY_INSTANCING_BUFFER_END(Props)

        // 表面处理函数
        void surf (Input IN, inout SurfaceOutputStandard o)
        {
            /*
                表面处理函数
                    输入：表面输入结构体
                    输出：标准的表面输出结构体
            */
            // Albedo comes from a texture tinted by color
            fixed4 c = _Color;
            o.Albedo = c.rgb;
        }
        ENDCG
    }
    FallBack "Diffuse"
}
```



### 压缩数组

1. **单值：**

2. **压缩数组：**

   shader中数组一般4维就够用了，可以用`x y z w`或者`r g b a`进行访问

   1. **类型写法**：`float3`，`int4`

      例如：`o.Albedo = _Color.a`，但是用了`rgba`就不能用`xyzw`了（禁止混合使用）。

   2. **特点：**

      - 混写swizzling
        - 赋值：`o.Albedo = _Color.rgb`
        - 调换`r b`顺序：`_Color.bgr`

      - 涂抹smearing
        - `o.Albedo = 0`    // o.Albedo = (0, 0, 0)

      - 遮蔽masking
        - `o.Albedo.rg = _Color.rg`

3. **压缩矩阵**

   1. 类型写法：`float4X4`：4*4矩阵，`float4X4 matrix`

   2. 元素索引：
      - 获取第一个元素：`float first = matrix._m00`
      - 获取最后一个元素：`float last = matrix._m33`
      - 获取对角线上元素（链式获取）：`float4 diagonal = matrix._m00_m11_m22_m33`
      - 获取第一行元素：`float4 firstRow = matrix[0]`、`float4 firstRow = matrix._m00_m01_m02_m03` 



### 给着色器添加纹理

 1. **给模型添加纹理的方法**

    新建shader - 新建材质 - 选择shader - 纹理拖入材质

2. **通过UV值滚动纹理**

   如果我们想让纹理在这个平面上滚动，可以修改UV坐标。例如，假设我们每帧将U坐标增加0.1，V坐标增加0.1：

   ```
   原始UV: (U, V)
   新UV: (U + 0.1, V + 0.1)
   ```

   ```
   void surf (Input IN, inout SurfaceOutputStandard o)
   {
       // 获取传入的UV坐标，IN.uv_MainTex表示每个片元顶点的UV坐标，在程序运行时不会被改变，永远保持最初的值不变。
       half2 scrolledUV = IN.uv_MainTex;
       // 计算X轴方向的滚动偏移量
       half xScrolledValue = _XScrollingSpeed * _Time;
       // 计算Y轴方向的滚动偏移量
       half yScrolledValue = _YScrollingSpeed * _Time;
       // 将滚动的偏移量应用到UV坐标上
       scrolledUV += half2 (xScrolledValue, yScrolledValue);
       // 根据滚动后的UV坐标采样纹理颜色
       half4 c = tex2D (_MainTex, scrolledUV) * _MainTint;
       // 将采样到的颜色的RGB值赋给表面的Albedo（反照率）
       o.Albedo = c.rgb;
       // 将采样到的颜色的Alpha值赋给表面的Alpha
       o.Alpha = c.a;
   }
   ```

   - **示例计算**

     假设初始 UV 坐标为 (0, 0)，`_XScrollingSpeed `和 `_YScrollingSpeed `都为 0.1：

     - **第1秒**：
       - `_Time.x` = 1
       - `xScrolledValue = 0.1 * 1 = 0.1`
       - `yScrolledValue = 0.1 * 1 = 0.1`
       - `scrolledUV = (0, 0) + (0.1, 0.1) = (0.1, 0.1)`
     - **第2秒**：
       - `_Time.x` = 2
       - `xScrolledValue = 0.1 * 2 = 0.2`
       - `yScrolledValue = 0.1 * 2 = 0.2`
       - `scrolledUV = (0, 0) + (0.2, 0.2) = (0.2, 0.2)`
     - **第3秒**：
       - `_Time.x` = 3
       - `xScrolledValue = 0.1 * 3 = 0.3`
       - `yScrolledValue = 0.1 * 3 = 0.3`
       - `scrolledUV = (0, 0) + (0.3, 0.3) = (0.3, 0.3)`

   - **Shader中的时间**

     |       名称        |   类型   | 说明 ( t = shader运行时间 \ 游戏开始时间 ) |
     | :---------------: | :------: | :----------------------------------------: |
     |      `_Time`      | `float4` |           `(t/20, t, t*2, t*3)`            |
     |    `_SinTime`     | `float4` |            `(t/8, t/4, t/2, t)`            |
     |    `_CosTime`     | `float4` |            `(t/8, t/4, t/2, t)`            |
     | `unity_DeltaTime` | `float4` |     `(dt, 1/dt, smoothDt, 1/smoothDt)`     |

3. **UV 坐标的表示**

   - UV坐标通常以二维向量的形式表示，记作 (U, V)。例如：

     - (0, 0) 表示纹理的左下角。

     - (1, 0) 表示纹理的右下角。

     - (0, 1) 表示纹理的左上角。

     - (1, 1) 表示纹理的右上角。

     中间的点也可以用相应的值表示：

     - (0.5, 0.5) 表示纹理的中心。

   - **举例：**

     ```
     (0,1)        (1,1)
       +------------+
       |            |
       |            |
       |            |
       |            |
       +------------+
     (0,0)        (1,0)
     ```











