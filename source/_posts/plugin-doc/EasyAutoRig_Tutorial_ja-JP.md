---
title: EasyAutoRig 使用チュートリアル
date: 2026/8/26 12:35:26
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png
categories:
  - Unreal Engine
tag:
  - 工具
  - 插件
published: true
---
**{% post_link plugin-doc/EasyAutoRig_DetailedGuide_ja-JP EasyAutoRig 詳細使用ガイド %}**

**{% post_link plugin-doc/EasyAutoRig_FAQ_ja-JP EasyAutoRig FAQ / よくある質問 %}**

## 1. EasyAutoRig とは

EasyAutoRig は Unreal Engine 向けの人型キャラクター自動リギングツールです。

条件を満たす **人型 Static Mesh** から、UE5 の標準人型 Skeleton の構成に準拠した Rig 結果をすばやく生成することを目的としています。生成内容には以下が含まれます。

- フィッティング済みの人型 Skeleton
- Skeletal Mesh
- 自動 Skin Weight
- 任意の Physics Asset
- UE5 標準スタイルの補助 Bone、Twist Bone、IK Bone

使用時に、Blender や Maya などの DCC ソフトで完全な Skeleton を事前に手動作成する必要はありません。

基本的な流れは次のようになります。

> Static Mesh をインポート → 人体 Landmark を配置 → Joint Center を調整 → Validate → Rig → Skeletal Mesh を取得

### 1.1 EasyAutoRig の位置づけ：より早く Rig を完成させるためのツールであり、すべての手作業を置き換えるものではありません

始める前に、ひとつ明確にしておきたい点があります。

> **EasyAutoRig は「ワンクリックですべてのキャラクターに完璧な Production Ready Skin Weight を生成する」ことを保証する自動 Skinning ツールではありません。**

Auto Rig と Auto Skinning は、**高品質なスタート地点**として考えるのが適切です。

EasyAutoRig は、次のような繰り返しで時間のかかる作業をできるだけ省くことを目的としています。

- UE5 スタイルの人型 Skeleton を一から構築する
- Twist、IK、補助 Bone を設定する
- 初期 Skin Weight を生成する
- Physics Asset を生成する
- Final Rig の前に、現在のモデルがこのワークフローに適しているか確認する

これにより、基本的な Rig 作業だけに多くの時間を使うのではなく、Static Mesh キャラクターを Unreal Engine の Animation Test や Gameplay Prototype により早く投入できます。

キャラクターごとに Topology、体型、衣服、髪、スカート、Detached Component などは異なるため、自動 Skinning の最終品質も同じではありません。

生成後そのまま Prototype や一般的な Animation Test に使えるモデルもあれば、Shoulder、Elbow、Hip、Knee、Finger、Clothing などをさらに手動調整したほうがよいモデルもあります。

そのため、EasyAutoRig のワークフローは次のように考えることをおすすめします。

> **Skeleton と初期 Skinning を素早く完成 → できるだけ早く Animation / Gameplay をテスト → 本当に問題がある領域だけを手動調整**

次のように考えるものではありません。

> **一度クリックすれば → すべてのモデルで確認不要の最終 Weight が完成**

キャラクターの Deformation Quality が重要なプロジェクトでは、Rig 完了後も実際の Animation でキャラクターをテストし、必要に応じて Skin Weight を調整してください。

## 2. 使用前：モデルに必要な条件

EasyAutoRig は現在、主に **標準的で左右対称な人型キャラクター** を対象としています。

入力モデルは以下の条件を満たすことをおすすめします。

- 人型キャラクター
- T Pose または A Pose
- 左右がおおむね対称
- キャラクターの正面がワールド `+Y`
- ワールド `+Z` が上方向
- 人体の左右中心が `X = 0`
- 人体本体がモデルのローカル原点付近
- 腕や脚が明確に交差していない
- 座り姿勢、走り姿勢、戦闘 Pose などの任意 Pose ではない

## 3. 裸のベースメッシュである必要はありません

キャラクターには以下を含めることができます。

- 衣服
- 靴
- 髪
- スカート
- マント
- 尻尾
- アクセサリー
- 複数の独立した Mesh Component

ただし、モデル構造が複雑になるほど、自動 Semantic Skinning で安定して認識できる領域が少なくなる場合があります。

EasyAutoRig はモデルの実際の構造に応じて、異なる Skinning 方法を選択します。

そのため：

> **Rig できるからといって、すべてのモデルが完全に同じ自動 Skinning アルゴリズムを使用するとは限らず、すべてのモデルで同じ Weight Quality が得られるとも限りません。**

これは正常な動作です。

比較的標準的な人型モデルでは、EasyAutoRig は可能な限り完全な Semantic Skinning Workflow を使用します。モデル構造が Full Semantic Skinning に適していない場合は、UE Geodesic Voxel Compatibility Route を使用できます。

どの Auto Skinning Route を使用した場合でも、最終的には実際の Animation で Shoulder、Elbow、Hip、Knee など主要な Deformation Area を確認することをおすすめします。局所的な結果が十分でない場合は、その部分だけ Skin Weight を手動修正してください。

## 4. 使用チュートリアル

### 4.1 EasyAutoRig Asset を作成

Content Browser で右クリックし、**Animation → EasyAutoRig** を選択すると EasyAutoRig Asset を作成できます。

![EasyAutoRig Asset を作成](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261536066.png)

Asset の名前を変更し、完了したらダブルクリックして開きます。

![Asset の名前を変更](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261537233.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539014.png)

### 4.2 A-Pose または T-Pose の Static Mesh を選択

Details Panel で **Source Static Mesh** に、Rig したい人型キャラクターモデルを設定します。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539791.png)

選択すると、モデルが Viewport に表示されます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539469.png)

### 4.3 Landmark の配置と調整を開始

上部 Toolbar の **Edit Landmarks、Landmark Names、Joint Center、Live Mirror、Skeleton Preview** をすべて有効にします。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261705336.png)

これで Landmark の配置を開始できます。Landmark は Perspective View、Left View、Front View のいずれでも配置できます。

> Perspective View のショートカット：Alt + G、Left View：Alt + K、Front View：Alt + H

#### Landmark を配置

黄色の Landmark は、次に配置する必要がある Landmark を示します。

下の例では、次に配置するのは `pelvis` Landmark です。

配置したい位置をマウスでクリックしてください。人体のセンターライン上にある Landmark は、自動的にセンターラインへスナップします。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png)

配置が完了すると Landmark は緑色になります。緑色のワイヤーフレームは補助線で、Landmark を移動するときに現在どの Plane 上で操作しているかを確認できます。

次に `spine_01` を配置し、同じように続けます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540144.png)
![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540420.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541683.png)

`clavicle_l` は鎖骨の位置に配置します。

Live Mirror が有効になっているため、右側の対応 Landmark も自動的に同期して配置されます。

そのため、左側の Landmark だけを配置すれば、右側は自動的にミラーされます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541859.png)

左腕の Landmark を配置します。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541253.png)

指の Landmark を配置します。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541954.png)
![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261541314.png)

脚の Landmark を配置します。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542257.png)

#### Landmark を調整

Front View で確認すると、いくつかの Landmark の位置は調整が必要な場合があります。

Landmark を直接ドラッグして位置を調整してください。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542833.png)

調整後は、下の画像のような状態になります。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542367.png)

### 4.4 Validate Rig

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542969.png)

**Validate Rig** をクリックすると、現在のモデルの Rig 前チェック結果を確認できます。

Validation 情報では、現在のモデルで Rig を続行できるか、確認すべき Warning があるか、プラグインがどの Auto Skinning 方法を使用する予定かを確認できます。

続行可能と表示されていれば、そのまま Rig を実行できます。

ここでもう一度強調しておきます。

> **Validation を通過したということは、現在 Rig Workflow を妨げる問題が見つかっていないという意味であり、最終的な自動 Weight に手動確認が一切不要という意味ではありません。**

Rig 完了後も、実際の Animation で主要 Joint の Deformation を確認してください。

現在のモデルが Auto Skinning に適していない場合は、最終的なフォールバックとして **Skeleton Only** を使用できます。まず UE5 スタイルの Skeleton を生成し、その後 Skin Weight を一から手動で Paint できます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542718.png)

### 4.5 Rig を実行

**Rig** ボタンをクリックし、Rig 処理が完了するまで待ちます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543611.png)

完了後、Output Panel で生成された Asset を確認できます。Output Directory を自由に設定することもできます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543298.png)

## 5. 結果と、その後の確認

このモデルには、UE5 スタイルの Skeletal Mesh と自動生成された初期 Skin Weight が用意されました。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543089.png)

「Rig が成功した」ことだけで終わらせず、いくつかの実際の Animation を再生して、次の点を確認することをおすすめします。

- 腕を上げたとき Shoulder が自然に変形するか
- 腕を曲げたとき Elbow が正常に変形するか
- 脚を上げたとき Hip が大きく潰れないか
- 脚を曲げたとき Knee が正常に変形するか
- Finger、Clothing、Hair など特殊な領域に追加調整が必要か

これらの領域が現在のプロジェクト要件を満たしていれば、そのまま使用できます。

一部の変形が十分でない場合は、自動 Weight をスタート地点として、本当に問題がある領域だけを修正してください。Skeleton を一から作成し、すべての Weight をゼロから Paint するよりも、通常は大幅に時間を節約できます。

EasyAutoRig は、ゲーム開発の実用的なスタート地点として使える Physics Asset も生成します。

**Simulate** をクリックすると Physics の動作を確認できます。結果が理想的でない場合は、キャラクターの体型に合わせて Rigid Body の位置と Scale を調整し、プロジェクトの実際の要件に応じてさらにテストしてください。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543682.png)

最終的には、次のように考えることをおすすめします。

> **EasyAutoRig は 0 → 1 を素早く完成させ、キャラクターをできるだけ早くゲーム内で動かすためのツールです。最終的にどこまで Deformation Quality を高めるかは、プロジェクトの要件に応じて調整してください。**
