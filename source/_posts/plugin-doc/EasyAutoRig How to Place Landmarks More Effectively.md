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

> **{% post_link plugin-doc/EasyAutoRig_DetailedGuide_en-US EasyAutoRig Detailed User Guide %}**
>
> **{% post_link plugin-doc/EasyAutoRig_FAQ_en-US EasyAutoRig FAQ %}**

## So, how can you place body Landmarks more accurately?

Before learning how to place body Landmarks more effectively, there is one important principle in 3D character rigging that you should understand: **try to keep the bones as close as possible to the volumetric center of the character's body**.

You should also understand what the standard UE5 skeleton looks like visually.

The standard UE5 skeleton is shown below:

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801943.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801689.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801738.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png)

As you can see, the neck is controlled by neck_01 and neck_02. Their positions are shown in the image below. In the following images, the green line indicates a cross-section of the reference position. On your own character, these two bones should also be placed at the corresponding locations.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302233314.png)

The chest area is mainly controlled by spine_04, with most of the weights concentrated around the chest region where spine_04 and spine_05 are located.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302236403.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325077.png)

The waist is mainly controlled by spine_01 through spine_03. This area is controlled more precisely, so the spacing between these bones is relatively small.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325498.png)

The shoulder bone, clavicle, is mainly positioned around the collarbone.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325130.png)

upperarm is positioned around the shoulder joint of the body (the green box indicates the relevant area).

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325016.png)

lowerarm is positioned around the elbow joint.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325413.png)

hand is positioned around the wrist.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325628.png)

pelvis is positioned around the human hip joint (the buttocks/hip area).

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325022.png)

Next to it is thigh, located at the root of the upper leg.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325967.png)

Then calf is positioned around the knee and controls the lower leg.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325210.png)

foot is positioned around the ankle.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326792.png)

ball is positioned around the ball of the foot.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326912.png)

## The Difference Between Bone and Joint

**There are two concepts you should pay attention to: Bone and Joint. If you are not familiar with 3D modeling and rigging, or if you are only familiar with Blender, this part may be confusing. A simple way to understand it is that, in UE, a Bone is visually represented by a sphere. When creating it in UE, that point is referred to as a Joint, meaning the position of the actual joint. The cone-shaped segment you see between two Joints can be understood as a visual connection drawn to imitate the appearance of a traditional bone. In common usage, each Joint is often referred to as a Bone as well. The position of that sphere is effectively a pivot point. UE uses a joint-based system: what matters is the position of the joint, rather than a bone segment with a physical length.**

**The same principle applies when placing Landmarks. Of course, this is not an absolute rule because every model has different body proportions. The goal is simply to follow the position and overall direction of the standard UE5 skeleton as closely as possible. In other words, try to place each Landmark at a reasonable anatomical joint position on your own model.**

**For an unclothed base body, I use UE Manny as the example. The Landmark placement is shown below:**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326524.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326285.png)

**Remember to enable "Joint Center" so that Landmarks can be placed at the volumetric center of the body.**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326402.png)

If there is any calculation error, you can adjust the Landmark manually. In the Landmark panel, constrain the Landmark's movement plane, then drag it to fine-tune its position.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326339.png)

## Placement Examples

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