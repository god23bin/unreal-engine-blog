---
title: 人体の Landmark をより適切に配置するにはどうすればよいでしょうか？
date: 2026/9/29 18:00:28
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png
categories:
  - Unreal Engine
tag:
  - 工具
  - 插件
published: true
---

EasyAutoRig を使用するうえで、最も重要な操作は Landmark（ランドマーク）の配置です。簡単に言えば、配置した Landmark の位置が最終的なボーンの位置になります。

> **{% post_link plugin-doc/EasyAutoRig_DetailedGuide_ja-JP EasyAutoRig 詳細使用ガイド %}**
>
> **{% post_link plugin-doc/EasyAutoRig_FAQ_ja-JP EasyAutoRig FAQ / よくある質問 %}**

## では、人体の Landmark をより適切に配置するにはどうすればよいでしょうか？

人体の Landmark をより適切に配置する方法を理解する前に、3D モデルのリギングにおける重要な原則を一つ理解しておく必要があります。**ボーンはできるだけキャラクターの身体の体積中心に近い位置へ配置します。**

あわせて、UE5 標準スケルトンが見た目としてどのような構造になっているのかも理解しておく必要があります。

UE5 標準スケルトンは以下のとおりです。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801943.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801689.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801738.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png)

見てわかるとおり、首は neck_01 と neck_02 によって制御されています。位置は以下の画像のとおりです。以降の画像に表示される緑色の線は、基準となる位置の断面を示しています。ご自身のキャラクターでも、対応する位置にこの 2 本のボーンを配置してください。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302233314.png)

胸郭部分は主に spine_04 によって制御され、ウェイトは主に spine_04 と spine_05 が存在する胸部周辺に割り当てられます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302236403.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325077.png)

腰部は主に spine_01 から spine_03 によって制御されます。この部分はより細かく制御されるため、ボーン同士の間隔も比較的狭くなっています。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325498.png)

肩のボーンである clavicle は主に鎖骨の位置にあります。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325130.png)

upperarm は人体の肩関節付近に配置されます（緑色の枠が該当する位置を示しています）。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325016.png)

lowerarm は人体の肘関節付近に配置されます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325413.png)

hand は手首付近に配置されます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325628.png)

pelvis は人体の股関節（臀部周辺）に位置します。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325022.png)

その隣に thigh があり、太ももの付け根に配置されます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325967.png)

続いて calf は膝付近に位置し、下腿を制御します。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302325210.png)

foot は足首付近に配置されます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326792.png)

ball は足の前足部に配置されます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326912.png)

## Bone と Joint の違い

**ここでは Bone と Joint という 2 つの概念に注意してください。3D モデリングや 3D リギングに慣れていない方、または Blender だけに慣れている方にとっては、この部分が少し分かりづらいかもしれません。簡単に理解すると、UE では Bone は視覚的には球体として表現されます。UE 上で作成するときは、その点を Joint、つまり関節の位置として扱います。2 つの Joint の間に表示される円錐状の部分は、従来の骨の見た目を模して描画された視覚的な接続線だと考えることができます。一般的には、それぞれの Joint 自体も Bone と呼ばれることが多く、この球体の位置が実質的なピボットポイントになります。UE は Joint Based System であり、重要なのは関節そのものの位置であって、長さを持つ一本の骨そのものではありません。**

**そのため、Landmark の配置も同じ考え方になります。もちろん絶対的なルールではありません。モデルごとに体型や比率が異なるため、できるだけ UE5 標準スケルトンの位置と全体的な流れに近づけて配置することが重要です。言い換えると、ご自身のモデル上で解剖学的に自然な関節位置へ Landmark を配置するようにしてください。**

**衣服のないベースボディの例として、ここでは UE Manny を使用します。Landmark を配置すると、以下のようになります。**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326524.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326285.png)

**「Joint Center（関節中心）」を有効にすることを忘れないでください。これにより、Landmark を身体の体積中心に配置しやすくなります。**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326402.png)

計算結果に誤差がある場合は、手動で調整できます。Landmark パネルで Landmark の移動平面を制限し、ドラッグして位置を微調整してください。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326339.png)

## 配置例

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