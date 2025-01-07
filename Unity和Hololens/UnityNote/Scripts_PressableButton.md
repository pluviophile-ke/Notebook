# Pressable Button



## 1. Advanced StatefulInteractable Settings







## 2. MRTK Events

### 2.1 PressableButton Events

#### Is Proximity Hovered



### 2.2 StatefulInteractable Events

#### ①Is Toggled

#### ②OnEnable/Disable



### 2.3 MRTKBaseInteractable Hover Events

#### ①Is Gaze Hovered

​	视线悬停在对象上即触发（与`Advanced StatefulInteractable Settings`中设置无关）

#### ②Is Gaze Pinch Hovered

​	视线悬停在对象上and手出现在视野中and手距离对象有一定距离=触发，手指捏合则按钮按下（与`Advanced StatefulInteractable Settings`中设置无关）

#### ③Is Ray Hovered

​	手部射线悬停在对象上触发。

#### ④Is Poke Hovered

​	手戳在对象上时触发。

#### ⑤Is Active Hovered

​	对象被激活时触发





### 2.4 MRTKBaseInteractable Select Events

#### ①Is Grab Selected

​	凝视一定时间则触发按键（有按键按下的**动画**），使用此功能需要在`Advanced StatefulInteractable Settings`勾选`Use Gaze Dwell`，并在`Gaze Dwell Time`处填写凝视触发时间。

#### ②Is Ray Selected

​	由手部射线引起的按键触发，分为两种情况

1. 射线停留触发（无动画）

   需要在`Advanced StatefulInteractable Settings`勾选`Use Far Dwell`，并在`Far Dwell Time`处填写射线悬停触发时间。

2. 射线点击触发（有动画）

   不需要勾选`Advanced StatefulInteractable Settings`中的任何设置，手部射线按下即触发。

#### ③Is Gaze Pinch Selected

​	不需要勾选`Advanced StatefulInteractable Settings`中的任何设置。

​	视线悬停在对象上and手出现在视野中and手距离对象有一定距离and手指捏合=触发（有动画）。

#### ④Is Poke Selected

​	手指戳下按钮触发

