---
title: EasyAutoRig 详细使用说明
date: 2026/8/26 12:35:28
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648830.png
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648830.png
categories:
  - Unreal Engine
tag:
  - 工具
  - 插件
published: true
---

> 如果您只是想快速完成一次绑定，可以先阅读 **{% post_link plugin-doc/EasyAutoRig使用教程 EasyAutoRig 快速入门指南 %}** 。本文则更详细地介绍 EasyAutoRig 的界面、各个标签页的作用，以及从选择模型到最终生成资产的完整使用逻辑。

## 1. EasyAutoRig 是什么？

EasyAutoRig 是一款用于 Unreal Engine 的人形角色自动绑定插件。

它可以把符合要求的 **Static Mesh 人形模型**，快速转换为可以继续在 Unreal Engine 中使用的角色绑定结果，并根据当前设置生成：

- Skeleton
- Skeletal Mesh
- 自动蒙皮权重
- 可选 Physics Asset
- UE5 风格 Twist 骨骼
- UE5 风格 IK 骨骼和辅助骨骼

您不需要先在 Blender、Maya 等 DCC 软件中手工创建完整骨架，再导入 Unreal Engine。

EasyAutoRig 的基本工作方式是：

> 选择 Static Mesh → 放置 Landmark → 调整骨骼位置 → 验证绑定 → Rig → 查看生成结果

Landmark 是整个流程中最重要的输入。它的位置会参与最终 Skeleton 的拟合，因此 Landmark 放置得越合理，后面的骨架生成、自动蒙皮和物理资产生成就越有可靠基础。

## 2. 只支持 A Pose / T Pose 的人形模型，以及朝向要求

EasyAutoRig 当前只支持 **T Pose** 和 **A Pose** 的标准人形模型。

推荐模型满足：

- 双足人形
- 左右身体基本对称
- T Pose 或 A Pose
- 角色正面朝向世界 `+Y`
- 世界 `+Z` 为上方
- 左右方向为 `X`
- 人体主体位于模型局部原点附近

也就是：

```text
+Y = Forward
+Z = Up
X  = Left / Right
```

坐姿、跑步姿势、战斗 Pose、双手交叉、单腿抬起等任意动作姿势，不属于当前正式支持的输入。

这是因为 EasyAutoRig 会利用 T Pose / A Pose 中比较稳定的人体空间关系判断左右身体、手臂、腿部、膝盖、躯干等区域。

模型可以包含衣服、鞋子、头发、裙子、披风、尾巴、饰品，也可以由多个独立 Mesh Component 组成，不要求一定是裸模。

## 3. 创建 EasyAutoRig 资产

在 Content Browser 中右键，选择「**Animation → EasyAutoRig**」，即可创建一个 EasyAutoRig 资产。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261647771.png)

创建后可以按照自己的项目命名规则重命名，例如：`EAR_CharacterName`、`AR_CharacterName`

双击该资产，就会打开 EasyAutoRig 专用编辑器。

这个资产会保存当前选择的模型、Landmark、预览状态、输出目录以及其它相关设置。一般建议一个角色对应一个 EasyAutoRig 资产，之后想重新调整时可以直接再次打开。

## 4. 细节面板

打开 EasyAutoRig 资产 后，首先可以看到右侧的细节面板。大多数情况下，真正需要修改的设置并不多。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261647289.png)

### 4.1 选择「源静态网格体」

最重要的设置是：**源静态网格体**

在这里选择您需要绑定的人形静态网格体。选择完成后，模型会立即显示在视口中。

此时建议先确认：

- 是否为 T Pose 或 A Pose
- 是否正面朝向 +Y
- 左右是否基本对称
- 人体位置是否合理

如果这些基础条件没有问题，就可以继续放置 Landmark。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261647992.png)

### 4.2 其它设置通常可以保持默认

EasyAutoRig 已经为标准 UE5 人形角色提供了一套默认设置，因此大多数情况下，其它参数都可以先不动。

如果模型是标准五指手，Hand / Finger 相关设置通常不需要修改。

如果角色手指数量不是五根，或者手部结构与标准人形不同，再根据实际模型调整手指设置即可。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648618.png)

其它「自动蒙皮、物理、输出」等设置也建议先保持默认。只有当您明确需要修改输出方式、蒙皮方式、物理资产行为或其它参数时，再进行调整。

因此第一次使用时，通常只需要：

> **选择源静态网格体，然后就可以进入标记标签页继续操作。**

## 5. Landmark 标签页

Landmark 标签页是 EasyAutoRig 最主要的编辑区域。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648568.png)

这里的按钮基本都带有 Tool Tip。把鼠标停留在按钮上，就可以看到对应功能的说明。如果不确定某个按钮是做什么的，可以先查看 Tool Tip。

### 5.1 编辑标记

开启**编辑标记**之后，就可以开始在模型上放置 Landmark。

当前下一个需要放置的位置会以黄色提示。

例如当前提示 `pelvis`，直接点击模型上 pelvis 对应的位置，就会完成该 Landmark 的放置，然后继续下一个。

### 5.2 标记名称

开启**标记名称**后，可以直接在视口中看到 Landmark 的名称。

Landmark 数量较多时，这个功能可以帮助您快速确认当前调整的是 pelvis、spine、clavicle、elbow、knee 还是其它位置。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648830.png)

### 5.3 Landmark 的位置就是主要骨骼位置

Landmark 不只是一个参考点。

它会直接参与最终 Skeleton 的拟合，因此可以简单理解为：**Landmark 放在哪里，对应的主要骨骼关节最终就会位于哪里。**

例如：

- `lowerarm` 决定肘关节位置
- `calf` 决定膝关节位置
- `hand` 决定手腕位置
- `pelvis`、`spine`、`neck` 会影响人体中轴骨骼

所以不建议只从一个角度完成全部 Landmark。可以在透视视图、正视图和左视图之间切换，从多个方向检查位置。

### 5.4 关节中心

开启**关节中心**后，EasyAutoRig 会尽量让 Landmark 从您点击到的模型表面，向当前局部体积的中心位置移动。

这对肩膀、手肘、手腕、髋部、膝盖、脚踝等关节很有帮助。

例如从正面点击膝盖表面时，真实膝关节一般并不位于最前面的模型表面，而是在腿部体积内部。Joint Center 可以帮助 Landmark 更接近这种内部关节中心。

不过，不同模型的结构差异很大。

角色可能穿着厚衣服、裙子、护甲，也可能具有特殊身体比例，因此自动计算得到的体积中心 **不一定就是视觉上和动画上最合适的位置**。

所以 Joint Center 更适合作为一个快速初始结果。如果发现某个 Landmark 不够理想，仍然需要手动调整。

### 5.5 关节编辑与移动限制平面

当需要手动移动 Landmark 时，可以在关节编辑相关设置中选择移动时限制的平面。

这样可以避免拖动时三个轴同时自由变化，导致位置难以控制。

例如：

- 从正面调整左右和上下位置时，可以限制在正面平面
- 从侧面调整前后深度时，可以切换到对应侧向平面

配合「平面辅助线」，可以更直观地看到当前编辑平面。

这种方式特别适合调整肩膀、手肘、手腕、髋部、膝盖、脚踝等。

### 5.6 实时镜像

模型左右基本对称，直接开启 Live Mirror。

调整一侧 Landmark 时，另一侧会同步更新，可以明显减少重复操作。

### 5.7 骨骼预览

开启骨骼预览后，可以直接看到当前 Landmark 对应生成的骨骼位置。

建议重点检查：

- pelvis → spine → neck → head 是否沿人体中心
- clavicle → upperarm → lowerarm → hand 是否经过肩、肘、腕
- thigh → calf → foot 是否经过髋、膝、踝

如果骨骼明显偏离真实关节，就继续调整 Landmark。

## 6. 报告标签页

当 Landmark 放置完成，并且骨骼预览看起来基本正确后，就可以点击**验证绑定**

EasyAutoRig 会对当前模型进行一次绑定前检查，并把结果显示在报告标签页中。

验证绑定的作用不是生成最终资产，而是尽量在正式 Rig 前告诉您：

- 当前模型是否可以继续绑定
- 是否存在 Blocking Error
- 是否有 Warning
- 当前会使用哪一种自动蒙皮路径
- 是否有需要绑定后重点检查的区域

### 6.1 准备就绪

如果状态是绿色的准备就绪，说明当前没有发现明显会阻止绑定的问题。

可以继续点击绑定。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648835.png)

### 6.2 Yellow / Ready, Review Warnings

如果状态是黄色，并显示类似：

> **可以绑定，请检查警告**

这不是失败。

它表示当前仍然有合法的绑定路径，只是某些区域可能使用备用方式，或者高级语义蒙皮不适用于当前模型。

例如：

```text
SemanticFull：不可用
AutoSkin Mode：GeodesicCompatibility
```

表示 EasyAutoRig 会使用 UE Geodesic Voxel 兼容蒙皮路径。

这种情况下仍然可以继续 Rig。

完成后建议根据 Report 提示，重点检查每一处关节。

### 6.3 Red / Cannot Rig

如果状态是红色，说明已经发现会阻止当前绑定流程的问题。

此时建议根据 Report 检查：

- 模型姿势
- 朝向
- Landmark
- Joint Center
- Skeleton Preview

处理完成后，再重新点击 Validate Rig。

### 6.4 Report 应该重点看什么？

正常使用时，主要关注：

- Status
- Summary
- Errors
- Warnings
- Recommendations
- AutoSkin Mode

不需要理解内部算法名称。

如果后续遇到插件内部问题，需要反馈时，再提供完整 Report 和 `LogEasyAutoRig` 即可。兜底是使用仅绑定骨骼。

## 7. 输出标签页

输出标签页用于管理和查看最终生成的资产。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648345.png)

### 7.1 设置输出目录

可以设置最终资产的生成目录。例如：`/Game/Characters/MyCharacter/`

这样 Skeleton、Skeletal Mesh 和 Physics Asset 都可以集中保存在角色自己的目录中。

### 7.2 查看生成的资产

Rig 完成后，可以在 Output 标签页中看到本次生成的资产。

通常包括：

- Skeleton
- Skeletal Mesh
- Physics Asset

如果没有开启 Physics Asset 生成，则只会生成当前设置要求的资产。

输出标签页可以帮助您快速确认资产是否成功生成、保存到了哪里，以及本次具体生成了哪些结果。

## 8. Rig 与 Skeleton Only

完成 Landmark 调整并通过「验证绑定」后，就可以执行最终绑定。

### 8.1 Rig / 绑定

点击 **Rig / 绑定**

EasyAutoRig 会开始完整绑定流程。

根据当前模型和设置，可能会执行：

- Skeleton 生成
- AutoSkin 路径选择
- 自动蒙皮权重生成
- Skeletal Mesh 生成
- Physics Asset 生成
- 最终输出验证

如果模型适合高级语义蒙皮，会使用 SemanticFull。

如果 SemanticFull 不适合，但 UE Geodesic Voxel 可以正常处理，则会使用 GeodesicCompatibility。

完成后，可以在输出标签页中看到生成结果。

### 8.2 Skeleton Only / 仅绑定骨骼

如果不需要自动权重，或者当前模型没有合适的自动蒙皮路径，可以选择 **Skeleton Only / 仅绑定骨骼**

这个功能主要用于：只利用 EasyAutoRig 自动创建 UE5 风格骨架，不依赖最终自动蒙皮结果。

之后可以在 Unreal Engine、Blender 或 Maya 中继续手动处理 Skin Weights。

如果您的目标只是快速获得 UE5 风格 Skeleton，或者本来就准备自己绘制权重，Skeleton Only 会更适合。

## 9. 推荐操作顺序

对于大多数标准人形模型，细节面板中的其它参数都可以先保持默认。

真正需要重点处理的通常只有三件事：

1. **选择正确的符合要求的静态网格体**

2. **把 Landmark 放准**

3. **根据报告决定是否继续绑定还是仅绑定骨骼。**

