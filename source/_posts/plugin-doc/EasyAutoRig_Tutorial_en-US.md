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

**{% post_link plugin-doc/EasyAutoRig_FAQ_en-US EasyAutoRig FAQ %}**

## 1. What Can EasyAutoRig Do?

EasyAutoRig rigs a **humanoid Static Mesh** in a T Pose or A Pose directly in the Unreal Engine Editor, turning it into a character that can play animations. Each rigging operation generates:

- A Skeleton fitted to your model using UE5 standard humanoid bone names and hierarchy, including twist bones and IK bones
- A Skeletal Mesh with initial automatic skin weights
- A Physics Asset (optional)

You do not need to build a skeleton manually in Blender, Maya, or another DCC application first. The workflow is:

> Create an asset → Select a model → Automatically place landmarks → Check landmarks → Validate rigging → Rig → Check the results → Manually adjust weights in UE5

### About Automatic Weights

EasyAutoRig generates **initial weights**, not production-quality weights. They help you get a character moving quickly so you can test animations and Gameplay early.

- After rigging, **you still need to adjust weights manually**, especially around the shoulders, armpits, elbows, wrists, hips/groin, knees, fingers, clothing, hair, and skirts.
- Usable weights (animations play without obvious mesh tearing) do not necessarily meet production standards.
- Topology, proportions, clothing, hair, and separate mesh parts differ between characters, so the amount of manual adjustment varies.

The good news: **you can edit weights directly in UE5**, without exporting to a DCC application. UE 5.5's Skeletal Mesh Editor includes weight editing tools by default (see Section 11).

Recommended workflow:

> **Generate a skeleton and initial weights quickly → Test animations early → Manually adjust weights in UE5 until they meet your project's requirements**

## 2. Prepare the Model

EasyAutoRig supports **standard, approximately bilaterally symmetrical bipedal humanoids**. Before starting, check that:

- The model is in a T Pose or A Pose. Sitting, running, and combat poses are unsupported; arms and legs must not cross.
- The character faces world `+Y`, with the top of the head pointing toward `+Z`.
- The body is approximately symmetrical, with its centerline at `X = 0`.
- The model was created with the character centered at the origin and the soles near `Z = 0`.

The plugin does not automatically rotate, move, or correct your model. Fix incorrect orientation or centering in a DCC application and reimport it.

The model **does not have to be an unclothed base mesh**: clothing, shoes, hair, skirts, capes, accessories, and multiple separate mesh islands are allowed. More complex structures are harder to recognize, but the plugin attempts to complete rigging and reports which regions need closer inspection.

## 3. Create an EasyAutoRig Asset

Right-click in the Content Browser and choose **Animation → EasyAutoRig**.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261536066.png)

Rename the asset (for example, `EAR_CharacterName` or `AR_CharacterName`) and double-click to open it. Generally, use one EasyAutoRig asset per character so you can reopen it for later adjustments.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261537233.png)

## 4. Select the Model

In the **Input** category of the **Details** panel, set **Source Static Mesh** to the humanoid model you want to rig.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539791.png)

The model appears in the viewport. Check that it is in a T Pose / A Pose, faces you, and is approximately symmetrical.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101619256.png)

Leave the other settings at their defaults for your first attempt, with one exception: **the character does not have standard five-finger hands** (for example, four fingers or a different number of finger segments). Before continuing, configure **Finger Count** and the bone count for each finger under **Skeleton → Left Hand / Right Hand**. If both hands match, configure the left hand and click **Copy Left Hand to Right Hand**.

## 5. Get to Know the Editor

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101623786.png)

The **toolbar** has two groups:

| Group                                               | Buttons                                                      | Purpose                                       |
| --------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------- |
| Toggles (left)                                      | Edit Landmarks, Landmark Names, Joint Center, Live Mirror, Skeleton Preview | Control landmark editing and viewport display |
| Actions (right of the separator, in workflow order) | Auto Place → Validate Rigging → Rig → Skeleton Only          | Perform the main steps in this guide          |

**Panels:**

- **Viewport:** Displays the model, landmarks, and skeleton preview. Click and drag landmarks here.
- **Landmarks:** Landmark list, placement guidance for the current point, confirmation/deletion tools, joint center tools, and hand views.
- **Report:** Validation and rigging results, and what to do next.
- **Details:** Asset settings (source model, fingers, skinning, physics).
- **Output:** Output folder and generated assets.

All buttons have tooltips. Hover over a button to read its description.

## 6. Automatically Place Landmarks

Landmarks tell the plugin where the character's joints are. **A corresponding bone joint is generated wherever you place its landmark.** Automatic placement is available starting in 1.1.0.

Click **Auto Place** on the toolbar.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101625001.png)

The plugin examines the model from the front to identify body joints, then generates a separate view for each hand to detect fingers and writes the landmarks.

1. It automatically runs validation and opens the **Report** panel, showing how many points were placed, which were preserved, and **which to check first**.
2. Enable **Edit Landmarks** on the toolbar. **Purple hollow circles** appear: these are estimated, unconfirmed points.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101628472.png)

Keep in mind:

- Auto Place only changes points that are **unplaced** or **still estimated**. Points you placed, dragged, or locked are preserved.
- The whole operation is one undo step; press `Ctrl + Z` to undo it.
- If fingers on a hand cannot be detected (for example, a fist, a mitten-like hand, or a hand holding an object), the report explains why. Place those finger landmarks manually. With **Live Mirror** enabled, a successfully detected hand can supply the result for both hands.
- If the notification says “Auto Place did not change any landmarks,” reliable detection was not possible (for example, exaggerated chibi proportions, a model not facing +Y, or an editor session unable to render the model). Follow Section 7.7 to place points manually.

## 7. Check and Adjust Landmarks

Automatic placement approximates the real joints but may not be completely accurate. Spend a few minutes checking before rigging, **starting with the points listed in the report**.

### 7.1 Enable the Editing Toggles

Enable **Edit Landmarks**, **Landmark Names**, **Joint Center**, **Live Mirror**, and **Skeleton Preview** on the toolbar.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101631060.png)

- **Edit Landmarks:** Allows click placement and dragging in the viewport.
- **Landmark Names:** Displays body-part names beside points, such as “Left Shoulder” and “Left Elbow.”
- **Joint Center:** Places points at joints inside the body rather than on its surface; dragging is constrained to a plane.
- **Live Mirror:** Edit the left side and the right follows automatically, suitable for symmetrical characters.
- **Skeleton Preview:** Shows the skeleton that will be generated from the current landmarks.

### 7.2 Understand Landmark Colors

| Viewport appearance   | Meaning                                                      |
| --------------------- | ------------------------------------------------------------ |
| Purple hollow circle  | Estimated (automatically placed or inferred), unconfirmed    |
| Green                 | Placed, joint center set                                     |
| Blue                  | Placed on the model surface, joint center not set            |
| Orange                | Next point to place manually                                 |
| Additional white ring | Currently selected point                                     |
| Translucent           | Right-side point driven by the left side with Live Mirror enabled |

The list at the bottom of the **Landmarks** panel also shows each point's status: **Not Placed**, **Estimated, Unconfirmed**, **Joint Center Set**, or **Joint Center Not Set**.

### 7.3 Check from the Front and Side

Use the view menu at the upper-left of the viewport or keyboard shortcuts. EasyAutoRig characters face `+Y`, while UE's Front / Back / Left / Right view names follow UE's own axes and do not directly correspond to the character's front and side:

| What to see                    | UE 5.5                        | UE 5.8                |
| ------------------------------ | ----------------------------- | --------------------- |
| Character front (face visible) | Right view, `Alt + Shift + K` | Left view, `Alt + K`  |
| Character side                 | Front view, `Alt + H`         | Front view, `Alt + H` |
| Perspective                    | `Alt + G`                     | `Alt + G`             |

For other engine versions, judge by what is displayed: if you see the face, you are looking at the front.

- Check height and left/right placement **from the front**.
- Check front/back depth **from the side**.

Joint points should lie **at joint centers inside the body**, not on skin or clothing. For example, place the elbow inside the arm's bending joint and the knee inside the joint between thigh and lower leg. If unsure, see EasyAutoRig: How to Place Landmarks More Effectively.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101640071.png)

### 7.4 Drag to Adjust

With **Edit Landmarks** and **Joint Center** enabled, drag points directly in the viewport. Movement is constrained to a plane; the green wireframe shows its guide.

The **Joint Center** section in the **Landmarks** panel provides finer controls:

- **View Plane / Front Plane / Side Plane:** Choose the plane used to constrain dragging.
- **Depth - / Depth +:** Move the selected point a small step backward or forward.
- **Centerline:** Align pelvis, spine, neck, and head points to the body's left/right centerline.
- **Show / Hide Plane Guide** and **Show / Hide Mesh:** Temporarily hide the model if it obscures points.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101642389.png)

### 7.5 Confirm Estimated Points

Purple estimated points behave as follows:

- They update when surrounding points move. For example, moving the pelvis or neck redistributes spine points.
- Once you drag one, it becomes your manually controlled point and stops updating automatically.

If a point looks correct after inspection, click **Confirm This Point** (selected point) or **Confirm All Estimated Points** in the **Landmarks** section of the panel. Confirmation does not move points; it stops them from following surrounding points.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101643098.png)

You can rig without confirming; the report simply reminds you to check these points.

### 7.6 Fingers: Use Hand Views

Fingers are hard to inspect in a full-body view. Version 1.1.0 adds **Hand Views**:

1. In the **Hand Views** section, click **Left Hand Back**, **Left Palm**, **Right Hand Back**, or **Right Palm**.
2. Only that hand is displayed, fingers pointing up, aligned automatically to its back or palm.
3. With **Joint Center** enabled, drag finger points along the palm plane. Click placement also hits only this hand.
4. Click **Show Full Model** to return to the full-body view.

The wrist and elbow landmarks on that side must already be placed. With **Live Mirror** enabled, adjusting the left hand is usually sufficient.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101645916.png)

### 7.7 Manual Placement (When Auto Place Fails or You Prefer to Place Points Yourself)

1. Enable **Edit Landmarks**, **Joint Center**, and **Live Mirror**.
2. The card at the top of the **Landmarks** panel shows **Next Point to Place: …**; the corresponding point is highlighted in orange in the viewport.
3. Click the appropriate position on the model, then continue to the next point.

With Live Mirror enabled, the approximate order is: pelvis → neck 1 → head → left shoulder → left elbow → left wrist → each left finger joint → left hip → left knee → left ankle → left ball of foot. Follow the panel's prompts.

You do not need to place every point: **spine, upper-neck, and clavicle points** are automatically inferred (purple) once surrounding points are placed, and the panel skips them. To correct mistakes, use **Clear Last**, **Delete Selected**, or **Reset All Landmarks** to start over.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101648268.png)

## 8. Validate Rigging

After checking landmarks, click **Validate Rigging** on the toolbar (or **Validate Landmarks** in the panel's guidance card). The result appears at the top of the **Report** panel:

| Status                         | Meaning                                            | Action                                                       |
| ------------------------------ | -------------------------------------------------- | ------------------------------------------------------------ |
| Basic Checks Passed            | No blocking issues found                           | You can rig                                                  |
| Ready to Rig — Review Warnings | Rigging is possible, but some items need attention | Read Warnings and Next Steps before deciding whether to adjust |
| Resolve Issues Before Rigging  | Blocking issues found                              | Use the Next Steps buttons, then Revalidate                  |

The **Next Steps** buttons take you directly to relevant issues. For example, **Check Left Elbow** selects that point and enables Joint Center mode; **Place Missing Landmarks** selects the first missing point.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101650385.png)

**Basic Checks Passed only means rigging can begin. It does not guarantee perfect joint positions; you must still visually inspect positions and animation results.**

## 9. Rig

Click **Rig** on the toolbar.

- Validation runs again automatically. If there are warnings, a notification lets you choose **View Report** first or **Continue** to rig immediately.
- A progress window appears. Rigging may take a few seconds to several tens of seconds, depending on polygon count.

Assets are saved to the **Output Folder** specified in the **Output** panel, defaulting to `/Game/EasyAutoRig/Generated`. Typical assets are:

- `SK_ModelName_Skeleton`: Skeleton
- `SKM_ModelName`: Skeletal Mesh
- `PHYS_ModelName`: Physics Asset

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101655897.png)

## 10. Check Rigging Results

After rigging, the **Report** panel displays a **Check Rigging Results** card with ordered steps:

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101657756.png)

1. Click **Open Rigged Model** to open the generated character in the Skeletal Mesh Editor.
2. In **Preview Scene Settings**, set **Preview Controller** to **Use Specific Animation**, then choose an animation retargeted to this skeleton.
3. Raise the arms and inspect the shoulders and armpits for obvious collapse or stretching.
4. Bend elbows and knees and check for pinching or collapse.
5. Use a fist/open-hand animation to check fingers.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543089.png)

If deformation is clearly wrong because a bone is misplaced (for example, the elbow joint is not at the arm's bending point), return to the EasyAutoRig asset, adjust landmarks, and validate and rig again. Once skeleton placement is reasonable, fix remaining deformation by manually editing weights as described below.

In the Physics Asset Editor, click **Simulate** to inspect physics. Usually only individual body positions and sizes need minor adjustments.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543682.png)

## 11. Adjust Weights in UE5

Automatic weights are initial weights and require manual adjustment after rigging. UE 5.5's Skeletal Mesh Editor includes weight editing tools by default, so you can work directly in UE5 without exporting to Blender or Maya:

1. Open the generated Skeletal Mesh (or click **Open Rigged Model** in the report).
2. Click **Editing Tools** on the toolbar, switch to **Skin**, and choose **Edit Weights**.
3. Select a bone in the bone list and paint weights using **Add**, **Replace**, **Multiply**, or **Relax**.
4. You can also select vertices and use **Mirror** (to the opposite side), **Flood** (assign throughout the selection), **Prune** (remove very small influences), or **Relax**.
5. Click **Accept** to apply changes, then save the asset.

Adjust while previewing animations, focusing on shoulders/armpits, elbows, wrists, hips/groin, knees, fingers, clothing, hair, skirts, and accessories. For symmetrical characters, edit one side first and use **Mirror** for the other.

If **Editing Tools** is missing, search for and enable **Skeletal Mesh Editing Tools** under **Edit → Plugins**, then restart the editor. UI names may vary slightly by engine version and editor language.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101700001.png)

## 12. Troubleshooting

- **Report says “Some Regions Used Basic Weights”:** A region could not be reliably identified (for example, hips beneath a skirt or a hand made from separate mesh islands). Only those regions use basic weights; the rest is rigged normally. Their weights are coarser, so prioritize manual adjustment there.
- **“Rig in Compatibility Mode” appears in the report:** Advanced automatic rigging could not complete for this model. Clicking it generates basic weights using UE Geodesic Voxel without changing your landmarks. These weights are coarser than advanced rigging; shoulders, hips, hands, and fingers require more manual adjustment.
- **You only want a skeleton:** Click **Skeleton Only** to generate a skeleton and a model asset for manual skinning, then paint weights yourself.
- **You need to report an issue:** Click **Copy Report for Support** (or **Copy Full Report** under **Diagnostics (for Technical Support)**). Send it with front/side screenshots of your model to god2333bin@gmail.com or god23bin@qq.com.

Recommended approach:

> **EasyAutoRig quickly generates a skeleton and initial weights to get your character moving. Production-quality deformation still requires manual weight adjustment in UE5.**



