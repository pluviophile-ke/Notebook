# Python面向对象编程



[【放松一刻】咻咻满《我想要》_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1iK411Q7pq/?vd_source=a26806a76d4618342a3d74d75fe95c73)




[toc]



面向对象就是将编程当成是一个事物，对外界来说，事物是直接使用的，不用去管它内部的情况。而编程就是设置事物能够做什么事。



比如：图纸→洗衣机→洗衣服
类：创建图纸
对象：洗衣机
类和对象的关系：用类实例化一个对象（用类创建一个对象）



## 一、理解类和对象

类是对一系列具有相同特征和行为的事物的统称，是一个抽象的概念，不是真实存在的事物
* 特征既是属性
* 行为即使方法

对象是类创建出来的真实存在的事物，例如：洗衣机

注意：开发中先有类，再创建对象



## 二、面向对象实现方法

举例子：

需求：洗衣机

功能：能洗衣服

1. 定义洗衣机类

2. 创建对象

3. 验证成果

### 定义类

语法，类名要满足标识符命名规则，同时遵循==大驼峰命名习惯== 

```python
class 类名():
    Code
    ……
```

体验

```python
# 定义洗衣机类
class Washer():
    def wash(self):
        print("洗衣服")
```

### 创建对象

语法

```python
对象名 = 类名()
```

体验

```python
# 创建对象
haier = Washer()

# <__main__.Washer object at 0x000001EDE94159A0>
print(haier)

# haier对象调用实例方法
haier.wash()
```



### self是什么

打印haier对象和self，发现两个都打印出了对象所在的内存地址且相同。

```python
# 定义洗衣机类
class Washer():
    def wash(self):
        print("洗衣服")
        print(self)
        
# 创建对象
haier = Washer()

# <__main__.Washer object at 0x000001EDE94159A0>
print(haier)

# haier对象调用实例方法
haier.wash()
```

<__main__.Washer object at 0x000001B296872FA0>
洗衣服
<__main__.Washer object at 0x000001B296872FA0>



## 三、添加和获取对象属性

属性即是特征。如：洗衣机长宽高、重量等

对象属性既可以在类外面添加和获取，也能在类里面添加和获取。



### 类外面添加对象属性

语法

```python
对象名.属性名 = 值
```

体验（不需要提前在类中有此属性）

```python
haier.width = 500
haier.height = 800
```

### 类外面获取对象属性

语法

```python
对象名.属性名
```

体验

```python
print(f"haier洗衣机的宽度是{haier.width}")
print(f"haier洗衣机的高度是{haier.height}")
```



### 类里面获取对象属性

语法

```python
self.属性名
```

体验

```python
# 定义洗衣机类
class Washer:
    def print_info(self):
        print(f"haier洗衣机的宽度是{self.width}")
        print(f"haier洗衣机的高度是{self.height}")

    def wash(self):
        print(self)
        print("洗衣服")


# 创建对象
haier = Washer()

# 在类外面添加实例属性
haier.width = 500
haier.height = 800

# 在类里面获取对象属性
haier.print_info()
```

haier洗衣机的宽度是500
haier洗衣机的高度是800



## 四、魔法方法

### `__init__()` 

思考：洗衣机的长宽高重量是与生俱来的属性，可不可以在生产过程中就赋予这些属性呢？

答：理应如此，在创建对象之前就有这个属性，即在类里面设置这些属性

`__init__()`方法的==作用==：初始化对象。即设置与生俱来的初始化属性。

**注意**：`__init__()` 方法，在创建一个对象时默认被调用，不需要手动调用，其中的self参数，不需要开发者传递，python解释器会自动把当前的对象引用传递过去。

体验

```python
# 定义洗衣机类
class Washer:
    # 定义__init__，添加实例属性
    def __init__(self):
        self.width = 500
        self.height = 800

    # 打印属性信息
    def print_info(self):
        print(f"haier洗衣机的宽度是{self.width}")
        print(f"haier洗衣机的高度是{self.height}")


# 创建对象
haier = Washer()
# 打印实例属性
haier.print_info()
```

haier洗衣机的宽度是500
haier洗衣机的高度是800



* 带参数的`__init__()`

思考：一个类可以创建多个对象，如何对不用的对象设置不同的初始化值呢？

答：传参数

体验

```python
# 定义洗衣机类
class Washer:
    def __init__(self, width, height=800):
        self.width = width
        self.height = height

    def print_info(self):
        print(f"haier洗衣机的宽度是{self.width}")
        print(f"haier洗衣机的高度是{self.height}")

# 创建对象
haier = Washer(400, 600)
# 打印信息
haier.print_info()
```

haier洗衣机的宽度是400
haier洗衣机的高度是600



### `__str()__` 

当使用print输出对象数据时，默认打印对象的内存地址。如果定义了`__str__`方法，那么就会打印这个方法return的数据

体验

```python
# 定义类
class Washer:
    def __init__(self, width, height=800):
        self.width = width
        self.height = height

    def __str__(self):
        return f"宽度：{self.width}\n" \
               f"高度：{self.height}"

# 实例化
haier = Washer(400, 600)
print(haier)
```

宽度：400
高度：600



### `__del__()`

当删除对象时，python解释器会默认调用`__del__()`方法

体验

```python
# 定义类
class Washer:
    def __init__(self, width, height=800):
        self.width = width
        self.height = height

    def __str__(self):
        return f"宽度：{self.width}\t" \
               f"高度：{self.height}"

    def __del__(self):
        print(f"{self}对象已经被删除")


haier = Washer(400, 600)
del haier
```

宽度：400	高度：600对象已经被删除



>  注意：在现有程序中，即便不手动删除对象，也能调用`__del__()`魔法方法，代码执行完毕后，内存中存储的变量等都会自动释放（对象也会自动删除掉），`__del__()`魔法方法自动调用





---



## 五、综合应用

### 烤地瓜

需求 → 分析步骤 → 代码落地

#### 需求

1. 被烤的时间和对应的地瓜状态

   * 0 - 3分钟：生的
   * 3 - 5分钟：半生不熟
   * 5 - 8分钟：熟的
   * 超过8分钟：烤糊了

2. 添加的调料

   用户可以按照自己的意愿添加调料

#### 分析步骤

* 地瓜的属性
  * 被烤的时间
  * 地瓜的状态
  * 添加的调料
* 地瓜的方法
  * 被烤
    * 用户根据医院设定每次烤地瓜的时间
    * 判断地瓜被烤的总时间是在哪个区间，修改地瓜状态
  * 添加调料
    * 用户根据意愿设定添加的调料
    * 将用户添加的调料存储
* 显示对象的信息

#### 书写代码

```python
# 定义地瓜类：
# 初始化属性、被烤和添加调料的方法、显示对象信息的str
class SweetPotato:
    def __init__(self, cook_time=0):
        self.cook_time = cook_time  # 被烤的时间
        self.cook_status = '生的'  # 烤的状态
        self.condiment = []  # 调料列表
        self.roast(0)   # 更新初始化时的状态

    def __str__(self):
        return f"这个地瓜烤了{self.cook_time}分钟\t" \
               f"状态是{self.cook_status}\t" \
               f"调料为{self.condiment}"

    def roast(self, delta_time=0):
        """烤地瓜的方法"""
        self.cook_time += delta_time
        if 0 <= self.cook_time < 3:
            self.cook_status = '生的'
        elif 3 <= self.cook_time < 5:
            self.cook_status = '半生不熟'
        elif 5 <= self.cook_time < 8:
            self.cook_status = '熟的'
        elif self.cook_time >= 8:
            self.cook_status = '烤糊了'

    def add_condiment(self, condiment):
        """添加调料"""
        self.condiment.append(condiment)


# 创建对象并调用对应的实例方法
digua1 = SweetPotato()
print(digua1)
# 烤2分钟
digua1.roast(2)
digua1.add_condiment("辣椒面")
print(digua1)
# 再烤3分钟
digua1.roast(3)
digua1.add_condiment("蜂蜜")
print(digua1)
```

这个地瓜烤了0分钟	状态是生的	调料为[]
这个地瓜烤了2分钟	状态是生的	调料为['辣椒面']
这个地瓜烤了5分钟	状态是熟的	调料为['辣椒面', '蜂蜜']



### 搬家具

#### 需求

将小于房子剩余面积的家具摆放到房子中

#### 分析步骤

需求涉及两个事物：房子和家具，故此案涉及两个类：房子类和家具类

定义类

* 房子类
  * 实例属性
    * 房子地理位置
    * 房子占地面积
    * 房子剩余面积
    * 房子内家具列表
  * 实例方法
    * 容纳家具
  * 显示房屋信息
* 家具类
  * 家具名称
  * 家具占地面积

#### 书写代码

```python
# 家具类
class Furniture:
    def __init__(self, name, area):
        self.name = name	# 家具名称
        self.area = area	# 家具占地面积

# 房子类
class House:
    def __init__(self, address, area):
        self.address = address  # 地理位置
        self.area = area        # 房屋面积
        self.free_area = area   # 房屋剩余面积
        self.furniture = []     # 家具列表

    def __str__(self):
        return f"房屋坐落于{self.address}，占地面积{self.area}，" \
               f"剩余面积{self.free_area}，家具有{self.furniture}"

    def add_furniture(self, item):
        """容纳家具"""
        if self.free_area >= item.area:
            self.furniture.append(item.name)
            self.free_area -= item.area
        else:
            print("家具太大，剩余面积不足，无法容纳")


# 实例化
bed = Furniture('双人床', 6)
sofa = Furniture('沙发', 3)

houseBig = House("北京", 200)
houseBig.add_furniture(bed)
print(houseBig)
```

房屋坐落于北京，占地面积200，剩余面积194，家具有['双人床']





---



## 六、继承

### 概念

**扩展**：经典类和新式类

不由任意内置类型派生出的类，称之为经典类

```python
class 类名:
    代码
```

新式类（python3默认为新式类）。

```python
class 类名(object):
    代码
```

python3.6后无经典类和新式类的区分，都是广度优先原则。

即`class A:` 等价于`class A():` 等价于`class A(object):`



python面向对象的继承指的是多个类之间的所属关系，即子类默认继承父类的所有属性和方法。

体验

```python
# coding=utf-8
class A(object):
    def __init__(self):
        self.num = 1
        
    def print_info(self):
        print(self.num)


class B(A):
    pass


# create an object
result = B()
print(result.num)	# 1
result.print_info()	# 1
```

> 在python中，所有类默认继承object类，object类是顶级类或基类；其他子类叫做派生类。



### 单继承和多继承

#### 单继承

一个父类继承给一个子类，这种单一的继承关系称之为单继承

```python
# coding=utf-8
class Master(object):
    def __init__(self):
        self.kungfu = "古法煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        print(f"运用{self.kungfu}制作煎饼果子")


class Prentice(Master):
    pass


daqiu = Prentice()
daqiu.make_cake()
```



#### 多继承

所谓多继承意思就是一个类同时继承了多个父类

**注意：当一个类有多个父类的时候，同名属性和方法默认使用第一个父类的**

如：下面代码优先使用`School`类的方法

```python
# coding=utf-8
class Master(object):
    """师父类"""
    def __init__(self):
        self.kungfu = "古法煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        print(f"运用{self.kungfu}制作煎饼果子")


class School(object):
    """学校类"""
    def __init__(self):
        self.kungfu = "新东方煎饼果子配方"

    def make_cake(self):
        print(f"运用{self.kungfu}制作煎饼果子")


class Prentice(School, Master):
    """徒弟类"""
    pass


daqiu = Prentice()
daqiu.make_cake()
```

运用新东方煎饼果子配方制作煎饼果子





### 子类重写父类的同名属性和方法

如果子类和父类拥有同名属性和方法，子类创建的对象，调用的同名属性或方法是子类中的。

```python
# coding=utf-8
class Master(object):
    """师父类"""
    def __init__(self):
        self.kungfu = "古法煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        print(f"运用{self.kungfu}制作煎饼果子")


class School(object):
    """学校类"""
    def __init__(self):
        self.kungfu = "新东方煎饼果子配方"

    def make_cake(self):
        print(f"运用{self.kungfu}制作煎饼果子")


class Prentice(School, Master):
    """徒弟类"""
    def __init__(self):
        self.kungfu = "独创煎饼果子配方"

    def make_cake(self):
        print(f"运用{self.kungfu}制作煎饼果子")


daqiu = Prentice()
daqiu.make_cake()
```



---

**拓展：查看继承的父类以及层级关系**

```python
print(类名.__mro__)
```

实例：在上次代码的基础上添加下面的代码，查看输出

```python
print(Prentice.__mro__)
"""
(<class '__main__.Prentice'>, <class '__main__.School'>, <class '__main__.Master'>, <class 'object'>)
"""
```

---



### 子类调用父类的同名属性和方法

**子类调用父类的同名属性和方法，把父类的同名属性和方法再次封装。**

注意到`Prentice`类中每次调用`类名.make_cake()`的时候都有`__init__()`，是因为如果不写这个魔法方法，就会被上一次的同名属性所覆盖，所以每次都要初始化要调用类的属性。

同时注意到：在`self.__init__()`中是没有self参数的，原因是`Prentice`类中的`self`都是指的`Prentice`实例化的对象，所以初始化父类属性需要传入`self`，而初始化自己属性不用传入self。

代码（关键代码在 27 - 44 行）

```python
# coding=utf-8
class Master(object):
    """师父类"""
    def __init__(self):
        self.kungfu = "古法煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        print(f"运用{self.kungfu}制作煎饼果子")


class School(object):
    """学校类"""
    def __init__(self):
        self.kungfu = "新东方煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        print(f"运用{self.kungfu}制作煎饼果子")


class Prentice(School, Master):
    """徒弟类"""
    def __init__(self):
        self.kungfu = "独创煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        # 如果先是调用了父类的属性和方法，父类属性会覆盖子类属性，故在调用属性前，先调用自己子类的初始化
        self.__init__()
        print(f"运用{self.kungfu}制作煎饼果子")

    def make_master_cake(self):
        """
        制作师父煎饼果子
        子类调用父类的同名属性和方法，把父类的同名属性和方法再次封装
        """
        Master.__init__(self)
        Master.make_cake(self)

    def make_school_cake(self):
        """制作学校煎饼果子"""
        School.__init__(self)
        School.make_cake(self)


daqiu = Prentice()
# 大秋制作师父煎饼
daqiu.make_master_cake()
# 大秋制作学校煎饼
daqiu.make_school_cake()
# 大秋制作独创煎饼
daqiu.make_cake()
```

运用古法煎饼果子配方制作煎饼果子
运用新东方煎饼果子配方制作煎饼果子
运用独创煎饼果子配方制作煎饼果子





### 多层继承

【师父、新东方】→【大秋】→【小二】

```python
# coding=utf-8
class Master(object):
    """师父类"""
    def __init__(self):
        self.kungfu = "古法煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        print(f"运用{self.kungfu}制作煎饼果子")


class School(object):
    """学校类"""
    def __init__(self):
        self.kungfu = "新东方煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        print(f"运用{self.kungfu}制作煎饼果子")


class Prentice(School, Master):
    """徒弟类"""
    def __init__(self):
        self.kungfu = "独创煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        # 如果先是调用了父类的属性和方法，父类属性会覆盖子类属性，故在调用属性前，先调用自己子类的初始化
        self.__init__()
        print(f"运用{self.kungfu}制作煎饼果子")

    def make_master_cake(self):
        """
        制作师父煎饼果子
        子类调用父类的同名属性和方法，把父类的同名属性和方法再次封装
        """
        Master.__init__(self)
        Master.make_cake(self)

    def make_school_cake(self):
        """制作学校煎饼果子"""
        School.__init__(self)
        School.make_cake(self)


class Tusun(Prentice):
    pass


xiaoer = Tusun()

# 小二制作师父煎饼
xiaoer.make_master_cake()
# 小二制作学校煎饼
xiaoer.make_school_cake()
# 小二制作独创煎饼
xiaoer.make_cake()
```



### `super()`调用父类方法



---

回忆：不用`super()`也可以实现调用父类的方法

* 同名：即`类名.方法名(self)`，并在上一行`类名.__init__(self)`初始化类属性。代码比较冗余。

* 不同名：直接调用

---



`super()`有两个方法，一个是带有参数的方法，另一个是不带参数的方法。

方法一：完整的写法

```python
super(当前类名, self).__init__()
super(当前类名, self).函数()
```

方法二：简化写法

```python
super().__init__()
super().函数()
```



实现【Master】→【School】→【Prentice】

```python
# coding=utf-8
class Master(object):
    """师父类"""
    def __init__(self):
        self.kungfu = "古法煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        print(f"运用{self.kungfu}制作煎饼果子")


class School(Master):
    """学校类"""
    def __init__(self):
        self.kungfu = "新东方煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        print(f"运用{self.kungfu}制作煎饼果子")
        # super(School, self).__init__()  # Master方法一
        # super(School, self).make_cake()
        super().__init__()      # School方法二
        super().make_cake()


class Prentice(School):
    """徒弟类"""
    def __init__(self):
        self.kungfu = "独创煎饼果子配方"

    def make_cake(self):
        """制作煎饼果子"""
        # 如果先是调用了父类的属性和方法，父类属性会覆盖子类属性，故在调用属性前，先调用自己子类的初始化
        self.__init__()
        print(f"运用{self.kungfu}制作煎饼果子")

    def make_old_cake(self):
        """使用super"""
        # super(Prentice, self).__init__()    # School方法一
        # super(Prentice, self).make_cake()
        super().__init__()      # School方法二
        super().make_cake()


daqiu = Prentice()
daqiu.make_old_cake()
```

运用新东方煎饼果子配方制作煎饼果子
运用古法煎饼果子配方制作煎饼果子



### 私有属性和私有方法

在python中，可以为实例属性和方法设置私有权限，即设置某个实例属性或实例方法不继承给子类。

设置私有权限的方法：在属性名和方法名前面加上两个下划线。

```python
# 示例
self.__money = 200

def __infomation():
    pass
```



修改私有属性和私有方法：只能在类里面访问和修改

```python
class Master(object):
    def __init__(self):
        self.kungfu = "古法煎饼果子"
        self.__money = 2000	# 私有属性
        
    def __infomation():
        """私有方法"""
        pass
      
    def get_money(self):
        """获取私有属性"""
        return self.__money
    
    def set_money(self, money):
        """修改私有属性"""
        self.__money = money
        
laoliu = Master()
print(laoliu.get_money())
laoliu.set_money(500)
print(laoliu.get_money())
```



# 面向对象-其他



## 1.面向对象三大特性

* **封装**
  * 将属性和方法写到类的里面的操作即为封装
  * 封装可以为属性和方法添加私有权限
* **继承**
  * 子类默认继承父类的所有属性和方法
  * 子类可以重写父类属性和方法

* **多态**
  * 传入不同的对象，产生不同的结果



## 2.多态

### 2.1了解多态

多态指的是一类事物有多种形态，一个抽象类有多个子类，因而多态的概念依赖于**继承**。（python多态不必须依赖继承，但最好依赖继承）

* 定义：多态是一种使用对象的方式，子类重写父类方法，调用不同子类对象的相同父类方法，可以产生不同的执行结果。
* 好处：调用灵活，有了多态，更容易编写通用代码，做出通用编程，以适应需求的不断变化！
* 实现步骤：
  * 定义父类，并提供公共方法
  * 定义子类，并重写父类方法
  * 传递子类对象给调用者，可以看到不同子类执行效果不同





### 2.2体验多态

1. 

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def make_sound(self):
        pass


class Dog(Animal):
    def make_sound(self):
        return "Woof!"


class Cat(Animal):
    def make_sound(self):
        return "Meow!"


class Cow(Animal):
    def make_sound(self):
        return "Moo!"


animals = [Dog("Buddy"), Cat("Whiskers"), Cow("Milly")]

for animal in animals:
    print(animal.name + ": " + animal.make_sound())

"""
Buddy: Woof!
Whiskers: Meow!
Milly: Moo!
"""
```

> 这个例子展示了多态性的基本概念。Animal 类定义了一个抽象方法 make_sound()，它在派生类中被重写。Dog、Cat 和 Cow 类都是 Animal 类的子类，并且它们分别重写了 make_sound() 方法。通过创建一个动物列表，并迭代调用 make_sound() 方法，我们可以看到不同动物对象的多态行为。



2. 

```python
# coding=utf-8
class Dog(object):
    """狗狗类"""
    def work(self):
        pass


class PoliceDog(Dog):
    """警犬"""
    def work(self):
        print("追击敌人……")


class DrugDog(Dog):
    """缉毒犬"""
    def work(self):
        print("追查毒品……")


class Person(object):
    """人类"""
    def work_with_dog(self, dog):
        dog.work()


daqiu = Person()
ad = PoliceDog()
dd = DrugDog()

daqiu.work_with_dog(ad)
daqiu.work_with_dog(dd)
"""
追击敌人……
追查毒品……
"""
```



3. **题目：**

   假设你正在开发一个电商网站，需要设计一个基础的商品类（`Product`），并从该类派生出两个具体商品类：`Book`（书籍）和`Clothing`（服装）。请你完成以下任务：

   1. 在`Product`类中，定义一个抽象方法`calculate_price()`，用于计算商品的价格。该方法应返回一个浮点数。

   2. `Book`类应包含一个额外的实例变量`pages`（整数类型），并在构造函数中初始化。

   3. `Clothing`类应包含一个额外的实例变量`size`（字符串类型），并在构造函数中初始化。

   4. 在各个类中，实现`calculate_price()`方法来计算商品的价格。以下是价格计算的规则：

      * `Product`类的价格为0。

      * `Book`类的价格为`pages * 0.01`。

      * `Clothing`类的价格为`10 + len(size)`。

   5. 创建一个`Book`对象和一个`Clothing`对象，并分别调用它们的`calculate_price()`方法，然后输出计算得到的价格。

   请根据以上要求，完成代码并输出结果。

   ```python
   # coding=utf-8
   from abc import ABC, abstractmethod
   
   class Product(object):
       """基础类"""
       @abstractmethod		# 抽象方法
       def calculate_price(self):
           pass
   
   
   class Book(Product):
       """书籍类"""
       def __init__(self, pages):
           self.pages = pages
   
       def calculate_price(self):
           return self.pages * 0.01
   
   
   class Clothing(Product):
       """衣服类"""
       def __init__(self, size):
           self.size = size
   
       def calculate_price(self):
           return 10 + len(self.size)
   
   
   book1 = Book(500)
   print("book1 price", book1.calculate_price())
   
   clothing1 = Clothing("XLL")
   print("clothing1 price", clothing1.calculate_price())
   """
   book1 price 5.0
   clothing1 price 13
   """
   ```





---





## 3.类属性和实例属性

### 3.1类属性

#### 设置和访问类属性

设置和访问类属性
* 类属性就是 **类对象** 所拥有的属性，它被该类的所有实例对象所共有
* 类属性可以使用 **类对象** 或 **实例对象** 访问

```python
class Dog(object):
    tooth = 10		# 设置类属性
    

wangcai = Dog()
xiaohei = Dog()

print(Dog.tooth)	# 10
print(wangcai.tooth)	# 10
print(xiaohei.tooth)	# 10
```

> 类属性的优点
> * **记录的的某项数据始终保持一致时**，则定义类属性
> * **实例属性**要求**每个对象**为其**单独开辟一份内存空间**来记录数据，而**类属性**为全类所共有，**仅占用一份内存，更加节省空间**。



#### 修改类属性

类属性只能通过类对象进行修改，不能通过实例对象修改，如果通过实例对象修改类属性，表示的是创建了一个实例属性。

```python
class Dog(object):
    tooth = 10  # 设置类属性


wangcai = Dog()
xiaohei = Dog()

# 查看属性
print(Dog.tooth)
print(wangcai.tooth)
print(xiaohei.tooth)

# 修改类属性(类.类属性= )
Dog.tooth = 12

# 查看类属性
print(Dog.tooth)
print(wangcai.tooth)
print(xiaohei.tooth)
"""
10
10
10
12
12
12
"""
# -----------------------------------------
# -----------------------------------------
class Dog(object):
    tooth = 10  # 设置类属性


wangcai = Dog()
xiaohei = Dog()

# 查看属性
print(Dog.tooth)
print(wangcai.tooth)
print(xiaohei.tooth)

# 修改类属性，使用对象修改类属性相当于创建了实例属性
wangcai.tooth = 12

# 查看类属性
print(Dog.tooth)
print(wangcai.tooth)
print(xiaohei.tooth)
"""
10
10
10
10
12
10
"""
```



### 3.2实例属性

就是我们之前学习的属性。





---





## 4.类方法和静态方法

### 4.1类方法（class method）

#### ①类方法特点

类方法是绑定到类而不是实例的方法。它们用**装饰器**`@classmethod`来标识其为类方法，并且在方法定义中的**第一个参数必须是类对象**，通常被命名为 `cls`，表示类本身。通过使用类方法，可以在不实例化类的情况下直接调用它们。

#### ②类方法使用场景

* 当方法中 **需要使用类对象**（如访问私有类属性等）时，定义类方法
* 类方法一般和类属性配合使用



```python
class MyClass:
    __class_attribute = "Hello, class!"

    @classmethod
    def class_method(cls):
        return cls.__class_attribute

# 调用类方法
print(MyClass.class_method())

"""
Hello, class!
"""
```



### 4.2静态方法

@staticmethod

该方法不强制要求传递参数，如下声明一个静态方法

```python
class C(object):
    @staticmethod
    def f(arg1, arg2, ...):
        pass
```

以上声明了静态方法`f`，从而可以实现实例化使用`c().f()`，当然也可以不实例化调用该方法`c.f()`。

```python
class C(object):
    @staticmethod
    def f():
        print('runoob')


C.f()       # 静态方法无需实例化
cobj = C()  # 实例化后使用
cobj.f()

"""
runoob
runoob
"""
```













