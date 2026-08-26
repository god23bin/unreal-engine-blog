---
title: EasyAutoRig Tutorial
date: 2026/8/26 12:35:27
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png
categories:
  - Unreal Engine
tag:
  - 工具
  - 插件
published: true
---

**{% post_link plugin-doc/EasyAutoRig_DetailedGuide_en-US EasyAutoRig Detailed User Guide %}**

## 1. What Is EasyAutoRig?

EasyAutoRig is a humanoid character auto-rigging tool for Unreal Engine.

Its goal is to take a compatible **humanoid Static Mesh** and quickly generate a rigging result that follows the UE5 standard humanoid skeleton conventions, including:

- A fitted humanoid Skeleton
- Skeletal Mesh
- Automatic skin weights
- Optional Physics Asset
- UE5-style helper bones, Twist bones, and IK bones

When using EasyAutoRig, you do not need to manually create a complete skeleton in DCC software such as Blender or Maya.

The basic workflow can be summarized as:

> Import a Static Mesh → Place humanoid Landmarks → Adjust Joint Centers → Validate → Rig → Get a Skeletal Mesh

## 2. Before You Start: What Requirements Must the Model Meet?

EasyAutoRig is currently designed mainly for **standard, symmetrical humanoid characters**.

The recommended input model should meet the following requirements:

- Humanoid character
- T Pose or A Pose
- Left and right sides are approximately symmetrical
- The character faces world `+Y`
- World `+Z` is Up
- The left/right center of the body is at `X = 0`
- The main body is located near the model's local origin
- Arms and legs are not obviously crossed
- The model is not in an arbitrary pose such as sitting, running, or a combat pose

## 3. The Model Does Not Need to Be a Nude Base Mesh

The character can include:

- Clothing
- Shoes
- Hair
- Skirts
- Capes
- Tails
- Accessories
- Multiple independent Mesh Components

However, the more complex the model structure is, the fewer regions may be reliably recognized by the automatic semantic skinning system.

EasyAutoRig will choose different skinning methods based on the actual model.

Therefore:

> **Being able to Rig does not mean every model will use exactly the same automatic skinning algorithm.**

This is expected behavior.

## 4. Tutorial

### 4.1 Create an EasyAutoRig Asset

In the Content Browser, right-click and select **Animation → EasyAutoRig** to create an EasyAutoRig Asset.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261536066.png)

Rename the asset, then double-click it to open it.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261537233.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539014.png)

### 4.2 Select an A-Pose or T-Pose Static Mesh

In the Details panel, set **Source Static Mesh** to the humanoid character model you want to rig.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539791.png)

After selection, your model will appear in the viewport.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539469.png)

### 4.3 Start Placing and Adjusting Landmarks

Enable **Edit Landmarks, Landmark Names, Joint Center, Live Mirror, and Skeleton Preview** from the top toolbar.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261705336.png)

You can now start placing Landmarks. Landmarks can be placed in Perspective view, Left view, or Front view.

> Perspective view shortcut: Alt + G; Left view shortcut: Alt + K; Front view shortcut: Alt + H.

#### Place Landmarks

The yellow Landmark indicates the next Landmark that needs to be placed. In the example below, the next Landmark is `pelvis`.

Simply click the position where you want to place it. Landmarks on the center line automatically snap to the center line.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png)

After placement, the Landmark turns green. The green wireframe is a guide that shows the plane used when moving the Landmark.

Next, place `spine_01`, and continue in the same way.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540144.png)
![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540420.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541683.png)

Place `clavicle_l` on the clavicle. Because Live Mirror is enabled, the corresponding Landmark on the right side will be placed automatically.

Therefore, you only need to place the Landmarks on the left side, and the right side will be mirrored automatically.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541859.png)

Place the left arm Landmarks.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541253.png)

Place the finger Landmarks.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541954.png)
![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541314.png)

Place the leg Landmarks.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542257.png)

#### Adjust Landmarks

Switch to Front view. You may notice that some Landmark positions need adjustment.

Drag the Landmarks directly to reposition them.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542833.png)

After adjustment, the result should look similar to the image below.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542367.png)

### 4.4 Validate Rig

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542969.png)

Click **Validate Rig** to view the validation information.

If automatic skinning fails, the final fallback is to click **Skeleton Only**, then manually paint the skin weights from scratch afterward.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542718.png)

### 4.5 Click Rig

Now click the **Rig** button and wait for the rigging process to finish.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543611.png)

After completion, you can see the generated assets in the Output panel.

You can also customize the output directory.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543298.png)

## 5. Result

The model now has a UE5-style Skeletal Mesh and automatic skin weights.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543089.png)

A game-ready Physics Asset is also generated.

You can click **Simulate** to preview the physics behavior. If the result is not ideal, you usually only need to slightly adjust the position and scale of the rigid bodies. The constraints between rigid bodies generally do not need to be changed.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543682.png)
