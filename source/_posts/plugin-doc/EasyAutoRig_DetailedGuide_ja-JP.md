---
title: EasyAutoRig 詳細使用ガイド
date: 2026/8/26 12:35:29
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648830.png
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648830.png
categories:
  - Unreal Engine
tag:
  - 工具
  - 插件
published: true
---

> まず一度の Rig を素早く完了したい場合は、 **{% post_link plugin-doc/EasyAutoRig_Tutorial_ja-JP Quick Start Guide %}** を先にご覧ください。このガイドでは、EasyAutoRig のインターフェース、各タブの役割、モデル選択から最終 Asset の生成までの流れをより詳しく説明します。

## 1. EasyAutoRig とは

EasyAutoRig は Unreal Engine 向けの人型キャラクター自動リギングプラグインです。

条件を満たす **人型 Static Mesh** を、Unreal Engine 内で引き続き使用できる Rig 済みキャラクターへ素早く変換し、現在の設定に応じて以下を生成できます。

- Skeleton
- Skeletal Mesh
- 自動 Skin Weight
- 任意の Physics Asset
- UE5 スタイルの Twist Bone
- UE5 スタイルの IK Bone と補助 Bone

Blender や Maya などの DCC ソフトで完全な Skeleton を手作業で作成してから Unreal Engine にインポートする必要はありません。

EasyAutoRig の基本的な流れは次の通りです。

> Static Mesh を選択 → Landmark を配置 → Bone の位置を調整 → Validate Rig → Rig → 生成結果を確認

Landmark はこのワークフローで最も重要な入力です。Landmark の位置は最終的な Skeleton のフィッティングに利用されるため、Landmark を適切に配置するほど、その後の Skeleton 生成、自動 Skinning、Physics Asset 生成の基礎が安定します。

## 2. A Pose / T Pose の人型モデルのみ対応、および向きの要件

EasyAutoRig は現在、**T Pose** と **A Pose** の標準的な人型モデルのみをサポートしています。

推奨条件：

- 二足歩行の人型
- 左右がおおむね対称
- T Pose または A Pose
- キャラクターの正面がワールド `+Y`
- ワールド `+Z` が上方向
- 左右方向が `X`
- 人体本体がモデルのローカル原点付近

つまり：

```text
+Y = Forward
+Z = Up
X  = Left / Right
```

座り姿勢、走り姿勢、戦闘 Pose、腕を交差した Pose、片脚を上げた Pose などの任意 Action Pose は、現在の正式サポート対象ではありません。

これは、EasyAutoRig が T Pose / A Pose の比較的安定した人体の空間関係を利用して、左右、腕、脚、膝、胴体などの領域を判定するためです。

モデルには衣服、靴、髪、スカート、マント、尻尾、アクセサリーを含めることができ、複数の独立した Mesh Component で構成されていても構いません。裸のベースメッシュである必要はありません。

## 3. EasyAutoRig Asset を作成

Content Browser で右クリックし、**Animation → EasyAutoRig** を選択すると EasyAutoRig Asset を作成できます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648335.png)

作成後は、プロジェクトの命名規則に合わせて名前を変更できます。例：`EAR_CharacterName`、`AR_CharacterName`

Asset をダブルクリックすると、EasyAutoRig 専用 Editor が開きます。

この Asset には、現在選択しているモデル、Landmark、Preview 状態、Output Directory、そのほかの関連設定が保存されます。基本的には 1 キャラクターにつき 1 つの EasyAutoRig Asset を作成しておくと、後から再度開いて調整しやすくなります。

## 4. Details Panel

EasyAutoRig Asset を開くと、まず右側に Details Panel が表示されます。通常、実際に変更する必要がある設定は多くありません。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648183.png)

### 4.1 Source Static Mesh を選択

最も重要な設定は **Source Static Mesh** です。

ここで Rig したい人型 Static Mesh を選択します。選択するとモデルがすぐに Viewport に表示されます。

この時点で、まず以下を確認してください。

- T Pose または A Pose か
- 正面が +Y を向いているか
- 左右がおおむね対称か
- 人体の位置が適切か

これらの基本条件に問題がなければ、Landmark の配置に進めます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648504.png)

### 4.2 その他の設定は通常デフォルトのままで構いません

EasyAutoRig には標準的な UE5 人型キャラクター向けのデフォルト設定が用意されているため、ほとんどの場合、その他のパラメータはそのままで構いません。

モデルが標準的な 5 本指の手であれば、Hand / Finger 関連設定を変更する必要は通常ありません。

指の本数が 5 本ではない場合、または手の構造が標準的な人型と異なる場合のみ、実際のモデルに合わせて Finger 設定を調整してください。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648965.png)

その他の **Auto Skinning、Physics、Output** などの設定も、まずはデフォルトのまま使用することをおすすめします。Output 方法、Skinning 方法、Physics Asset の動作、その他のパラメータを明確に変更したい場合のみ調整してください。

そのため、初めて使用する場合は通常：

> **Source Static Mesh を選択したら、そのまま Landmark タブに進む**

だけで十分です。

## 5. Landmark タブ

Landmark タブは EasyAutoRig の主要な編集領域です。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648257.png)

ここにあるボタンのほとんどには Tool Tip があります。マウスカーソルをボタンの上に置くと、その機能の説明を確認できます。ボタンの役割が分からない場合は、まず Tool Tip を確認してください。

### 5.1 Edit Landmarks

**Edit Landmarks** を有効にすると、モデル上に Landmark を配置できるようになります。

次に配置する必要がある位置は黄色で表示されます。

例えば現在 `pelvis` と表示されている場合、モデル上の pelvis に対応する位置をクリックすると、その Landmark の配置が完了し、次の Landmark に進みます。

### 5.2 Landmark Names

**Landmark Names** を有効にすると、Viewport に Landmark 名を直接表示できます。

Landmark の数が多い場合でも、現在調整しているのが pelvis、spine、clavicle、elbow、knee など、どの位置なのかをすぐ確認できます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648234.png)

### 5.3 Landmark の位置が主要 Bone の位置になります

Landmark は単なる参考点ではありません。

最終的な Skeleton Fitting に直接利用されるため、簡単に言えば：**Landmark を置いた位置が、対応する主要 Bone Joint の最終位置になります。**

例：

- `lowerarm` が Elbow Joint の位置を決める
- `calf` が Knee Joint の位置を決める
- `hand` が Wrist Joint の位置を決める
- `pelvis`、`spine`、`neck` が人体の Center Chain に影響する

そのため、1 つの角度だけで全 Landmark の配置を完了することはおすすめしません。Perspective、Front、Left View を切り替えながら、複数方向から位置を確認してください。

### 5.4 Joint Center

**Joint Center** を有効にすると、EasyAutoRig はクリックしたモデル表面から、現在の局所体積の中心方向へ Landmark を移動するように補助します。

これは Shoulder、Elbow、Wrist、Hip、Knee、Ankle などの Joint に特に役立ちます。

例えば Front View から膝の表面をクリックした場合、実際の Knee Joint はモデルの最前面ではなく、脚の内部にあるのが一般的です。Joint Center は Landmark をそのような内部 Joint Center に近づけるための補助になります。

ただし、モデルの構造はそれぞれ大きく異なります。

厚い衣服、スカート、Armor、特殊な体型などがある場合、自動で計算された体積中心が **見た目や Animation 上で最適な位置とは限りません**。

そのため Joint Center は、素早く妥当な初期位置を得るための機能として利用し、位置が理想的でない場合は手動で調整してください。

### 5.5 Joint Editing と移動制限 Plane

Landmark を手動で移動する場合、Joint Editing 関連設定で移動を制限する Plane を選択できます。

これにより、ドラッグ中に 3 軸すべてが同時に自由移動して位置調整が難しくなるのを防げます。

例えば：

- Front から左右・上下を調整する場合は Front Plane に制限
- Side から前後 Depth を調整する場合は対応する Side Plane に切り替え

**Plane Guide** と組み合わせると、現在の編集 Plane をより直感的に確認できます。

この方法は Shoulder、Elbow、Wrist、Hip、Knee、Ankle の調整に特に便利です。

### 5.6 Live Mirror

モデルが左右ほぼ対称であれば、Live Mirror をそのまま有効にしてください。

片側の Landmark を調整すると反対側も同期されるため、重複作業を大きく減らせます。

### 5.7 Skeleton Preview

Skeleton Preview を有効にすると、現在の Landmark から生成される Bone の位置を直接確認できます。

主に以下を確認してください。

- pelvis → spine → neck → head が人体中心に沿っているか
- clavicle → upperarm → lowerarm → hand が Shoulder、Elbow、Wrist を通っているか
- thigh → calf → foot が Hip、Knee、Ankle を通っているか

Bone が実際の Joint から明らかにずれている場合は、Landmark を引き続き調整してください。

## 6. Report タブ

Landmark の配置が完了し、Skeleton Preview がほぼ正しく見えるようになったら、**Validate Rig** をクリックします。

EasyAutoRig は現在のモデルに対して Rig 前のチェックを行い、その結果を Report タブに表示します。

Validate Rig の目的は最終 Asset を生成することではなく、実際の Rig の前にできるだけ以下を知らせることです。

- 現在のモデルで Rig を続行できるか
- Blocking Error があるか
- Warning があるか
- どの自動 Skinning Route が使用されるか
- Rig 後に重点的に確認すべき領域があるか

### 6.1 Ready

Status が緑色の Ready であれば、Rig を妨げる明確な問題は検出されていません。

そのまま Rig をクリックして続行できます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261648635.png)

### 6.2 Yellow / Ready, Review Warnings

Status が黄色で、例えば以下のように表示されている場合：

> **Ready to Rig, Review Warnings**

これは失敗ではありません。

現在も有効な Rig Route が存在しますが、一部領域で Backup Method を使用している、または高度な Semantic Skinning が現在のモデルに適していない可能性があります。

例：

```text
SemanticFull: Unavailable
AutoSkin Mode: GeodesicCompatibility
```

これは EasyAutoRig が UE Geodesic Voxel Compatibility Skinning Route を使用することを意味します。

この場合でも Rig を続行できます。

完了後は Report の内容に従い、各 Joint を重点的に確認することをおすすめします。

### 6.3 Red / Cannot Rig

Status が赤色の場合、現在の Rig Workflow を妨げる問題が検出されています。

Report の内容に従って以下を確認してください。

- Model Pose
- Orientation
- Landmark
- Joint Center
- Skeleton Preview

問題を修正した後、再度 Validate Rig を実行してください。

### 6.4 Report で重点的に見る項目

通常の使用では、主に以下を確認します。

- Status
- Summary
- Errors
- Warnings
- Recommendations
- AutoSkin Mode

内部アルゴリズムの名前を理解する必要はありません。

後でプラグイン内部の問題が発生して報告が必要な場合は、完全な Report と `LogEasyAutoRig` を提供してください。最終的なフォールバックとして Skeleton Only を使用できます。

## 7. Output タブ

Output タブは、最終的に生成された Asset の管理と確認に使用します。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261649271.png)

### 7.1 Output Directory を設定

最終 Asset の生成先 Directory を設定できます。例：`/Game/Characters/MyCharacter/`

これにより Skeleton、Skeletal Mesh、Physics Asset をキャラクター専用 Directory にまとめて保存できます。

### 7.2 生成された Asset を確認

Rig 完了後、Output タブで今回生成された Asset を確認できます。

通常は：

- Skeleton
- Skeletal Mesh
- Physics Asset

が含まれます。

Physics Asset Generation を有効にしていない場合は、現在の設定で必要な Asset のみ生成されます。

Output タブでは、Asset が正常に生成されたか、どこに保存されたか、今回何が生成されたかを素早く確認できます。

## 8. Rig と Skeleton Only

Landmark の調整を完了し、**Validate Rig** を通過したら、最終 Rig を実行できます。

### 8.1 Rig

**Rig** をクリックします。

EasyAutoRig は完全な Rig Workflow を開始します。

現在のモデルと設定に応じて、以下を実行する場合があります。

- Skeleton Generation
- AutoSkin Route Selection
- Automatic Skin Weight Generation
- Skeletal Mesh Generation
- Physics Asset Generation
- Final Output Validation

モデルが高度な Semantic Skinning に適している場合は SemanticFull を使用します。

SemanticFull が適していなくても UE Geodesic Voxel で正常に処理できる場合は GeodesicCompatibility を使用します。

完了後は Output タブで生成結果を確認できます。

### 8.2 Skeleton Only

自動 Weight が不要な場合、または現在のモデルに適した AutoSkin Route がない場合は、**Skeleton Only** を選択できます。

この機能は主に、最終的な自動 Skinning 結果に依存せず、EasyAutoRig で UE5 スタイルの Skeleton だけを自動生成するために使用します。

その後、Unreal Engine、Blender、Maya で Skin Weights を手動調整できます。

UE5 スタイルの Skeleton を素早く取得したい場合、または最初から自分で Weight Paint を行う予定であれば、Skeleton Only がより適しています。

## 9. 推奨操作順

ほとんどの標準人型モデルでは、Details Panel のその他のパラメータはデフォルトのままで構いません。

特に重要なのは次の 3 点です。

1. **要件を満たす正しい Static Mesh を選ぶ**

2. **Landmark を正確に配置する**

3. **Report を確認し、Rig を続けるか Skeleton Only を使用するか判断する**
