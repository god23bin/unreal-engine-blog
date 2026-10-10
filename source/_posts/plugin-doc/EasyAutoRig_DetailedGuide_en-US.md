---
title: EasyAutoRig Detailed User Guide
date: 2026/8/26 12:35:30
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648830.png
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648830.png
categories:
  - Unreal Engine
tag:
  - 工具
  - 插件
published: true
---

> If you only want to complete your first rig quickly, you can start with the **{% post_link plugin-doc/EasyAutoRig_Tutorial_en-US Quick Start Guide %}** . This guide provides a more detailed introduction to the EasyAutoRig interface, the purpose of each tab, and the complete workflow from selecting a model to generating the final assets.

## 1. What Is EasyAutoRig?

EasyAutoRig is an automatic humanoid rigging plugin for Unreal Engine. It rigs a suitable **humanoid Static Mesh** directly in the editor and generates the following according to your settings:

- A Skeleton fitted to your model using UE5 standard humanoid bone names, hierarchy, and reference orientations
- UE5-style twist bones and IK bones
- A Skeletal Mesh with initial automatic skin weights
- A Physics Asset (optional)

> Automatic weights are **initial weights**, not production-quality weights. Manual adjustment is still required after rigging and can be done directly in UE5 (Section 14).

Basic workflow:

> Select a model → Automatically (or manually) place landmarks → Check and adjust → Validate rigging → Rig → Check the results → Manually adjust weights in UE5

**Landmarks** are the most important input: their positions determine the final bone-joint positions and guide automatic skinning's identification of body regions. Well-placed landmarks provide a more reliable foundation for the skeleton, skinning, and physics assets.

## 2. Input Model Requirements

EasyAutoRig supports only **standard bipedal humanoids**, with these requirements:

- T Pose or A Pose
- Approximately symmetrical body
- Character centered at the origin during modeling, soles near `Z = 0`
- Orientation following these conventions:

```text
+Y = Forward (character front)
+Z = Up (top of the head)
X  = Left / Right (body centerline at X = 0)
```

Sitting, running, combat, crossed arms, a raised leg, and other action poses are unsupported. The plugin relies on stable spatial relationships in T Pose / A Pose to identify left/right, arms, legs, knees, torso, and other regions.

The plugin **does not** automatically rotate, move, scale, or correct the model. Validation reports errors or warnings for clearly incorrect orientation or centering. Correct these in a DCC application and reimport.

Clothing, shoes, hair, skirts, capes, tails, accessories, and multiple separate mesh islands are allowed. An unclothed base mesh is not required.

## 3. Create an EasyAutoRig Asset

Right-click in the Content Browser and choose **Animation → EasyAutoRig**.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261647771.png)

Rename it according to your project's conventions, for example `EAR_CharacterName`. Double-click to open the EasyAutoRig Editor.

The asset stores the selected model, landmarks, editing toggle states, output folder, latest report, and other settings. Use one asset per character so you can reopen it for later adjustments.

## 4. Editor Layout

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101623786.png)

### 4.1 Toolbar

A separator divides the toolbar into two groups.

**Toggles** (enable or disable at any time; states are saved in the asset):

| Button           | Purpose                                                      |
| ---------------- | ------------------------------------------------------------ |
| Edit Landmarks   | Place and drag landmarks in the viewport. When disabled, viewing only. |
| Landmark Names   | Display the body-part name beside each point.                |
| Joint Center     | Joint Center mode: clicking and dragging places landmarks inside the body rather than on the surface. |
| Live Mirror      | Right-side points follow corresponding left-side edits automatically. |
| Skeleton Preview | Display the skeleton that will be generated from the current landmarks. |

**Actions** (in workflow order):

| Button           | Purpose                                                      |
| ---------------- | ------------------------------------------------------------ |
| Auto Place       | Automatically place body and finger landmarks from model views (Section 7). |
| Validate Rigging | Check whether rigging can begin and list issues in Report (Section 10). |
| Rig              | Generate a skeleton and automatically rig the model to it (Section 12). |
| Skeleton Only    | Generate a skeleton and model asset for manual skinning, without automatic weights (Section 12.4). |

### 4.2 Panels

| Panel                  | Contents                                                     |
| ---------------------- | ------------------------------------------------------------ |
| Viewport               | Model, landmarks, skeleton preview, plane guides             |
| Details                | Source model, skeleton/fingers, automatic skinning, physics settings |
| Preview Scene Settings | Standard UE preview scene settings, such as lighting and environment |
| Landmarks              | Placement guidance, landmark tools, hand views, landmark list |
| Report                 | Validation/rigging results, automatic placement results, next steps |
| Output                 | Output folder and generated assets                           |

Most buttons have tooltips. For disabled buttons, the tooltip also explains why.

## 5. Details Panel

The **Details** panel is on the right when an EasyAutoRig asset is opened. Usually, few settings need changing.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101704593.png)

### 5.1 Input: Source Static Mesh

The most important setting is **Source Static Mesh** under **Input**. Select the humanoid Static Mesh you want to rig; it immediately appears in the viewport.

First check:

- T Pose or A Pose
- Facing +Y
- Approximately symmetrical
- Body positioned near the origin

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261647992.png)

### 5.2 Skeleton: Finger Settings

For standard five-finger hands with three segments per finger, leave the **Skeleton** finger settings unchanged.

If finger count or segment count differs, configure them **before placing landmarks**:

- **Finger Count** under **Left Hand** and **Right Hand** (0–5)
- **Default Bones per Finger**, plus individual counts for thumb, index, middle, ring, and little finger (1–5)
- For matching hands, configure the left and click **Copy Left Hand to Right Hand** in the **Hand Settings** row

These settings determine which finger landmarks are required and which Auto Place generates.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648618.png)

The same category includes **Generate Twist Bones**, **Generate IK Bones**, and **Skeleton Preview Line Thickness**. Normally, leave them at their defaults.

### 5.3 Automatic Skinning

The **Automatic Skinning** category indicates whether you are using **Recommended Defaults** or **Custom Basic Weight Settings**. Click **Reset to Recommended** to restore defaults after changes.

- **Max Bone Influences:** Maximum number of bones influencing a vertex; default 4.
- **Basic Weight Quality (Advanced):** Solver and smoothing parameters for basic weights; usually no changes are needed.

Use defaults initially and change them only when you have a specific reason to adjust results.

### 5.4 Physics

**Generate Physics Asset** is enabled by default. Disabling it generates only the Skeleton and Skeletal Mesh during rigging. Parameters under **Legacy UE Auto** are retained for older-asset compatibility; current physics asset generation does not use them.

## 6. Viewport and Viewing Directions

Check landmarks from multiple directions: **height and left/right position from the character's front, and front/back depth from the character's side**. Use the view menu at the upper-left of the viewport or UE keyboard shortcuts.

EasyAutoRig characters face `+Y`. UE's Front / Back / Left / Right view names follow UE's own axes and do not directly correspond to the character's front and side. Plugin guidance therefore says “view from the character's front/side,” rather than using UE view names.

| What to see                    | UE 5.5                        | UE 5.8                |
| ------------------------------ | ----------------------------- | --------------------- |
| Character front (face visible) | Right view, `Alt + Shift + K` | Left view, `Alt + K`  |
| Character side                 | Front view, `Alt + H`         | Front view, `Alt + H` |
| Perspective                    | `Alt + G`                     | `Alt + G`             |

For other engine versions, judge by the displayed image: seeing the character's face means you are viewing the front.

## 7. Auto Place

### 7.1 What Auto Place Does

After clicking **Auto Place** on the toolbar, the plugin:

2. Writes 17 main body points, then infers spine, upper-neck, and clavicle points using UE5 Manny skeleton proportions, giving 25 body points in total.
3. Generates a separate hand view aligned to each palm, detects fingers using the hand landmark model, and writes finger landmarks.
4. Runs validation automatically, opens **Report**, and displays “Auto Place complete: N landmarks estimated.”

All points written by Auto Place are **estimated points**, displayed as purple hollow circles and listed as **Estimated, Unconfirmed**.

### 7.2 Which Points Are Changed

- Only **unplaced** or **still estimated**, **unlocked** points are changed.
- Points you placed, dragged, or locked are preserved and listed as “Preserved” in the report.
- With Live Mirror enabled, only left-side and centerline points are written; the right follows the left. Otherwise, both sides are written independently.
- The entire operation is one undo step (`Ctrl + Z`). If no points change, no undo step is created and the asset is not marked modified.

You can run it repeatedly—for example, place a few key points yourself, then fill in the rest automatically.

### 7.3 Auto Place Section in the Report

After placement, an **Auto Place** section appears at the top of **Report**. Possible entries:

| Entry                                                        | Meaning                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Automatically placed N landmarks                             | Remain estimated until moved or confirmed.                   |
| Preserved landmarks you placed or locked: …                  | These points were not changed.                               |
| Check first: … (left/right results differ)                   | Detection disagreed between sides; one side's result was used for both. |
| Check first: … (ears not found; height estimated from neck)  | Head-point height was inferred.                              |
| Check first: … (model surface not found / finger thickness could not be measured; depth estimated) | Front/back depth is an estimate; inspect from the side.      |
| Left (right) finger landmarks not placed: reason             | Place this hand's finger points manually; see reasons below. |
| Left fingers could not be placed; right-hand results used for both hands | With Live Mirror enabled, the successfully detected hand supplies the other side. |
| N required landmarks remain unplaced                         | Place these manually.                                        |

Common reasons finger points are not placed:

- Wrist or elbow landmarks have not been placed.
- The hand cannot be isolated from the rest of the model.
- Fingers cannot be recognized: for example, a fist, mitten-like hand, or hand holding an object.
- Some finger landmarks fall outside the hand.
- The hand detection model cannot be loaded (NNERuntimeORT must be enabled).

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101712900.png)

### 7.4 When Auto Place Fails

If “Auto Place did not change any landmarks” appears, the asset is unchanged. The subtitle explains why:

| Reason                                                       | Action                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Specify a Source Static Mesh first                           | Select a model in Details.                                   |
| Current editor session cannot render the model (for example, no GPU) | Place manually.                                              |
| Body detection model cannot be loaded                        | Ensure NNERuntimeORT is enabled (a plugin dependency enabled by default), then retry. |
| Model cannot be viewed from the front                        | Check +Y forward, +Z up, and soles at Z = 0.                 |
| No body found in the model's front view / body could not be reliably detected | For example, heavily stylized proportions; place manually.   |

## 8. Landmarks Panel

The **Landmarks** panel contains all placement and adjustment tools.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101713304.png)

### 8.1 Guidance Card

The top card adapts to the current state:

- **Title:** **Next Point to Place: …** when points are missing, **Selected: …** when a point is selected, or **Check Joint Landmarks** when all are placed.
- **Status:** Placement progress of the current point.
- **Placement guidance:** Recommended body position; for an elbow, “Place inside the bending joint between upper arm and forearm; check height from the front and depth from the side.”
- **Operation hints:** For example, “Click the model to place…” or “Drag to adjust, or click Confirm This Point.”
- **Validate Landmarks:** Same operation as the toolbar's **Validate Rigging**.

### 8.2 Placement and Display

Four checkboxes match toolbar toggles: **Edit Landmarks**, **Joint Center**, **Live Mirror**, and **Landmark Names**, allowing direct control from the panel.

### 8.3 Landmarks

| Button                       | Purpose                                                      |
| ---------------------------- | ------------------------------------------------------------ |
| Confirm This Point           | Keep the selected estimated point at its current position; stop automatic updates from surrounding points. |
| Confirm All Estimated Points | Confirm all estimated points. Check from front and side first. |
| Clear Last                   | Clear the most recently placed unlocked landmark.            |
| Delete Selected              | Clear the selected landmark's placement data.                |
| Mirror Once                  | Copy placed left-side points to empty, unlocked right-side points when Live Mirror is disabled. |
| Reset All Landmarks          | Clear all points, including locked ones. Requires confirmation and can be undone. |

Hover over disabled buttons to see why. For example, inferred points cannot be deleted while the inputs needed to infer them still exist (they would immediately be inferred again). Move surrounding points or drag the inferred point itself instead.

### 8.4 Joint Center

| Button                                | Purpose                                                      |
| ------------------------------------- | ------------------------------------------------------------ |
| Depth - / Depth +                     | Move the selected joint center one step backward/forward.    |
| Centerline                            | Align the selected point to the body's left/right centerline. For pelvis, spine, neck, and head, not arm/leg joints. |
| View Plane / Front Plane / Side Plane | Constrain dragging to the current view plane, character-front plane, or character-side plane. |
| Show / Hide Plane Guide               | Show or hide the current dragging plane guide (green viewport wireframe). |
| Show / Hide Mesh                      | Temporarily hide the model while editing joint centers to see obscured landmarks and bones. |

Button labels describe the action clicking will perform. For example, **Hide Mesh** means the model is currently visible.

### 8.5 Hand Views

For placing and inspecting finger landmarks:

- **Left Hand Back / Left Palm / Right Hand Back / Right Palm:** Show only that hand, fingers up, viewed from the back or palm, and frame it.
- Click placement hits only that hand, avoiding a thigh in front of the palm. In Joint Center mode, dragging follows the palm plane.
- **Show Full Model:** Exit hand view, restore and frame the full model.
- Wrist and elbow landmarks on that side must already be placed; otherwise the buttons are disabled.
- Switching views does not change landmarks or asset data. Clicking a report's “Check …” action also automatically exits hand view.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101645916.png)

### 8.6 Last Operation

Shows the latest landmark action result, such as “Confirmed 5 estimated landmarks” or “Adjusted left elbow landmark depth.” Failed or unchanged operations are also reported accurately.

### 8.7 Landmark List

| Column             | Contents                                                     |
| ------------------ | ------------------------------------------------------------ |
| Body Part          | Readable name, such as Left Shoulder or Left Index Finger Joint 2 |
| Requirement        | Required or Optional                                         |
| Placement Progress | Not Placed; Estimated, Unconfirmed; Joint Center Set; Joint Center Not Set |

Click a row to select its point. **Joint Center Set** only means center data exists, not that its position is accurate. Visual inspection is still required.

## 9. Landmark Placement and Adjustment

### 9.1 Landmarks Are Bone Joints

Landmarks directly participate in skeleton fitting: **the corresponding bone joint is generated wherever its landmark is placed**. For example:

- Left elbow (`lowerarm_l`) determines the elbow position.
- Left knee (`calf_l`) determines the knee position.
- Left wrist (`hand_l`) determines the wrist position.
- Pelvis, spine, and neck determine the central body bones.

See EasyAutoRig: How to Place Landmarks More Effectively for recommended positions.

### 9.2 Landmark Appearance in the Viewport

| Appearance            | Meaning                                           |
| --------------------- | ------------------------------------------------- |
| Purple hollow circle  | Estimated, unconfirmed                            |
| Green                 | Placed, joint center set                          |
| Blue                  | Placed on surface, joint center not set           |
| Orange                | Next point to place                               |
| Additional white ring | Selected                                          |
| Translucent           | Right-side point driven by left under Live Mirror |

### 9.3 Estimated Points and Automatic Inference

Spine (`spine_01`–`spine_05`), upper-neck (`neck_02`), and clavicle (`clavicle_l` / `clavicle_r`) points are inferred using UE5 Manny proportions once pelvis, neck, head, shoulder, and other prerequisite points are placed. The panel skips them during manual placement.

Rules:

- They follow surrounding edits, updating once on mouse release, not during dragging.
- Dragging, adjusting depth, or aligning to the centerline turns an estimated point into a manually controlled point that stops updating. Points you manually place in between also serve as inference anchors.
- **Confirm This Point** and **Confirm All Estimated Points** preserve current positions.
- If prerequisite points are deleted or their order is reversed (for example, neck below pelvis), dependent estimated points are cleared for manual placement.

Estimated points do not block rigging. Validation lists them under **Suggestions** and provides **Check Estimated Landmarks**.

### 9.4 Manual Placement

1. Enable **Edit Landmarks**, preferably also **Joint Center** and **Live Mirror**.
2. Click the model according to **Next Point to Place** on the guidance card.
3. Centerline points (pelvis, spine, neck, head) automatically align to the body's centerline.

With Live Mirror, only the left side needs placement. Approximate order: pelvis → neck 1 → head → left shoulder → left elbow → left wrist → left fingers → left hip → left knee → left ankle → left ball of foot.

### 9.5 Joint Center

When enabled, clicking the surface searches along the viewing ray for the body's volume at that location and places the point inside it rather than on the surface. This is especially helpful for shoulders, elbows, wrists, hips, knees, and ankles.

The volume center is not always the best animation joint position: thick clothing, skirts, armor, and unusual proportions affect the result. Joint Center provides a quick starting point; manually adjust points that look wrong.

### 9.6 Dragging and Plane Constraints

Dragging moves a point within one plane, avoiding difficult simultaneous changes on three axes:

- Use **Front Plane** to adjust height and left/right position from the front.
- Use **Side Plane** to adjust front/back depth from the side.
- **View Plane** follows the current view; in hand view, it is the palm plane.

Enable **Show Plane Guide** to see the active plane. Changing viewport views does not automatically change a selected fixed plane.

### 9.7 Live Mirror

Enable it for approximately symmetrical models. Left-side edits update the right, whose points are translucent. Dragging a right-side point actually applies the edit through its corresponding left-side point.

### 9.8 Skeleton Preview

Preview shows the skeleton generated from current landmarks. Check that:

- Pelvis → spine → neck → head follows the body center.
- Clavicle → upper arm → forearm → hand passes through shoulder, elbow, and wrist.
- Thigh → calf → foot passes through hip, knee, and ankle.

If bones clearly miss real joints, adjust the corresponding landmarks.

## 10. Report Panel

### 10.1 Before Validation

Initially the report shows **Check Before Rigging** with **Validate Rigging**. Any landmark edit invalidates the previous report and requires revalidation.

### 10.2 Status Card

After validation or rigging, a colored card at the top shows a title, summary, and counts of **Errors / Warnings / Suggestions**.

**After validation:**

| Title                          | Meaning                                                      |
| ------------------------------ | ------------------------------------------------------------ |
| Basic Checks Passed            | No blocking issues; rigging can begin. Joint positions and deformation still need visual checks. |
| Ready to Rig — Review Warnings | Rigging is possible; review warnings and skeleton preview first. |
| Resolve Issues Before Rigging  | Blocking issues exist; follow Next Steps and revalidate.     |

**After rigging:**

| Title                                              | Meaning                                                      |
| -------------------------------------------------- | ------------------------------------------------------------ |
| Rigging Complete                                   | Automatic rigging completed. Open the generated character and preview animations. |
| Rigging Complete — Some Regions Used Basic Weights | Unreliably identified regions use basic weights; other regions retain advanced rigging (10.5). |
| Rigging Complete in Compatibility Mode             | An internal advanced-rigging error occurred or you selected compatibility mode; basic automatic weights were used throughout. |
| Skeleton Generated — Manual Skinning Required      | Only the skeleton was generated; automatic weights did not complete. |
| Skeleton Ready                                     | Result of Skeleton Only; manually add skin weights.          |
| Rigging Incomplete                                 | Failed; review the reason and Next Steps.                    |
| Rigging Cancelled                                  | You cancelled; restart whenever you wish.                    |

### 10.3 Report Sections

| Section                             | Contents                                                     |
| ----------------------------------- | ------------------------------------------------------------ |
| Auto Place                          | Appears immediately after Auto Place (7.3); disappears on next validation or landmark edit. |
| Check Rigging Results               | Inspection card after successful automatic rigging (Section 13). |
| Next Steps                          | Issue-specific action buttons (10.4); hidden when no action is required. |
| Rigging                             | One-sentence explanation of how rigging will proceed or was completed. |
| Errors                              | Blocking issues.                                             |
| Warnings                            | Non-blocking issues requiring attention.                     |
| Suggestions                         | Non-blocking advice, such as unconfirmed estimates or proportions differing substantially from Manny. |
| Diagnostics (for Technical Support) | Collapsed by default; technical details and Copy Full Report. Not needed for normal use. |

### 10.4 Next Steps Buttons

| Button                                      | Purpose                                                      |
| ------------------------------------------- | ------------------------------------------------------------ |
| Check Left Elbow (or another specific part) | Select point, enable Joint Center, and focus the viewport. Inspect front/side, adjust if needed, then revalidate. |
| Check Joint Landmarks                       | Open Landmarks to inspect joints from front and side.        |
| Check Estimated Landmarks                   | Select the first estimated point and enable Joint Center.    |
| Place Missing Landmarks                     | Select the first missing required point and show the full model. |
| Open Input Settings                         | Open Details to inspect Source Static Mesh.                  |
| Revalidate                                  | Run validation again.                                        |
| Rig in Compatibility Mode                   | Appears when advanced rigging could not complete (12.3).     |
| Copy Report for Support                     | Copy the full report to the clipboard.                       |

These buttons only help select and inspect; they do not automatically move, mirror, or confirm your landmarks.

### 10.5 Basic Weights in Some Regions

Starting in 1.1.0, when advanced rigging cannot reliably identify a body region (hips beneath a skirt, hands built from separate mesh islands, or arms inside loose sleeves), **only that region** switches to basic weights generated by UE Geodesic Voxel. The rest keeps advanced rigging. The report:

- Lists affected regions in warnings and recommends animations to test afterward, such as leg raises and squats.
- Notes that landmarks outside joint centers can also cause this, and provides inspection buttons in **Next Steps**.

This is not a failure, but affected weights are coarser. Prioritize animation testing and manual adjustment in these regions. Validation also tries to predict fallback in advance, for example, “Hands are expected to use basic weights.”

## 11. Output Panel

Use **Output** to set the destination and inspect generated assets.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648345.png)

- **Output Folder:** New assets use the project's **Default Output Folder**, `/Game/EasyAutoRig/Generated`. A character-specific folder such as `/Game/Characters/MyCharacter/` is recommended.
- **Generated Skeleton / Generated Skeletal Mesh / Generated Physics Asset:** Assets from this operation, named `SK_ModelName_Skeleton`, `SKM_ModelName`, and `PHYS_ModelName`. No Physics Asset is generated when that option is disabled.
- Collapsed categories below contain statistics from the last skinning and physics generation for troubleshooting.

## 12. Rigging, Compatibility Mode, and Skeleton Only

### 12.1 Rig

Clicking **Rig**:

1. Runs validation; blocking issues prevent the operation from starting.
2. If warnings exist, offers **View Report** (opens report without generating assets) or **Continue**.
3. Displays “Rigging character…” and generates the skeleton, automatic skinning, Skeletal Mesh, and Physics Asset in order, then checks output validity.
4. Shows results in the report and opens generated assets automatically (can be disabled in project settings).

### 12.2 How Automatic Skinning Is Selected

No manual algorithm selection is needed. Processing follows this order:

1. **Advanced rigging** (`SemanticFull` in diagnostics): Identifies head/neck, torso, shoulders, arms, elbows, wrists, hands, hips, thighs, knees, calves, feet, and other regions, then generates region-based weights. This is the highest-quality method.
2. **Basic weights in some regions:** Only regions that cannot be reliably identified use basic weights (10.5).
3. **Compatibility mode** (`GeodesicCompatibility`): If the model as a whole is unsuitable for advanced rigging, or an internal error occurs, UE Geodesic Voxel generates basic automatic weights for the whole model. On automatic fallback due to an internal error, the report asks you to send the full report to the author.
4. **Skeleton only:** If even basic weights cannot be validly generated, only the skeleton is committed and the report explains that manual skinning is needed.

All methods must pass the same validity checks before assets are written. All automatic weights are **initial weights** requiring manual adjustment afterward (Section 14). Basic and compatibility weights are coarser and need more adjustment.

### 12.3 Rig in Compatibility Mode

When the report says advanced automatic rigging could not complete, **Rig in Compatibility Mode** appears under **Next Steps**. Clicking it **runs rigging again**:

- Skips advanced body-region analysis and uses UE Geodesic Voxel for basic weights.
- Does not change your landmarks.
- Produces coarser weights; shoulders, hips, hands, and fingers need more manual adjustment.

This choice is not saved in the asset. Clicking **Rig** next time tries advanced rigging first again.

### 12.4 Skeleton Only

If you do not need automatic weights or intend to paint all weights yourself, click **Skeleton Only**. It generates a skeleton and a model asset for manual skinning (also a Physics Asset when enabled), without automatic weights. Paint weights later in UE, Blender, or Maya.

This still saves repetitive work on bone creation, names, hierarchy, twist bones, and IK bones.

## 13. Check Rigging Results

After successful automatic rigging, the report displays **Check Rigging Results**:

1. **Open Rigged Model:** Open the generated character in the Skeletal Mesh Editor.
2. **Choose a Preview Animation:** In **Preview Scene Settings**, set **Preview Controller** to **Use Specific Animation**, then select **Animation**. Use an animation compatible with or retargeted to this skeleton.
3. **Raise the Arms:** Inspect both shoulders and armpits for collapse, excessive stretching, or unintended chest movement.
4. **Bend Elbows and Knees:** Check for obvious pinching, collapse, or stretching.
5. **Bend the Fingers:** Use open/closed-hand animations; check that each finger bends at its own joints without unintentionally moving neighboring fingers.

If no suitable animation is available, set **Preview Controller** to **Reference Pose** and display the skeleton with **Character > Bones > All Hierarchy**. Inspect positions from front and side. A static pose cannot reveal deformation during bending.

If deformation is clearly wrong because bones are misplaced (for example, an elbow outside the bending joint), inspect and adjust the corresponding landmarks from front and side, then validate and rig again. Once positions are reasonable, manually edit weights to fix remaining deformation (Section 14). Animation problems can also originate in the animation itself; if the cause is unclear, copy the report for support.

## 14. Adjust Weights in UE5

EasyAutoRig generates **initial weights** to get characters moving and allow early tests; these are **not production-quality weights**. Usable weights (animations play without obvious mesh tearing) do not necessarily meet production standards. Manual adjustment remains necessary; the amount depends on topology, proportions, clothing, hair, and separate parts.

You can adjust directly in UE5 without exporting to Blender or Maya. UE 5.5's Skeletal Mesh Editor includes weight editing tools by default:

1. Open the generated Skeletal Mesh (or click **Open Rigged Model** in the report).
2. Click **Editing Tools**, switch to **Skin**, and choose **Edit Weights**.
3. Select a bone and paint with:
   - **Add:** Increase the selected bone's weight.
   - **Replace:** Replace weights with a specified value.
   - **Multiply:** Scale weights up or down proportionally.
   - **Relax:** Smooth weight transitions.
4. Alternatively select vertices and use **Mirror** (mirror weights to the opposite side), **Flood** (apply throughout the selection), **Prune** (remove tiny influences), or **Relax**.
5. Click **Accept** to apply, then save.

Recommended order:

1. Adjust while previewing arm raises, elbow bends, leg raises, squats, and fist animations.
2. Start with major joints: shoulders/armpits, elbows, wrists, hips/groin, knees.
3. Then fingers.
4. Finally clothing, hair, skirts, capes, and accessories.
5. For symmetrical characters, finish one side and **Mirror** to the other.

If **Editing Tools** is missing, enable **Skeletal Mesh Editing Tools** under **Edit → Plugins** and restart the editor. UI names may vary slightly by engine version and language.

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202610101700001.png)

## 15. Scripting and AI Interfaces

EasyAutoRig provides `EasyAutoRigEditorScriptingLibrary`, callable via Python (`unreal.EasyAutoRigEditorScriptingLibrary`) or Editor Blueprints in UE 5.5–5.8. It can read settings and landmarks, automatically place points, place/confirm/clear points, validate, rig, and read reports. It follows exactly the same rules as editor buttons: validation runs before rigging, and warnings require explicit acceptance.

In UE 5.8, when Toolset Registry is enabled, the plugin also registers AI tools and workflow skills. An AI assistant connected through MCP can follow: Auto Place → inspect listed points → validate → obtain your approval before rigging.

## 16. Recommended Workflow

For most standard humanoid models, focus on three things:

1. **Select a suitable Static Mesh**; configure non-five-finger hands first.
2. **Run Auto Place, then inspect and adjust landmarks**, especially the report's priority points and fingers.
3. **Decide based on the report:** rig directly, fix issues and revalidate, or use compatibility mode / Skeleton Only.

Then inspect actual animations and manually adjust weights in UE5 until they meet your project's requirements.