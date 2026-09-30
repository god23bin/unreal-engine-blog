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

其实在使用 EasyAutoRig 的使用，最重要的操作就是 Landmark （标记）的放置，简单来说，您放置的标记就是最终的骨骼。

> **{% post_link plugin-doc/EasyAutoRig_DetailedGuide_zh-CN EasyAutoRig 详细使用说明 %}**
>
> **{% post_link plugin-doc/EasyAutoRig_FAQ_zh-CN EasyAutoRig 常见问题 %}**

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

如果计算有误差，可以手动调整。在标记面板中通过限制 Landmark 的移动平面来拖拽调整 Landmark 所在的位置。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326339.png)

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