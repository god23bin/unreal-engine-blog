---
title: Blender 90分钟入门笔记
date: 2024/6/19 20:23:25
index_img: /img/postcover/blender.png
banner_img: /img/postcover/blender.png
categories:
  - Blender
tag:
  - 建模
  - 渲染
  - 灯光
  - 材质
published: true
---

## 基础操作以及常用的快捷键

![初始界面](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624193636026.png)

### 3D 视图的操作

#### 场景镜头

旋转镜头：按住鼠标中键，拖动鼠标进行旋转

移动镜头：按住 Shift + 鼠标中键，拖动鼠标进行移动

缩放镜头：滚动鼠标中键进行缩放

#### 对象

移动对象（Grab）：快捷键 G

旋转对象（Rotate）：快捷键 R

缩放对象（Scale）：快捷键 S

在此基础上，按 X、Y、Z 键可以沿着对应的轴进行编辑。

#### 视图调整

正视图：小键盘 1

右视图：小键盘 3

透视图：小键盘 5

顶视图：小键盘 7

小键盘 Del 键：拉近到最大化视角。

小键盘 / 键：单独显示某一对象，其他对象会隐藏。

## 凳子案例

### Shift + A 添加物体

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624203149839.png)

### Ctrl + Tab

Ctrl + Tab 可以出现弹窗，有 6 个选项，现在选择**编辑模式**，可以编辑模型。

在编辑模式中，选中模型的点、边，即可对其进行调整。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624195456593.png)

### Alt + Z 透视显示模式

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624200115246.png)

在透视模式下，我们用鼠标框选正视图下正方形的底边。

看似只选了一条边，实际上整个正方体的底面都被选择了，因为处于透视模式下，可以选择到正常模式下选不到的点和边。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624200941880.png)

### Ctrl + B 倒角

倒角工具用于为几何体创建倒角或者圆角。所谓倒角，即用来平滑边线或拐角的。

#### 编辑模式下的选择模式

![编辑模式中的选择模式](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624201415243.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624202249399.png)

#### Ctrl + B 倒角

选中需要倒角的边，然后 Ctrl + B

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624202548636.png)

直接点击对象，左下角展开倒角选项卡，单独精确调整。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624202824259.png)

由于我们先选择了边，所以这里倒角影响的是**边**。接着我们主要调整宽度和段数。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624203039952.png)

### 平滑着色

倒角后的边实际上是有点棱角的，主要就是表面不光滑，解决这个问题就在**物体模式**下通过右键选择**平滑着色**。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624203721569.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624203813504.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624203833793.png)

### Alt 循环选边

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624204649897.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624204724908.png)

Alt + Shift 多选循环选边

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624204832590.png)

### Shift + D 复制

### X 删除

### 镜像修改器

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624205503420.png)

### 设置物体的轴中心（轴心点）

这样旋转时，物体就是以自己的几何中心为原点进行旋转。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624205830739.png)

### 分割窗口

鼠标放在视图左上角边框位置，鼠标出现十字准心，拖拽可以分割窗口。

## 咖啡案例

### Ctrl + R 循环切割

在编辑模式下，使用 Ctrl + R 可以循环切割

### I 插入一个面（内插面）

在编辑模式下，选择一个面，按键盘 I 键，可以插入一个面

### E 挤压一个面（挤出面）

按下 I 之后，有了一个面，我们按下 E 键，可以挤压这个面。

### 表面细分修改器

用于将网格的面分割成更小的面，使其看起来更加平滑。使我们可以对简单模型创建复杂的光滑表面。

一般配合循环切割使用。

### F 封闭填充缺失的面

### 书本内插面

编辑模式下，面选择模式，选中三个面，右键内插面。接着调整内插面。

现在面有了，接着就是调整深度了，右键沿法向挤出面，顾名思义，沿面的法向量的方向进行挤压。





