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

## では、人体の Landmark をより適切に配置するにはどうすればよいでしょうか？

人体の Landmark をより適切に配置する方法を理解する前に、まず UE5 標準スケルトンが見た目としてどのような構造になっているのかを理解しておく必要があります。

UE5 標準スケルトンは以下のとおりです。

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801943.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801689.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801738.png)

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291801084.png)

見てわかるとおり、首は neck_01 と neck_02 によって制御されています。

胸郭部分は主に spine_04 によって制御され、ウェイトは主に spine_04 と spine_05 の間にある胸部の領域へ割り当てられます。腰部は主に spine_01 から spine_03 によって制御されます。この部分はより細かく制御されるため、各ボーンの間隔も比較的狭くなっています。また、これらの spine ボーンは基本的にメッシュの体積中心付近に配置されています。

肩のボーンである clavicle は主に鎖骨の位置にあります。upperarm は肩関節付近、lowerarm は肘関節付近、hand は手首付近に配置されています。

pelvis は人体の股関節（臀部周辺）に位置します。その隣に thigh があり、太ももの付け根に配置されています。続いて calf は膝付近に位置し、下腿を制御します。foot は足首付近、ball は足の前足部付近に配置されています。

これらのボーンは、基本的に身体の体積中心付近に位置しています。

そのため、Landmark も同じ考え方で配置するのが基本です。もちろん絶対的なルールではありません。モデルごとに体型や比率が異なるため、できるだけ UE5 標準スケルトンの位置と全体的な流れに近づけて配置することが重要です。

**衣服のないベースボディの例として、ここでは UE Manny を使用します。Landmark を配置すると、以下のようになります。**

![](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202609291844839.png)

## 配置例

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
