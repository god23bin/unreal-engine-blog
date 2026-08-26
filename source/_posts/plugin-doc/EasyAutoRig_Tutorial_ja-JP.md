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

## 1. EasyAutoRig とは

EasyAutoRig は Unreal Engine 向けの人型キャラクター自動リギングツールです。

条件を満たす **人型 Static Mesh** から、UE5 の標準人型 Skeleton の構成に準拠した Rig 結果をすばやく生成することを目的としています。生成内容には以下が含まれます。

- フィッティング済みの人型 Skeleton
- Skeletal Mesh
- 自動 Skin Weight
- 任意の Physics Asset
- UE5 標準スタイルの補助 Bone、Twist Bone、IK Bone

使用時に、Blender や Maya などの DCC ソフトで完全な Skeleton を手動作成する必要はありません。

基本的な流れは次のようになります。

> Static Mesh をインポート → 人体 Landmark を配置 → Joint Center を調整 → Validate → Rig → Skeletal Mesh を取得

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

ただし、モデル構造が複雑になるほど、自動 Semantic Skinning で認識できる領域が少なくなる場合があります。

EasyAutoRig はモデルの実際の構造に応じて、異なる Skinning 方法を選択します。

そのため：

> **Rig できるからといって、すべてのモデルが完全に同じ自動 Skinning アルゴリズムを使用するとは限りません。**

これは正常な動作です。

## 4. 使用チュートリアル

### 4.1 EasyAutoRig Asset を作成

Content Browser で右クリックし、**Animation → EasyAutoRig** を選択すると EasyAutoRig Asset を作成できます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261536066.png)

Asset の名前を変更し、完了したらダブルクリックして開きます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261537233.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539014.png)

### 4.2 A-Pose または T-Pose の Static Mesh を選択

Details Panel で **Source Static Mesh** に、Rig したい人型キャラクターモデルを設定します。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539791.png)

選択すると、モデルが Viewport に表示されます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261539469.png)

### 4.3 Landmark の配置と調整を開始

上部 Toolbar の **Edit Landmarks、Landmark Names、Joint Center、Live Mirror、Skeleton Preview** をすべて有効にします。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261705336.png)

これで Landmark の配置を開始できます。

Landmark は Perspective View、Left View、Front View のいずれでも配置できます。

> Perspective View のショートカット：Alt + G、Left View：Alt + K、Front View：Alt + H

#### Landmark を配置

黄色の Landmark は、次に配置する必要がある Landmark を示します。

下の例では、次に配置するのは `pelvis` Landmark です。

配置したい位置をマウスでクリックしてください。人体のセンターライン上にある Landmark は、自動的にセンターラインへスナップします。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261540880.png)

配置が完了すると Landmark は緑色になります。

緑色のワイヤーフレームは補助線で、Landmark を移動するときに現在どの Plane 上で操作しているかを確認できます。

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

Front View で確認します。

いくつかの Landmark の位置は調整が必要な場合があります。

Landmark を直接ドラッグして位置を調整してください。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542833.png)

調整後は、下の画像のような状態になります。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542367.png)

### 4.4 Validate Rig

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542969.png)

**Validate Rig** をクリックすると、現在の Rig に関する情報を確認できます。

自動 Skinning に失敗した場合、最終的なフォールバックとして **Skeleton Only** をクリックし、その後 Skin Weight を手動で一からペイントできます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261542718.png)

### 4.5 Rig を実行

**Rig** ボタンをクリックし、Rig 処理が完了するまで待ちます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543611.png)

完了後、Output Panel で生成された Asset を確認できます。

Output Directory を自由に設定することもできます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543298.png)

## 5. 結果

このモデルには、UE5 スタイルの Skeletal Mesh と自動 Skin Weight が生成されています。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543089.png)

ゲームで使用できる Physics Asset も生成されます。

**Simulate** をクリックすると Physics の動作を確認できます。

結果が理想的でない場合でも、通常は Rigid Body の位置と Scale を少し調整するだけで十分です。Rigid Body 間の Constraint は基本的に調整する必要はありません。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202608261543682.png)
