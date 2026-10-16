---
title: EasyAutoRig 如何更好的放置人体标记呢？
date: 2026/9/29 18:00:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png
categories:
  - Unreal Engine
tag:
  - 工具
  - 插件
published: true
---

> **{% post_link plugin-doc/EasyAutoRig_DetailedGuide_zh-CN EasyAutoRig 详细使用说明 %}**
>
> **{% post_link plugin-doc/EasyAutoRig_FAQ_zh-CN EasyAutoRig 常见问题 %}**

在使用 EasyAutoRig 时，最重要的操作就是 Landmark（标记点）的放置。简单来说，您放置的标记点就是最终的骨骼关节。

> **1.1.0 提示**：现在可以先点击工具栏的「自动放置」，让插件自动放好身体和手指的标记点，再按本文的标准逐个检查和调整，尤其是「报告」中“请优先检查”的点。脊柱、上颈部和锁骨的点会根据周围的点自动推算；手指可以使用「标记」面板的「手部视图」单独查看。

## 所以如何更好的放置人体标记呢？

想要了解如何更好的放置人体标记之前，需要了解 3D 模型绑定中的一个重要原则：**尽量让骨骼贴近角色身体体积的中心位置**。

同时需要了解 UE5 标准骨架在视觉上是怎样的。

UE5 标准骨架如下图所示：

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801943.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801689.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801738.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png)

可以看到脖子由 neck_01 和 neck_02 进行控制，所在位置如下图所示，后续的绿色线段，是我们参考的位置的横截面，您的角色也应该在相对应的位置放置这两个骨骼；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302233314.png)

胸腔这部分主要由 spine_04 控制，权重主要落在 spine_04 与 spine_05 的所在胸腔区域；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302236403.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325077.png)

腰部主要就是 spine_01 到 spine_03，这部分控制的比较精细，骨骼之间的间距较小；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325498.png)

肩膀的骨骼 clavicle 主要在锁骨所在的位置；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325130.png)

upperarm 则是在人体肩关节这部分（绿色方框表示所在位置）；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325016.png)

lowerarm 则是在人体的肘关节这部分；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325413.png)

hand 则是在手腕这里；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325628.png)

pelvis 就是人体髋关节（臀部）所在位置；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325022.png)

旁边则是 thigh 大腿，也就是大腿的根部；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325967.png)

接着是 calf 在膝盖的位置上，控制小腿；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325210.png)

foot 位于脚踝位置；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326792.png)

ball 位于脚掌；

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326912.png)

## Bone 和 Joint 的区别

**需要注意两个概念 Bone 和 Joint，对于不熟悉 3D 建模和 3D 绑定的朋友们来说，或者只熟悉 Blender 的朋友们来说，会对这部分有所困扰，简单理解，在 UE 中，一个 Bone 的可视化体现是一个球体；在 UE 中创建时会称为 Joint，也就是关节所在的位置。而您看到的两个 Joint 之间出现的锥体，可以理解为模仿传统骨骼外观而绘制出来的视觉连线。目前习惯上对每一个 Joint 都称为 Bone，这个球体所在的位置就是一个枢轴点。UE 是  Joint Base System，关心的是关节所在的位置，而不是一段有长度的骨骼。**

**所以我们放置的 Landmark 也理应如此；当然不是说绝对的，因为模型体型各异，只能说尽可能靠近 UE5 标准骨架的位置走向。换句话说，尽可能让您的 Landmark 放置在您的模型上合理的关节位置上。**

**纯裸模我这里使用 UE Manny 作为演示，放置后如下图所示：**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326524.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326285.png)

**记得开启「关节中心」，这样放置 Landmark 能够放置到体积中心。**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326402.png)

如果计算有误差，可以手动调整。在「标记」面板的「关节中心」分区中选择「正面平面」或「侧面平面」限制 Landmark 的移动平面，再拖拽调整 Landmark 所在的位置。也可以用「深度 -」「深度 +」微调前后深度。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326339.png)

## 从正面和侧面检查

每个点都至少要从两个方向看：**从角色正面检查高度和左右位置，从角色侧面检查前后深度。**

注意：EasyAutoRig 的角色面向 `+Y`，而 UE 视图菜单的“前 / 后 / 左 / 右”是按 UE 自己的坐标轴命名的，和角色方向不一致：

| 想看                 | UE 5.5                                 | UE 5.8                         |
| -------------------- | -------------------------------------- | ------------------------------ |
| 角色正面（能看到脸） | 「右（Right）」视图，`Alt + Shift + K` | 「左（Left）」视图，`Alt + K`  |
| 角色侧面             | 「前（Front）」视图，`Alt + H`         | 「前（Front）」视图，`Alt + H` |

其他版本以画面为准：能看到角色的脸就是正面。

## 手指标记点

每根手指的第一个点放在**手指与手掌连接的关节**处，其余的点沿指尖方向依次放在手指**弯曲的关节**处，都要在手指内部，不要放在指尖。

手指很小，建议使用「标记」面板的「手部视图」：点击「左手手背」或「左手手掌」，视口只显示这只手，手指朝上。这时单击只会落在这只手上，开启「关节中心」后拖动会沿手掌平面进行。手背视图看手指的左右分布，再切到侧面检查深度（手指点应在手指厚度的中间）。检查完点击「显示完整模型」返回。

## 自动放置后重点检查什么

自动放置的点已经接近关节，但下面这些情况最值得再看一眼：

- 「报告」中“请优先检查”列出的点：左右检测不一致的点、按颈部推算高度的头部点、深度为推测值的点；
- 肩（upperarm）：从侧面检查是否在肩关节内部，而不是肩部表面或上臂中段；
- 髋（thigh）：穿裙子、外套时，确认在大腿根部的关节内，而不是裙子上；
- 手腕（hand）：手里拿着道具时，确认在前臂与手掌之间；
- 脚踝（foot）：穿长靴时，确认在小腿与脚之间的关节内；
- 手指：报告提示手指未放置，或手指点看起来偏离关节时，用手部视图调整。

检查后觉得合适，可以在「标记」面板中点击「确认此点」或「确认全部估算点」。

## 放置示例

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801206.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801837.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801300.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326027.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801508.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801174.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801445.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326265.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801436.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326451.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801290.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801536.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801152.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302327511.png)