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

> **{% post_link plugin-doc/EasyAutoRig_DetailedGuide_ja-JP EasyAutoRig 詳細使用ガイド %}**
>
> **{% post_link plugin-doc/EasyAutoRig_FAQ_ja-JP EasyAutoRig FAQ / よくある質問 %}**

EasyAutoRig を使用するうえで、最も重要な操作は Landmark（ランドマーク）の配置です。簡単に言えば、配置した Landmark の位置が最終的なボーンの位置になります。

> **1.1.0 のヒント**：まずツールバーの「自動配置」をクリックして体と指のマーカーをプラグインに配置させ、その後この記事の基準で 1 つずつ確認・調整できます。特に「レポート」の「まず確認」に挙げられたマーカーを確認してください。背骨、首の上部、鎖骨のマーカーは周囲のマーカーから自動で計算されます。指は「マーカー」パネルの「手のビュー」で単独表示できます。

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

**「ジョイントセンター（Joint Center）」を有効にすることを忘れないでください。これにより、Landmark を身体の体積中心に配置しやすくなります。**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326402.png)

計算結果に誤差がある場合は、手動で調整できます。「マーカー」パネルの「ジョイントセンター」セクションで「正面平面」または「側面平面」を選んで Landmark の移動平面を制限し、ドラッグして位置を微調整してください。「奥行き -」「奥行き +」で奥行きを微調整することもできます。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609302326339.png)

## 正面と側面から確認する

すべてのマーカーを少なくとも 2 方向から見てください。**正面から高さと左右の位置を、側面から奥行きを確認します。**

注意：EasyAutoRig のキャラクターは `+Y` を向いていますが、UE のビューメニューの「前 / 後 / 左 / 右」は UE 自身の座標軸に基づく名前なので、キャラクターの向きと一致しません。

| 見たいもの                       | UE 5.5                                   | UE 5.8                           |
| -------------------------------- | ---------------------------------------- | -------------------------------- |
| キャラクターの正面（顔が見える） | 「右（Right）」ビュー、`Alt + Shift + K` | 「左（Left）」ビュー、`Alt + K`  |
| キャラクターの側面               | 「前（Front）」ビュー、`Alt + H`         | 「前（Front）」ビュー、`Alt + H` |

ほかのバージョンでは画面で判断してください。キャラクターの顔が見えていれば正面です。

## 指の Landmark

各指の最初のマーカーは**指と手のひらがつながる関節**に、残りのマーカーは指先に向かって順番に**指の曲がる関節**に置きます。すべて指の内部に置き、指先には置かないでください。

指は小さいので、「マーカー」パネルの「手のビュー」を使うのがおすすめです。「左手の甲」または「左手のひら」をクリックすると、ビューポートにはその手だけが指を上に向けて表示されます。このときクリックはその手にだけ当たり、「ジョイントセンター」がオンならドラッグは手のひらの平面に沿って動きます。手の甲のビューで指の左右の並びを確認し、側面から奥行きを確認します（指のマーカーは指の厚みの中央に置きます）。終わったら「モデル全体を表示」で戻ります。

## 自動配置の後に重点的に確認すること

自動配置のマーカーは関節に近い位置にありますが、次のケースはもう一度確認する価値があります。

- 「レポート」の「まず確認」に挙げられたマーカー：左右の検出が一致しなかったマーカー、首から高さを推定した頭のマーカー、奥行きが推測値のマーカー
- 肩（upperarm）：側面から、肩の表面や上腕の中ほどではなく、肩関節の内部にあるか
- 股関節（thigh）：スカートやコートを着ている場合、スカートの上ではなく太ももの付け根の関節内にあるか
- 手首（hand）：手に小道具を持っている場合、前腕と手の間にあるか
- 足首（foot）：ロングブーツを履いている場合、下腿と足の間の関節内にあるか
- 指：レポートで指が配置されなかったと表示された場合や、指のマーカーが関節からずれて見える場合は、手のビューで調整します

位置に問題がなければ、「マーカー」パネルで「ポイントを確定」または「推定をすべて確定」をクリックします。

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