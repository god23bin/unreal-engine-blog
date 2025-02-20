---
title: Blender 4.0 入门笔记
date: 2024/7/4 20:46:25
index_img: /img/postcover/blender.png
banner_img: /img/postcover/blender.png
categories:
  - Blender
tag:
  - 建模
  - 渲染
  - 灯光
  - 材质
  - 动画
  - [骨骼,雕刻]
published: true
---

## 下载与安装

官方：[www.blender.org](www.blender.org)

斑斓中国

Steam

软件安装一路无脑回车

辣椒酱：https://www.blendermagic.cn/

### 关于软件的中文设置

编辑菜单 -> 偏好设置

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624224112890.png)

## 软件的功能模块

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624224247017.png)

### 模块介绍

布局：摆放模型

建模：编辑模型

雕刻：模型雕刻 ZB（ZBrush）

UV：模型的 UV 展开（便于后续绘制贴图）

纹理绘制：贴图

着色：材质编辑器

动画：模型动画

渲染：查看渲染图

合成：图片后期处理

几何节点：参数化建模

脚本：Python脚本

### 界面控制

观察虚拟世界

- 旋转观察：鼠标中键

- 平移观察：Shift + 鼠标中键

- 远近观察：Ctrl + 鼠标中键

- 居中显示：Home

正交图：

- 正面 小键盘 1
- 侧视图 小键盘 3 
- 顶视图 小键盘 7
- 底视图 小键盘 9
- 透视图与正交视图的切换 小键盘 5
- 剩余的 2 4 6 8 是用来旋转视图的

### 可能遇到的问题

1. Blender 鼠标中键滚动缩放视图时，无法放大、缩小或者很慢，同时按住中键移动时，视角并不会围绕中点旋转，而是基于自身旋转。怎么办？

**视图透视角度问题**：视图透视角度大则缩放容易，角度越小，缩放越困难。可以通过调整视图透视角度来改善缩放效果。按 `Shift + B`，拖动鼠标左键画个框，这样可以直接移动到所选区域，并恢复正常的缩放速度。

**选中对象并聚焦**：选中对象图层，按小键盘的 `.` 键，可以在视窗中放大显示对象。这是一个快速聚焦到对象的方法。

最一劳永逸的办法就是在菜单栏编辑→偏好设置→视图切换→视勾选“深度”，设置以后都可以用鼠标中键滚轮，滚动缩放。

参考：https://www.zhihu.com/question/540754063

### 界面规划

拖动边框出现新界面

喜欢一个界面布局，可以保存

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624224813298.png)

## 功能说明

### **添加模型**

- Shift + A 添加几何体

  ![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624235218391.png)

### **控制你的模型**

- 界面左侧 工具栏 T

  ![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624235134668.png)

- 游标 Shift + 右键

  游标在哪里，添加的物体就在哪里。

  ![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624235310332.png)

- 移动 G（XYZ）

- 旋转 R（XYZ）

- 缩放 S（XYZ）

  - 缩放罩体（鼠标长按缩放，可以选择缩放罩体）：可单独控制某一面的缩放，或者多面的缩放。

    ![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624235451407.png)

- 变换工具，包含移动 旋转 缩放

  ![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624235715697.png)

### **模型编辑-选择**

进入**建模** 模块 或者 按 Tab 进入编辑模式

#### 子元素控制：点 边 面

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240624235855984.png)

可通过键盘 1，2，3 来切换 点 边 面 选择模式。

#### 子元素选择

##### 循环选择（Alt，支持 点 边 面）

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625000553879.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625000612310.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625000637803.png)

##### 环形选择（Ctrl + Alt，只支持 边）

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625000728785.png)

多选按住 Shift，可配合循环多选，即按下 Shift 和 Alt 再进行选择

### 模型编辑-操作

#### 挤出 E

挤出一个面，可以向外或者向内。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625003556107.png)

其它挤出 Alt + E

#### 内插面 I 

可以在一个面中插入一个新的面。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625003811579.png)

#### 倒角 Ctrl + B

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625004409631.png)

#### 环切 Ctrl + R

可以切出多个面。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625004644699.png)

#### 环切偏移 Ctrl + Shift + R

在环切好的基础上可以继续偏移边线并滑移。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625004843262.png)

#### 切割（手工切线）K

切割后按 Enter 回车键确认。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625005044981.png)

#### 删除切线 Ctrl + X（融并命令）

选择删除的切线，按 Ctrl + X 可以删除。

#### 连接顶点线 J

选择两个顶点，按 J 可以连接成线。

### 布尔操作

计算模型之间 **交 并 差**

Ctrl + Shift + B 布尔工具

差集 Ctrl + Shift + `-`

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625010528683.png)

并集 Ctrl + Shift + `+`

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625010928788.png)

交集Ctrl + Shift + `*`

![image-20240625011232948](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625011232948.png)

## 建模

### 模式预览方式 Z

线框模式、实体模式、材质模式、渲染模式

### 快速切换线框 Shift + Z

### 叠加层（显示信息） Shift + Alt + Z

### 分离模型 P

### 合并模型 Ctrl + J

### 独立显示对象 /

### 复制模型 Shift+D

### 点 边 面的命令组

Ctrl+V 点命令组

Ctrl+E 边命令组

Ctrl+F 面命令组

桥接循环边（哑铃）

### 材质

窗口右侧的属性面板添加材质

AIt+M

### 点命令 Ctrl+V

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625221735262.png)

### 顶点倒角 Ctrl+SHift+B

### 链接顶点 J

### 断开顶点 V

### 焊接顶点 M

### 边命令 Ctrl+E

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625221859410.png)

Ctrl+B 倒角

细分

桥接

环切 Ctrl+R

### 面命令 Ctrl+F

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625221931953.png)

挤出 E

Alt + E

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625222021222.png)

内插面 I

填充 F

栅格化填充，能够完美填充曲率

独立显示 /

### 关于缩放后模型影响

物体模式下，Ctrl + A 清空缩放数据方便后续编辑

### 文件柜

调节切割次数

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625222809097.png)

内插面单独各个面插入

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625223019497.png)

### Shift + R 重复上一步骤

### Shift + S 设置游标到原点

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240703025817084.png)

### Ctrl + 小键盘加号 选中点扩选

扩展选择 

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240703032016168.png)

### 轴向概念

1. 轴向方向 **快捷键 <**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625223348375.png)

- 全局坐标轴（世界空间）
- 局部坐标轴（对象自身）
- 法向（面的朝向）
- 视图（坐标永远面对我们自己）
- 游标（以游标位置作为坐标轴）

2. 轴心位置 **快捷键 >**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240625231550809.png)

- 边界框中心，即选择中心（公共中心）为轴心

- 游标，即以游标为轴心（中心）
- 各自原点(自身轴点)

### Alt + M 沿边拆面

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626112531259.png)

### N 面板

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626114127564.png)

### 法线朝向

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626115025574.png)

正面蓝色，反面红色

解决：Alt + N ，翻转

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626115303613.png)

处理后的效果。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626121718568.png)

### Ctrl + > 移动轴心点

选中物体，按下 `Ctrl` 和 `>` ，出现轴心点，使用 G、R 调整轴心点位置，最后再按下 `Ctrl` 和 `>`  结束轴心点的调整。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626122841163.png)

### 修改器

窗口右侧属性面板--扳手

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626140342835.png)

#### 生成组

生成组主要是建模相关的修改器

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626140436404.png)

1. 阵列（快速复制多个）
2. 倒角（模型整体倒角）
3. 布尔修改器（可随时调整效果）
4. 精简（减少面数）
5. 遮罩（局部隐藏模型）
6. 镜像（对称效果）
7. 螺旋线（旋转建模，比如弹簧，酒杯）（车削）
8. 蒙皮（针对点的，对点进行蒙皮）
9. 实体化（增加厚度）
10. 表面细分（细分平滑）应用修改器的效果需要在物体模式下才能应用。
11. 焊接修改器
12. 线框修改器（适用于制作线框模型，比如铁丝网）

#### 变形组

模型外形修改

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626140727539.png)



### 球形化

L 选中相连的面后，网格->变换->球形化

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626190554214.png)

插入面 + 挤出 + 再挤出 + 缩放 + 删除，即可扣出一个洞

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626215810567.png)

### V 拆分点和边

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626220038023.png)

### 样条曲线

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626215718357.png)



点击一个点，可以按 G 移动，可以按 E 挤出。

数据面板中有两种模式，2D 和 3D。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626220301045.png)

#### 1. 建模

挤出

倒角

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626220527479.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626220643689.png)

深度用来增加曲线厚度

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626221252907.png)

#### 2. 动画

动画轨迹

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240626221617061.png)



#### 3. 曲线修改与编辑

手绘

钢笔 Ctrl + 点

挤出 E 

扭曲 Ctrl+T

切变

随机

#### 4. 曲线顶点类型 V

自动

手柄自定改变朝向矢量

形成尖角对齐

手柄两侧同时移动自由

手柄分开调整

#### 5. 曲线平滑

Shift + N



### 树工具

曲线 -> Sapling: Add Tree (Tree Gen)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240627095436452.png)

### 物理系统

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702013903684.png)

#### 刚体物理系统

活动对象：猴头

被动对象：地面（等待被碰撞的对象）

将猴头设置为活动项，平面设置为被动项，这样播放的时候，猴头就会自由落体，并与平面发生碰撞。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702014236137.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702014558258.png)

记得 Ctrl + A，清空对象的缩放数据。

#### 快速建模小技巧

先建好一个模型，接着其他相关的方块可以全部选中，接着最后选择我们编辑好的模型，按下 Ctrl + L，选择 `关联物体数据`。

#### 布料运算

布料对象：平面

碰撞对象：球

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702015500427.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702015825429.png)

#### 窗帘

编辑模式下，选中窗帘顶点，顶点->挂钩（Ctrl + H）->挂钩到一个物体

接着可以在修改器中看到挂钩，物体是空物体，也就是挂钩到空物体上了，我们可以吸管吸取挂到哪个物体上。

同时选中顶点，在物体数据属性面板中新建一个顶点组

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702020802385.png)

这样在布料中设置定点组，这样布料平面的就知道该跟着哪些顶点进行移动模拟物理效果。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702020941484.png)

### 粒子系统

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702134418580.png)

#### 粒子发射器

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702134519885.png)

#### 粒子毛发

地毯

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702142529153.png)

## 渲染



### Eevee渲染器

实时渲染(游戏 VR)

速度快，真实度欠佳

AO 环境遮蔽

辉光 镜头光晕

景深  摄影机远景虚化

次表面 配合材质

屏幕空间反射(折射)



### Cycles渲染器

CG渲染(电影 广告)

速度慢 效果真实



### 环境设置与Hdr



## 灯光

### 灯光类型

日光

点光

面光

聚光

### 灯光参数

颜色

灯光强度(能量)

形状(面光源)

灯光强度衰减

自定义距离

聚光区域(聚光灯)



## 材质

两种方式编辑材质：

1. 着色器编辑(材质)

2. 属性面板访问着色器表面属性

体积材质

VX材质库(赠送材质)设置(设置透明效果)

### 着色器编辑器面板

#### 着色器参数

基础颜色

金属度

粗糙度

折射率(需要投射配合)

Alpha

法向(法线贴图)

次表面(SSS)高光与高光颜色

各向异性(金属拉丝)(需要Cycles)

投射参数(折射)

涂层(表面一层清漆

光泽：模拟绒布边沿光反射

自发光



### UV 概念

贴图坐标：贴图如何包裹到三维模型上

1.UV展开

先期条件：

- 裁切边（标记那些边撕开这个模型）：选中边后按 Ctrl + E，标记为缝合边。
- 准备展开的面：编辑模式下点 UV，展开UV

## 动画基础

1. 时间轴与关键帧

时间轴关键帧(自动)

关键帧(手动)i

动画通道

2. 时间曲线:Ctrl+Tab

3. 案例 弹跳球

## 雕刻

### 进入雕刻模式正确姿势

手绘板

模型面数 要充足

### 基础模型准备

快速切割（Ctrl + Shift + X）

搭建基础模型

布尔

融合球

### 雕刻基本通识

增加细分修改器（雕刻之前可以应用掉）

多精度修改器（可以直接雕刻）

动态拓扑（画笔雕刻到哪里，细分就发生在哪里）

重构键网格，先 R 调整细分精度， Ctrl+R 应用细分

### 雕刻画笔的基础控制

画笔半径(大小)F

画笔力度 Shift+F

画笔角度旋转 Ctrl+F

画笔正负调整 Ctrl

平滑画笔 Shift

纹理（笔尖样式）：方形黑白图，黑色透明，白色不透明，白色作为样式。

笔画（绘画方式）：其中的曲线，需要用 Ctrl + 鼠标右键，类似 PS 的钢笔。右键调整控制手柄（可以配合 Shift 键）。

衰减（画笔硬度）

镜像雕刻（对称）

径向雕刻（某一个方向）

### 雕刻画笔分类

#### 雕刻类

**自由线（手绘）V**

锐边

粘土画笔

指推

层次

#### 松弛打平类

**松弛（平滑）Shift**

打平填充

**刮削 Shift + T**

#### 变形类

**夹捏 P**

**抓起（移动）G**

弹性

**蛇形钩 K**

姿态（调整角色四肢）

推移

旋转

#### 杂项

滑动松弛（推移布线）

边界范围（处理边界）

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702182928365.png)

布料

简化（需要开启动态拓扑）：可以不改变形状下增加细分

#### 遮罩类

遮罩可以形成一块区域，不受雕刻影响。

遮罩 M

- Ctrl + I 反转遮罩
- Alt + M 清空遮罩

遮罩提取：制作雕花手镯，紧箍圈

选区遮罩工具：套索、矩形、直线、圆形（Shift + A）

#### 面组类

绘制面组：

绘制面组后，需要在笔刷中勾选面组，这样才能限制在某个面组中进行雕刻。还可以勾选上面组边界，更加精确。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240702184434287.png)

选区面组：套索、矩形、直线、圆形

#### 多精度工具

(必须结合多精度修改器)

橡皮擦

涂抹

#### 涂色工具

绘制顶点颜色

涂抹顶点颜色

#### 模型切割

修剪工具

投影切割

#### 滤镜

整体应用某个画笔属性



## 骨骼系统

FK 父对象控制子对象，正向运动。

骨骼本质上是一大堆父子对象

骨骼里面可以使用一种 IK 技术，通过子对象控制父对象，反向运动。

搭建骨骼后，可以驱动角色的动作。

### 创建骨骼

内置骨骼

内置插件 Rigify

第三方插件 AutoRigPro

通过 Shift + A 骨架 -> 单段骨骼，创建一个骨骼。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704143612720.png)

点击骨骼，Tab 进入编辑模式，选中骨骼圆点，按E可以挤出骨骼。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704143917962.png)

接着 Ctrl + Tab 选择姿态模式

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704144037709.png)

选中子骨骼，按 Shift + I 可以创建 IK 控制器。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704144252826.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704144327366.png)

现在就可以按 G 移动子骨骼，父骨骼也会跟着移动。

骨骼有 3 种模式：物体模式、编辑模式（创建和对位）、姿态模式（主要用来做动画的）

### 编辑模式

骨骼挤出 E

骨骼扭转 Ctrl + R（比如手指头的骨骼，有不同朝向的角度），Alt + R 可以清空扭转。

扭转对齐 Shift + N

骨骼镜像：

1. 先进行左右名称命名

现在我们可以看到，骨骼分别是 001 002 003

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704150022535.png)

骨架->名称->自动左右命名

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704150100500.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704150222128.png)

2. 骨架->对称，即可镜像出右边的骨骼。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704150308522.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/image-20240704150349305.png)

### 骨骼 IK 控制器

在姿态模式下，选中某个骨骼

添加 IK：Shift + I

清除 IK：Ctrl + Alt + I

### 蒙皮权重

也就是让骨骼驱动模型。

先选择模型，再选择骨骼，接着 Ctrl + P，给模型设置父对象，选择附带自动权重。也就是模型的父对象是骨架。

原理就是让模型成为骨骼的子对象，这样控制骨骼就能控制模型了。

模型依靠顶点组，完成骨骼权重。

权重绘制：先选择骨骼，再 Shift 选择模型，就可以进入权重绘制模式。在该模式下按住 Alt 选择骨骼，按 F 可以绘制权重（像画画一样），权重越高，骨骼影响模型的形变就越大。Ctrl 可以抹掉权重。