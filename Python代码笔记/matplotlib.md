

## 单图

使用`plot()`

### 直线和点


```python
import matplotlib.pyplot as plt
import numpy as np
"""
	plot()函数用于在图表中绘制点（标记）。
	默认情况下，plot()函数从点到点绘制一条线。
	该函数采用参数来指定图中的点。
	参数1是一个包含x轴上的点的数组。
	参数2是一个包含y轴上的点的数组。
	如果我们需要绘制一条从（1，3）到（8，10）的线，我们必须将两个数组[1,8][3.10]传递给plot()函数
"""

# 1-1在图中从位置（0，0）到位置（6，250）画一条直线
xpoints = np.array([0, 6])
ypoints = np.array([0, 250])
plt.plot(xpoints, ypoints)
plt.show()

# 1-2在图中绘制两个点，一个在位置(1,3)，一个在位置(8,10)
xpoints = np.array([1, 8])
ypoints = np.array([3, 10])
plt.plot(xpoints, ypoints, 'o')
plt.show()

# 2-1折现段
xpoints = np.array([1, 2, 6, 8])
ypoints = np.array([3, 8, 1, 10])
plt.plot(xpoints, ypoints)
plt.show()

# 2-2多点
xpoints = np.array([1, 2, 6, 8])
ypoints = np.array([3, 8, 1, 10])
plt.plot(xpoints, ypoints, 'o')
plt.show()

# 3 默认X点
# 如果我们不指定X轴上的点，它们将获得默认值0,1,2,3...（取决于y的长度
ypoints = np.array([3, 8, 1, 10])
plt.plot(ypoints)
plt.show()
```



### 标记和线型

```python
import matplotlib.pyplot as plt
import numpy as np

# 格式化字符串fmt
# 可以使用快捷字符串符号参数来指定标记
# 使用此种语法编写 → marker|linestyle|color
# 如：绘制红色虚线，标记为实心圆
plt.plot(ypoints, 'o:r')

"""   1.marker   """
# 用实心圆标记
ypoints = np.array([3, 8, 1, 10])
plt.plot(ypoints, marker = 'o')
plt.show()
# 用星星标记每个点
plt.plot(ypoints, marker = '*')

# 标记的尺寸
# 使用markersize，或者简写ms
plt.plot(ypoints, marker='h', markersize=20)
plt.plot(ypoints, marker='h', ms=20)

# 标记的颜色
# 使用markerfacecolor，或者简写mfc设置标记里面的颜色
plt.plot(ypoints, marker='h', ms=20, mfc='r')
# 使用mec设置标记的边框的颜色
plt.plot(ypoints, marker='h', ms=20, mfc='r', mec='r')
# 也可以使用十六进制颜色值
plt.plot(ypoints, marker='h', ms=20, mfc='#4caf50', mec='r')
# 使用颜色名称
plt.plot(ypoints, marker='h', ms=20, mfc='hotpink', mec='r')


"""   2.linestyle   """
# 参数可用linestyle或者ls

# 线类型
# 使用点虚线
plt.plot(ypoints, ls=':')
# 使用点划线
plt.plot(ypoints, ls='-.')

# 线的宽度
# 使用参数linewidth或者简写lw
plt.plot(ypoints, linewidth='10')

# 多条线
# 第1种
ypoints1 = np.array([3, 8, 1, 10])
ypoints2 = np.array([1, 6, -1, 8])
plt.plot(ypoints1)
plt.plot(ypoints2)
plt.show()
# 第2种
xpoints1 = np.array([1, 2, 4, 8])
ypoints1 = np.array([3, 8, 1, 10])
xpoints2 = np.array([0, 3, 5, 8])
ypoints2 = np.array([1, 6, -1, 8])
plt.plot(xpoints1, ypoints1, xpoints2, ypoints2)
plt.show()

"""   3.color   """
# 参数可用color或者c
# 红色线条
plt.plot(ypoints, c='r')

# 使用十六进制数
plt.plot(ypoints, c='#4caf50')

# 使用颜色的名字
plt.plot(ypoints, c='hotpink')
```



#### 绘图标记

绘图过程如果我们想要给坐标自定义一些不一样的标记，就可以使用 `plot`() 方法的 `marker` 参数来定义。`plt.plot(ypoints, marker = '*')`

| 参数 | 图形 | 说明 | 参数 | 图形 | 说明 |
| :---: | :---: | :-----: | :----: | :-----: | :-----: |
| "."  | ![m00](https://www.runoob.com/images/m00.png) | 点           | "X"                | ![m24](https://www.runoob.com/images/m24.png) | 乘号 x (填充)                                |
| ","  | ![m01](https://www.runoob.com/images/m01.png) | 像素点       | "D"                | ![m19](https://www.runoob.com/images/m19.png) | 菱形                                         |
| "o"  | ![m02](https://www.runoob.com/images/m02.png) | 实心圆       | "d"                | ![m20](https://www.runoob.com/images/m20.png) | 瘦菱形                                       |
| "v"  | ![m03](https://www.runoob.com/images/m03.png) | 下三角       | "\|"               | ![m21](https://www.runoob.com/images/m21.png) | 竖线                                         |
| "^"  | ![m04](https://www.runoob.com/images/m04.png) | 上三角       | "_"                | ![m22](https://www.runoob.com/images/m22.png) | 横线                                         |
| "<"  | ![m05](https://www.runoob.com/images/m05.png) | 左三角       | 0 (TICKLEFT)       | ![m25](https://www.runoob.com/images/m25.png) | 左横线                                       |
| ">"  | ![m06](https://www.runoob.com/images/m06.png) | 右三角       | 1 (TICKRIGHT)      | ![m26](https://www.runoob.com/images/m26.png) | 右横线                                       |
| "1"  | ![m07](https://www.runoob.com/images/m07.png) | 下三叉       | 2 (TICKUP)         | ![m27](https://www.runoob.com/images/m27.png) | 上竖线                                       |
| "2"  | ![m08](https://www.runoob.com/images/m08.png) | 上三叉       | 3 (TICKDOWN)       | ![m28](https://www.runoob.com/images/m28.png) | 下竖线                                       |
| "3"  | ![m09](https://www.runoob.com/images/m09.png) | 左三叉       | 4 (CARETLEFT)      | ![m29](https://www.runoob.com/images/m29.png) | 左箭头                                       |
| "4"  | ![m10](https://www.runoob.com/images/m10.png) | 右三叉       | 5 (CARETRIGHT)     | ![m30](https://www.runoob.com/images/m30.png) | 右箭头                                       |
| "8"  | ![m11](https://www.runoob.com/images/m11.png) | 八角形       | 6 (CARETUP)        | ![m31](https://www.runoob.com/images/m31.png) | 上箭头                                       |
| "s"  | ![m12](https://www.runoob.com/images/m12.png) | 正方形       | 7 (CARETDOWN)      | ![m32](https://www.runoob.com/images/m32.png) | 下箭头                                       |
| "p"  | ![m13](https://www.runoob.com/images/m13.png) | 五边形       | 8 (CARETLEFTBASE)  | ![m33](https://www.runoob.com/images/m33.png) | 左箭头 (中间点为基准)                        |
| "P"  | ![m23](https://www.runoob.com/images/m23.png) | 加号（填充） | 9 (CARETRIGHTBASE) | ![m34](https://www.runoob.com/images/m34.png) | 右箭头 (中间点为基准)                        |
| "*"  | ![m14](https://www.runoob.com/images/m14.png) | 星号         | 10 (CARETUPBASE)   | ![m35](https://www.runoob.com/images/m35.png) | 上箭头 (中间点为基准)                        |
| "h"  | ![m15](https://www.runoob.com/images/m15.png) | 六边形 1     | 11 (CARETDOWNBASE) | ![m36](https://www.runoob.com/images/m36.png) | 下箭头 (中间点为基准)                        |
| "H"  | ![m16](https://www.runoob.com/images/m16.png) | 六边形 2     | "None", " " or ""  |                                               | 没有任何标记                                 |
| "+"  | ![m17](https://www.runoob.com/images/m17.png) | 加号         | '$...$'            | ![m37](https://www.runoob.com/images/m37.png) | 渲染指定的字符。例如 "$f$" 以字母 f 为标记。 |
| "x"  | ![m18](https://www.runoob.com/images/m18.png) | 乘号 x       |                    |                                               |                                              |



#### 线的类型

线的类型可以使用 `linestyle` 参数来定义，简写为 `ls`。`plt.plot(ypoints, linestyle = ':')`

|      类型      |   参数   |  说明  |
| :--------: | :---------: | :----: |
| 'solid' (默认) |    '-'    |  实线  |
|    'dotted'    |    ':'    | 点虚线 |
|    'dashed'    |   '--'    | 破折线 |
|   'dashdot'    |   '-.'    | 点划线 |
|     'None'     | '' 或 ' ' | 不画线 |





#### 线的颜色

线的颜色可以使用 `color` 参数来定义，简写为 `c`。`plt.plot(ypoints, color = 'r')`

| 颜色标记 | 描述 |
| :----: | :--: |
|   'r'    | 红色 |
|   'g'    | 绿色 |
|   'b'    | 蓝色 |
|   'c'    | 青色 |
|   'm'    | 品红 |
|   'y'    | 黄色 |
|   'k'    | 黑色 |
|   'w'    | 白色 |





### 标签

使用`xlabel()`和`ylabel()`方法来设置x轴和y轴的标签

使用``title()`方法设置标题

```python
import matplotlib
import matplotlib.pyplot as plt
import numpy as np

# 设置matplot的字体为楷体
matplotlib.rcParams['font.sans-serif'] = ['KaiTi']

x = np.array([80, 85, 90, 95, 100, 105, 110, 115, 120, 125])
y = np.array([240, 250, 260, 270, 280, 290, 300, 310, 320, 330])

# 1-1设置标签
plt.xlabel("平均脉搏")
plt.ylabel("卡路里消耗量")
# 1-2设置字体属性
font_label = {'color': 'blue', 'size': 15}
plt.xlabel("平均脉搏", fontdict=font_label)
plt.ylabel("卡路里消耗量", fontdict=font_label)

# 2-1设置标题
plt.title("运动手表数据")
# 2-2设置字体属性
font_title = {'color': 'darkred', 'size': 20}
plt.title("运动手表数据", fontdict=font_title)
# 2-3定位标题，使用loc参数'left', 'center', 'right'
plt.title("运动手表数据", loc='left')

plt.show()
```



### 网格线

我们可以使用`pyplot`中的 `grid() `方法来设置图表中的网格线。

```python
# grid()方法语法格式
matplotlib.pyplot.grid(b=None, which='major', axis='both', )
# b：可选，默认为 None，可以设置布尔值，true 为显示网格线，false 为不显示，如果设置 **kwargs 参数，则值为 true。
# which：可选，可选值有 'major'、'minor' 和 'both'，默认为 'major'，表示应用更改的网格线。
# axis：可选，设置显示哪个方向的网格线，可以是取 'both'（默认），'x' 或 'y'，分别表示两个方向，x 轴方向或 y 轴方向。
# **kwargs：可选，设置网格样式，可以是 color='r', linestyle='-' 和 linewidth=2，分别表示网格线的颜色，样式和宽度。简写分别为c,ls,lw
```



```python
"""
	....
"""
plt.xlabel("平均脉搏")
plt.ylabel("卡路里消耗量")
plt.title("运动手表数据")

# 1 使用grid()
plt.grid()
# 2 只显示x轴的线
plt.grid(axis='x')
# 3 设置网格线的属性
plt.grid(color='g', linestyle='-.', linewidth=0.5)
plt.grid(c='g', ls='-.', lw=2)		# 简写形式

plt.show()
```





## 多图

使用`subplot()`或者`subplot()`方法

`subplot()`方法在绘图时需要指定位置，`subplots()`方法可以一次生成多个，在调用时只需要调用生成对象的 `ax` 即可。



### 1. `subplot()`

```python
# subplot
# 将整个绘图区域分成 nrows 行和 ncols 列，然后从左到右，从上到下的顺序对每个子区域进行编号 1...N ，左上的子区域的编号为 1、右下的区域编号为 N，编号可以通过参数 index 来设置。
subplot(nrows, ncols, index, **kwargs)
subplot(pos, **kwargs)
subplot(**kwargs)
subplot(ax)
```



```python
import matplotlib.pyplot as plt
import numpy as np

# plot1
x1 = np.array([1, 2, 4, 8])
y1 = np.array([3, 8, 1, 10])
plt.subplot(1, 2, 1)	# 指定位置
plt.plot(x1, y1)
plt.title("plot1")

# plot2
x2 = np.array([0, 3, 5, 8])
y2 = np.array([1, 6, -1, 8])
plt.subplot(1, 2, 2)	# 指定位置
plt.plot(x2, y2)
plt.title("plot2")

# 为整个图形添加标题
plt.suptitle("subplot title test")

plt.show()
```





### 2. `subplots()`

```python
matplotlib.pyplot.subplots(nrows=1, ncols=1, *, sharex=False, sharey=False, squeeze=True, subplot_kw=None, gridspec_kw=None, **fig_kw)
```

`plt.subplots()`方法是一个非常有用的工具，它允许你在一个图表中创建多个子图，方便进行多个数据的可视化和比较。下面我将详细介绍`plt.subplots()`方法的使用方法。

#### 1. 基本用法

首先，我们来看一下`plt.subplots()`方法的基本用法。`plt.subplots()`方法可以传入两个整数参数`nrows`和`ncols`，用于指定子图的行数和列数。该方法会返回一个`Figure`对象和一个包含子图对象的二维数组，你可以通过索引来访问各个子图对象。

```python
import matplotlib.pyplot as plt

# 创建一个2x2的图表，并返回figure对象和一个包含四个子图对象的数组
fig, axarr = plt.subplots(2, 2)

# 在第一个子图中绘制数据
axarr[0, 0].plot([1, 2, 3, 4], [1, 4, 9, 16])

# 在第二个子图中绘制数据
axarr[0, 1].scatter([1, 2, 3, 4], [1, 4, 9, 16])

# 在第三个子图中绘制数据
axarr[1, 0].bar([1, 2, 3, 4], [1, 4, 9, 16])

# 在第四个子图中绘制数据
axarr[1, 1].hist([1, 2, 3, 4], bins=[0, 1, 2, 3, 4, 5])

# 显示图表
plt.show()
```



#### 2. 调整子图的排列方式和间距

除了基本用法，你还可以使用`plt.subplots()`方法的其他参数来调整子图的排列方式和间距。例如，使用`sharex`和`sharey`参数来共享子图的x轴和y轴刻度，使用`gridspec_kw`参数来设置子图的网格样式，使用`figsize`参数来设置整个图表的大小等。

```python
import matplotlib.pyplot as plt

# 创建一个2x2的图表，共享x轴和y轴刻度
fig, axarr = plt.subplots(2, 2, sharex=True, sharey=True)

# 设置整个图表的大小
fig.set_size_inches(8, 6)

# 在第一个子图中绘制数据
axarr[0, 0].plot([1, 2, 3, 4], [1, 4, 9, 16])

# 在第二个子图中绘制数据
axarr[0, 1].scatter([1, 2, 3, 4], [1, 4, 9, 16])

# 在第三个子图中绘制数据
axarr[1, 0].bar([1, 2, 3, 4], [1, 4, 9, 16])

# 在第四个子图中绘制数据
axarr[1, 1].hist([1, 2, 3, 4], bins=[0, 1, 2, 3, 4, 5])

# 调整子图之间的间距
plt.tight_layout()

# 显示图表
plt.show()
```



#### 3. 设置子图的标题和坐标轴标签

你可以使用子图对象的方法来设置子图的标题和坐标轴标签，例如`set_title()`、`set_xlabel()`和`set_ylabel()`等。

```python
import matplotlib.pyplot as plt

# 创建一个2x2的图表
fig, axarr = plt.subplots(2, 2)

# 在第一个子图中绘制数据
axarr[0, 0].plot([1, 2, 3, 4], [1, 4, 9, 16])
axarr[0, 0].set_title("Line Plot")
axarr[0, 0].set_xlabel("X Axis")
axarr[0, 0].set_ylabel("Y Axis")

# 在第二个子图中绘制数据
axarr[0, 1].scatter([1, 2, 3, 4], [1, 4, 9, 16])
axarr[0, 1].set_title("Scatter Plot")
axarr[0, 1].set_xlabel("X Axis")
axarr[0, 1].set_ylabel("Y Axis")

# 在第三个子图中绘制数据
axarr[1, 0].bar([1, 2, 3, 4], [1, 4, 9, 16])
axarr[1, 0].set_title("Bar Plot")
axarr[1, 0].set_xlabel("X Axis")
axarr[1, 0].set_ylabel("Y Axis")

# 在第四个子图中绘制数据
axarr[1, 1].hist([1, 2, 3, 4], bins=[0, 1, 2, 3, 4, 5])
axarr[1, 1].set_title("Histogram")
axarr[1, 1].set_xlabel("X Axis")
axarr[1, 1].set_ylabel("Frequency")

# 调整子图之间的间距
plt.tight_layout()

# 显示图表
plt.show()
```



#### 4. 子图占据多行多列

```python
import matplotlib.pyplot as plt

# 创建一个2x3的子图布局
fig, axs = plt.subplots(2, 3)

# 移除原有的子图
for ax in axs.flat:
    ax.remove()

# 使用GridSpec来设置复杂的子图布局
gs = plt.GridSpec(2, 3)

# 将第一张图片放在第1、2、4、5个位置（跨越第1行和第1列）
ax_combined = fig.add_subplot(gs[0:2, 0:2])
ax_combined.plot([1, 2, 3, 4], [4, 5, 6, 7])

# 将第2张图片放在第3个位置
axs[0, 2] = fig.add_subplot(gs[0, 2])
axs[0, 2].plot([3, 2, 1], [6, 5, 4])

# 将第3张图片放在第6个位置
axs[1, 2] = fig.add_subplot(gs[1, 2])
axs[1, 2].plot([7, 8, 9], [10, 11, 12])

# 调整子图之间的间距
plt.tight_layout()

# 显示图表
plt.show()
```

