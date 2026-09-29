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

## 所以如何更好的放置人体标记呢？

想要了解如何更好的放置人体标记之前，就需要了解 UE5 标准骨架在视觉上是怎样的。

UE5 标准骨架如下图所示：

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801943.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801689.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801738.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png)

可以看到脖子由 neck_01 和 neck_02 进行控制；

胸腔这部分主要由 spine_04 控制，权重主要落在 spine_04 与 spine_05 之间的胸腔区域；腰部主要就是 spine_01 到 spine_03，这部分控制的比较精细，骨骼之间的间距较小；这些 spine 骨骼也是基本位于几何体的体积中心；

肩膀的骨骼 clavicle 主要在锁骨所在的位置；upperarm 则是在人体肩关节这部分；lowerarm 则是在人体的肘关节这部分；hand 则是在手腕这里；

pelvis 就是人体髋关节（臀部）所在位置；旁边则是 thigh 大腿，也就是大腿的根部；接着是 calf 在膝盖的位置上，控制小腿；foot 位于脚踝位置；ball 位于脚掌；

这些骨骼基本都处于体积中心；

所以我们放置的 Landmark 也理应如此；当然不是说绝对的，因为模型体型各异，只能说尽可能靠近 UE5 标准骨架的位置走向。

**纯裸模我这里使用 UE Manny 作为演示，放置后如下图所示：**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291844839.png)

## 放置示例

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801206.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801837.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801300.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801508.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801174.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801445.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801436.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801290.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801536.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801152.png)











































