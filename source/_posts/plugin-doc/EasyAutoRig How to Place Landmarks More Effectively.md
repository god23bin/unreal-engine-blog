---
title: How should you place the body Landmarks more accurately？
date: 2026/9/29 18:00:26
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png
categories:
  - Unreal Engine
tag:
  - 工具
  - 插件
published: true
---

When using EasyAutoRig, the most important operation is placing the Landmarks. Simply put, the Landmarks you place determine the final bone positions.

## So, how should you place the body Landmarks more accurately?

Before learning how to place body Landmarks more effectively, it helps to first understand what the standard UE5 skeleton looks like visually.

The standard UE5 skeleton is shown below:

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801943.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801689.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801738.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png)

As you can see, the neck is controlled by neck_01 and neck_02.

The chest area is mainly controlled by spine_04, with most of the weights concentrated around the chest region between spine_04 and spine_05. The waist is mainly controlled by spine_01 through spine_03. This area is controlled more precisely, so the spacing between these bones is relatively small. These spine bones are also generally positioned near the volumetric center of the mesh.

The shoulder bone, clavicle, is mainly positioned around the collarbone. upperarm is positioned around the shoulder joint, lowerarm is positioned around the elbow joint, and hand is positioned around the wrist.

pelvis is positioned around the human hip joint (the buttocks/hip area). Next to it is thigh, located at the root of the upper leg. Then calf is positioned around the knee and controls the lower leg. foot is positioned around the ankle, while ball is positioned around the ball of the foot.

These bones are generally located near the volumetric center of the body.

Therefore, the Landmarks we place should follow the same principle. Of course, this is not an absolute rule, because every character has different body proportions. The goal is to make the Landmark placement follow the position and overall direction of the standard UE5 skeleton as closely as possible.

**For an unclothed base body, I use UE Manny as the example. The Landmark placement is shown below:**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291844839.png)

## Placement Examples

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
