---
title: EasyAutoRig 快速入门指南
date: 2026/8/26 12:35:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png
categories:
  - Unreal Engine
tag:
  - 工具
  - 插件
published: true
---

**{% post_link plugin-doc/EasyAutoRig_Tutorial_ja-JP EasyAutoRig 使用チュートリアル %}** | **{% post_link plugin-doc/EasyAutoRig_Tutorial_en-US EasyAutoRig Tutorial %}**

**{% post_link plugin-doc/EasyAutoRig_DetailedGuide_zh-CN EasyAutoRig 详细使用说明 %}**

**{% post_link plugin-doc/EasyAutoRig_FAQ_zh-CN EasyAutoRig 常见问题 %}**

## 1. EasyAutoRig 是什么？

EasyAutoRig 是一款用于 Unreal Engine 的人形角色自动绑定工具。
它的目标是把一个符合要求的 **Static Mesh 人形角色**，快速生成一套与 UE5 标准人形骨架约定兼容的绑定结果，包括：

- 拟合后的人形 Skeleton
- Skeletal Mesh
- 自动蒙皮权重
- 可选 Physics Asset
- UE5 标准风格的辅助骨骼、Twist 骨骼与 IK 骨骼

使用时，你不需要在 Blender、Maya 等 DCC 软件中手动创建完整骨架。

基本流程可以概括为：

> 导入静态模型 → 放置人体标记 → 调整关节中心 → 验证 → Rig → 得到 Skeletal Mesh

### 1.1 EasyAutoRig 的定位：帮你更快完成绑定，而不是替代所有手工调整

在开始之前，有一点需要先说明：

> **EasyAutoRig 并不是一款承诺“一键生成完美生产级权重”的自动蒙皮工具。**

自动绑定和自动蒙皮更适合被理解为一个**高质量的起点**。

EasyAutoRig 希望帮你省掉大量重复且耗时的工作，例如：

- 从零搭建 UE5 风格的人形骨架
- 设置 Twist、IK 和辅助骨骼
- 完成一套初始蒙皮权重
- 生成 Physics Asset
- 在真正绑定之前检查模型是否适合当前流程

这样你可以更快地让一个 Static Mesh 角色进入 Unreal Engine 的动画测试和 Gameplay 原型阶段，而不是先把大量时间花在基础绑定工作上。

不同角色的拓扑、身体比例、衣服、头发、裙子和分离组件都可能不同，因此自动权重的最终质量也会不同。

有些模型生成后的权重已经可以满足原型和普通动画测试；有些模型则可能需要继续微调肩膀、手肘、髋部、膝盖、手指、衣物等区域。

所以更推荐把 EasyAutoRig 的工作流程理解为：

> **快速完成骨架与初始蒙皮 → 尽快测试动画和游戏效果 → 再针对真正有问题的区域做少量手工调整**

而不是：

> **点击一次按钮 → 所有模型都得到完全不需要检查的最终权重**

如果你的项目对角色变形质量要求较高，完成 Rig 后仍然建议使用实际动画测试角色，并根据需要继续调整 Skin Weights。

## 2. 使用前：模型需要满足什么条件？

EasyAutoRig 当前主要面向**标准对称人形角色**。
推荐输入模型满足以下条件：

- 人形角色
- T Pose 或 A Pose
- 左右身体基本对称
- 角色正面朝向世界 `+Y`
- 世界 `+Z` 为上方
- 身体左右中心位于 `X = 0`
- 人体主体位于模型局部原点附近
- 手臂和腿没有明显交叉
- 不是坐姿、跑步姿势、战斗动作等任意 Pose

## 3. 模型不需要是裸模

角色可以包含：

- 衣服
- 鞋子
- 头发
- 裙子
- 披风
- 尾巴
- 饰品
- 多个独立 Mesh Component

但模型结构越复杂，自动语义蒙皮能够识别的区域就越少。
EasyAutoRig 会根据模型实际情况选择不同的蒙皮方式。
因此：

> **可以 Rig，不代表所有模型最终都会使用完全相同的自动蒙皮算法。**

这是正常现象。

## 4. 使用教程

### 4.1 创建 EasyAutoRig 资产

在内容浏览器中右键，选择「动画->EasyAutoRig」，即可创建 EasyAutoRig 资产；

![创建 EasyAutoRig 资产](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261536066.png)

重命名该资产，完成后双击打开。

![重命名该资产](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261537233.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539014.png)

### 4.2 选择 A-Pose 或者 T-Pose 的静态网格体

在细节面板中，设置**源静态网格体**为你需要绑定的人形角色模型。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539791.png)

选择完成之后，你的模型会出现在视口中。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539469.png)

### 4.3 开始放置标记并调整

一次性开启顶部工具栏的「编辑标记、标记名称、关节中心、实时镜像、骨骼预览」。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261705336.png)

现在可以开始放置标记了。可以在透视视图下放置标记，也可以在左视图和正视图下放置标记。

> 透视视图快捷键是 Alt + G；左视图快捷键是 Alt + K；正视图快捷键是 Alt + H；

#### 放置标记

黄色的标记表示当前下一个需要放置的标记，如下图所示下一个需要放置的是 pelvis 标记。直接鼠标点击你需要放置的位置即可，中轴线的标记自动吸附中轴线。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png)

放置完成后变为绿色标记，绿色线框是辅助线，可以让你知道移动标志时所在的平面。接下来放置 spine_01，以此类推。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540144.png)
![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540420.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541683.png)

clavicle_l 放置在锁骨，此时右边的也会同步放置，因为开启了实时镜像。所以只需放置左边的标记即可，右边自动同步。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541859.png)

放置左手臂标记。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541253.png)

放置手指标记。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541954.png)
![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541314.png)

放置腿部标记。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542257.png)

#### 调整标记

在正视图查看。可以看到有些标记位置是需要调整的。直接拖动标记进行调整。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542833.png)

调整后如下图所示。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542367.png)

### 4.4 验证绑定

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542969.png)

可以点击验证绑定，查看一些信息。如果自动蒙皮失败，最终兜底方案是直接点击「仅绑定骨骼」，后续手动从零开始绘制权重。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542718.png)

### 4.5 点击绑定

现在可以直接点击「绑定」按钮，等待绑定结果。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543611.png)

完成后可以在输出面板中看到生成的资产。你也可以自定义输出的目录。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543298.png)

## 5. 结果

该模型拥有 UE5 风格的骨骼网格体和自动权重。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543089.png)

接下来不要只确认「Rig 成功」，还建议给角色播放几组实际动画，重点观察：

- 抬手时肩膀是否自然
- 弯曲手臂时手肘是否正常
- 抬腿时髋部是否出现明显塌陷
- 弯曲腿部时膝盖是否正常
- 手指、衣服、头发等特殊区域是否需要进一步调整

如果这些区域已经满足当前项目需求，可以直接继续使用。

如果某些位置的变形不够理想，就把自动权重作为起点，只修正真正有问题的区域。这样通常仍然比从零开始搭骨架和绘制整套权重要节省大量时间。

EasyAutoRig 还会生成一套适合作为游戏开发起点的 Physics Asset。

可以点击「模拟」查看物理效果。如果效果不理想，可以根据角色体型微调刚体的位置和缩放，并根据项目实际需求继续测试。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543682.png)

最终推荐的思路是：

> **EasyAutoRig 帮你快速完成 0 → 1，把角色尽快放进游戏里跑起来；最终需要多高的变形质量，再根据项目需求继续精修。**